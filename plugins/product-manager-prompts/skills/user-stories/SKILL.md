---
name: user-stories
description: Use when the user asks about user stories, acceptance criteria, Gherkin format, Given/When/Then, story splitting, story mapping, backlog refinement, epic hypothesis, Mike Cohn format, or writing requirements for development teams. Helps create and validate well-structured user stories.
version: 1.0.0
---

# User Stories Skill

Helps product managers create and validate user stories using Mike Cohn's format with Gherkin-style acceptance criteria. Includes story splitting logic and story mapping frameworks.

## When to Use

- Writing new user stories for development
- Refining backlog items
- Splitting large stories into smaller ones
- Validating existing user stories
- Creating story maps for releases

## Prerequisites

Before creating user stories, ensure you have:
1. **Product Overview**: Description of the product/feature
2. **Target User Persona**: Who the user is, their goals and pain points
3. **Product Goals**: Objectives the feature aims to achieve
4. **Competitive Landscape**: How the product differentiates

## User Story Format Template

```markdown
### User Story [ID]:

- **Summary**: [Brief, memorable title describing value to persona]

#### Use Case:
- **As a** [user persona or role],
- **I want to** [action user takes],
- **so that** [desired outcome].

#### Acceptance Criteria:
- **Scenario**: [Human-readable scenario description]
- **Given**: [Initial context or precondition]
- **and Given**: [Additional context based on user's state]
- **and Given**: [UI-focused preconditions for the When event]
- **and Given**: [Outcome-focused preconditions for the Then result]
- **When**: [Event that triggers the action - connects to "I want to"]
- **Then**: [Expected outcome - connects to "so that"]
```

## Story Splitting Logic

When a story is too large, apply this decision tree in order:

1. **Multiple workflow steps?** → Split along workflow steps
2. **Business rule variations?** → Split along business rules
3. **Data variations?** → Split along data types
4. **Complex acceptance criteria?** → Split along discrete When/Then pairs
5. **Major build effort?** → Split along effort milestones
6. **External dependencies?** → Split along dependencies
7. **Significant DevOps effort?** → Split along DevOps steps
8. **None apply?** → Use Tiny Acts of Discovery to refine

### Splitting Indicators

Watch for these signs a story needs splitting:
- Multiple "When" statements
- Multiple "Then" statements
- Estimate > 8 story points
- Can't demo in one sprint
- Requires multiple teams

## Epic Hypothesis Template

For larger initiatives, frame as a hypothesis:

```markdown
### If/Then Hypothesis

**If we** [action or solution]
**for** [target persona]
**Then we will** [achieve desirable outcome].

### Tiny Acts of Discovery

**We will test our assumption by:**
- [Experiment 1]
- [Experiment 2]

### Validation Measures

**We know our hypothesis is valid if within** [timeframe]
**we observe:**
- [Quantitative outcome]
- [Qualitative outcome]
```

## Story Mapping Template

For release planning using Jeff Patton's approach:

```markdown
### Who
**Segment**: [Target segment]
**Persona**: [Persona description and characteristics]

### Backbone
**Narrative**: [Primary goal framed by jobs-to-be-done]

**Activities** (3-5 key activities):
1. [Activity 1]
2. [Activity 2]
3. [Activity 3]

**Steps** (3-5 per activity):
For [Activity 1]:
- Step 1: [Description]
- Step 2: [Description]

**Tasks** (5-7 per step):
For [Activity 1, Step 1]:
- Task 1: [Description]
- Task 2: [Description]
```

## Validation Checklist

When reviewing user stories, verify:

- [ ] **Single When/Then**: Only one action and outcome per story
- [ ] **User Perspective**: Written from user's point of view
- [ ] **Valuable**: Delivers value the user cares about
- [ ] **Estimable**: Team can estimate the effort
- [ ] **Small**: Can complete in one sprint
- [ ] **Testable**: Clear acceptance criteria
- [ ] **Independent**: Can be delivered without other stories

## Common Anti-Patterns

Avoid these mistakes:
- **Technical Stories**: "As a developer, I want to refactor..." (Not user value)
- **Vague Outcomes**: "so that I have a better experience" (Not measurable)
- **Solution Dictation**: "I want a dropdown menu" (Prescribes implementation)
- **Multiple Outcomes**: "so that I can X and Y and Z" (Needs splitting)

## Attribution

Based on templates by Dean Peters, inspired by Mike Cohn's User Story format and Gherkin acceptance criteria. Story splitting logic from Richard Lawrence and Peter Green's "Humanizing Work Guide to Splitting User Stories". Licensed under MIT License.
