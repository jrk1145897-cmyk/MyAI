---
name: meeting-notes
description: Process meeting transcripts to create Notion meeting summaries and action items. Use this skill when the user says "meeting notes", "process this meeting", "summarize this transcript", shares a meeting transcript or recording notes, or wants to extract action items from a meeting. Also trigger when user pastes text that looks like meeting dialogue or mentions names like Jon, Mark, Toran, or Abeer in a meeting context.
user_invocable: true
---

# Meeting Notes Processor

This skill processes meeting transcripts and creates structured entries in Notion:
1. A **Meeting Notes** page with comprehensive, topic-organized notes
2. **Action Items** (To-Do entries) with detailed context, linked to the meeting

## Input

Accept meeting content in any of these forms:
- Pasted transcript text in the conversation
- File path to a transcript file (.txt, .md, etc.)
- Raw meeting notes the user types out

## Workflow

### Step 1: Extract Meeting Metadata

From the transcript, identify:
- **Meeting name**: Look for headers, subject lines, or derive from main topic discussed
- **Date**: Parse from transcript timestamps, or use today's date
- **Category**: Match against available options based on content
- **Primary Project/Topic**: Identify the main project or topic (e.g., "Q2 Code", "Alloy", "CEP") - this will be used for action item categorization

Available categories for Meeting Notes:
- Alloy
- Project Ash
- CEP
- Q2 Stand Ups
- AppDirect
- Brightwell
- Q2 Genius
- 1 on 1s
- Product

### Step 2: Generate Comprehensive Meeting Notes

Create TWO things:

#### A. Brief Summary (for Summary property)
A 1-2 sentence overview of what the meeting covered. This goes in the "Summary" property field.

#### B. Detailed Notes (for page content)
Comprehensive, topic-organized notes that go in the page body. These should:

1. **Organize by topic/theme** - Group related discussion points under clear headers
2. **Use proper markdown structure**:
   - `# Heading` for major topics
   - `## Subheading` for subtopics
   - Bullet points for details
   - `---` dividers between major sections
   - Tables for timelines, comparisons, or structured data
   - `> Blockquotes` for important direct quotes from participants

3. **Include for each topic**:
   - Context and background
   - Key points discussed
   - Decisions made
   - Concerns or blockers raised
   - Relevant quotes that capture important nuances

4. **End with a Key Timelines section** if dates/milestones were discussed

Example structure:
```markdown
# Topic One

Context and what was discussed...

## Subtopic
- Detail point
- Another point

> "Important quote from participant" - Person

---

# Topic Two
...

---

# Key Timelines

| Milestone | Target Date |
|-----------|-------------|
| Item 1 | March 15 |
| Item 2 | April 1 |
```

### Step 3: Extract Action Items

Scan for action items indicated by:
- Explicit assignments ("Jon will...", "Mark to follow up on...")
- Commitments ("I'll handle that", "Let me take care of...")
- Due dates ("by Friday", "next week", "EOD")
- Task language ("need to", "should", "action item", "TODO")
- Targets/goals discussed ("we need 300 users by...", "target is March workshop")

For each action item, extract:
- **Task description**: Short, actionable phrase
- **Assigned To**: One of Jon, Mark, Toran, Abeer
- **Due Date**: Parse from context (relative dates like "next Monday", "by the workshop", "end of March")
- **Priority**: High/Medium/Low based on urgency language
- **Category**: Use the primary project/topic identified in Step 1

If assignee is unclear from context, ask the user before creating the entry.

### Step 4: Create Notion Entries

**Create Meeting Note** using notion-create-pages:
```
Parent: data_source_id "26456468-98e4-807f-930a-000be9118d14"
Properties:
  - "Meeting name": <extracted title>
  - "date:Date:start": <YYYY-MM-DD format>
  - "Category": <if applicable, as JSON array e.g. "[\"Product\"]">
  - "Summary": <brief 1-2 sentence summary>
```

**Then update page content** using notion-update-page with command "replace_content":
- Replace any `<Put Meeting Notes Here>` placeholder with the detailed notes
- If no placeholder exists, add the detailed notes as the page content

**Create Action Items** using notion-create-pages for each task:
```
Parent: data_source_id "26456468-98e4-81d4-8cba-000be705a952"
Properties:
  - "Tasks": <task description>
  - "Meeting Notes": <JSON array with meeting note URL>
  - "Assigned To": <Jon|Mark|Toran|Abeer>
  - "date:Created Date:start": <meeting date in YYYY-MM-DD>
  - "date:Created Date:is_datetime": 0
  - "date:Due Date:start": <YYYY-MM-DD if known>
  - "date:Due Date:is_datetime": 0
  - "Status": "To Do"
  - "Priority": <High|Medium|Low if determinable>
  - "Category": <JSON array with primary project, e.g. "[\"Q2 Code\"]">
```

**Then update each action item's page content** using notion-update-page with command "replace_content":

Each action item should have detailed page content including:
```markdown
# Context

Why this task matters and background from the meeting...

# Requirements

- Specific requirement 1
- Specific requirement 2
- What success looks like

# Why This Matters

Business context, dependencies, or urgency...

# From the Meeting

> "Direct quote from the transcript that prompted this action item"
```

### Step 5: Report Results

After creating entries, summarize what was created:
- Link to the meeting note
- Table of action items with assignees and due dates
- Note that all items have detailed context in their page bodies

## Example Interaction

**User**: /meeting-notes
Here's the transcript from our standup:

Jon: Alright, quick sync. Mark, where are we on the Alloy integration?
Mark: Almost done, should have the PR up by tomorrow.
Jon: Great. Toran, can you review it once it's ready?
Toran: Sure, I'll prioritize that.
Abeer: I still need the API docs from the vendor - Jon, can you follow up?
Jon: Yeah, I'll ping them today.

**Claude**:
I'll process this standup transcript.

[Creates meeting note with detailed topic-organized content]
[Creates action items with Category: Alloy, Created Date set, and detailed page content]

**Meeting**: Q2 Standup - [today's date]
**Category**: Alloy

**Action Items Created**:
| Task | Assignee | Due | Priority |
|------|----------|-----|----------|
| Submit Alloy integration PR | Mark | [tomorrow] | High |
| Review Alloy integration PR | Toran | - | High |
| Follow up with vendor for API docs | Jon | [today] | High |

Created meeting note: [link]
Created 3 action items with detailed context in To-Do list.

## Important Notes

- Always use the Notion MCP tools (notion-create-pages, notion-update-page, notion-fetch) for database operations
- The Meeting Notes and To-Do list databases are already linked via a relation field
- Date properties require the expanded format: `date:Date:start`, `date:Due Date:start`, `date:Created Date:start`
- Always set `date:Created Date:start` on action items to the meeting date
- Always set `Category` on action items to match the meeting's primary project/topic
- Always add detailed page content to action items explaining context, requirements, and including relevant quotes
- Summary property = brief overview; Page content = comprehensive detailed notes
- Look for `<Put Meeting Notes Here>` placeholder in the page template and replace it with detailed notes
- If the transcript is ambiguous about who should do something, ask rather than guess
