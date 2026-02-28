# Product Manager Prompts Plugin

A Claude Code plugin providing PM validation and prompting frameworks based on [Dean Peters' product-manager-prompts](https://github.com/deanpeters/product-manager-prompts).

## Purpose

Use this plugin to:
- **Validate** existing PM artifacts (user stories, positioning statements, personas)
- **Create** new PM documents using proven frameworks
- **Improve** PM thinking through structured templates

## Skills

| Skill | Triggers On | Use For |
|-------|-------------|---------|
| `jobs-to-be-done` | "JTBD", "customer jobs", "pains and gains", "Value Proposition Canvas" | Understanding customer needs and motivations |
| `user-stories` | "user story", "acceptance criteria", "Given/When/Then", "story splitting" | Creating and validating development requirements |
| `problem-positioning` | "problem statement", "positioning statement", "value proposition", "Geoffrey Moore" | Articulating problems and competitive positioning |
| `customer-journey` | "customer journey", "buyer journey", "touchpoints", "happy path" | Mapping the full customer experience |
| `market-analysis` | "PESTEL", "TAM SAM SOM", "market sizing", "MRD" | Strategic market analysis and sizing |
| `working-backwards` | "press release", "FAQ", "Amazon Working Backwards" | Vision documents before building |
| `proto-persona` | "proto-persona", "user persona", "buyer persona" | Creating initial persona hypotheses |
| `recommendation-canvas` | "AI recommendation", "solution hypothesis", "value justification" | Evaluating and presenting AI solutions |

## Quick Start

### Validate Existing Work
```
"Review this user story and check if it follows best practices"
"Validate my positioning statement"
"Is this JTBD analysis complete?"
```

### Create New Documents
```
"Help me create a Jobs-to-be-Done analysis for our target customer"
"Generate a positioning statement for our product"
"Create a customer journey map for our buyer persona"
```

### Get Guidance
```
"What questions should I ask to validate this proto-persona?"
"How do I split this user story?"
"What's missing from this problem statement?"
```

## Framework Summary

### Jobs-to-be-Done (Osterwalder/Value Proposition Canvas)
- Functional, Social, Emotional Jobs
- Pains: Challenges, Costs, Mistakes, Unresolved Problems
- Gains: Expectations, Savings, Adoption Factors, Life Improvements

### User Stories (Mike Cohn + Gherkin)
- As a [persona], I want [action], so that [outcome]
- Given/When/Then acceptance criteria
- Story splitting decision tree

### Problem Framing
- I am / Trying to / But / Because / Which makes me feel
- Context & Constraints
- Final Problem Statement

### Positioning (Geoffrey Moore)
- For [target] that need [need], [product] is a [category] that [benefit]
- Unlike [competitor], [product] provides [differentiation]

### Customer Journey
- Awareness → Consideration → Decision → Service → Loyalty
- Happy Path / Fail Path / Difficult Path emotional mapping

### Market Analysis
- PESTEL: Political, Economic, Social, Technological, Environmental, Legal
- TAM/SAM/SOM market sizing with data sources

### Working Backwards (Amazon)
- Visionary Press Release
- Futuristic FAQ for all stakeholders

### Proto-Persona Canvas
- Bio, Quotes, Pains, Goals, Attitudes & Influences
- Validation priorities and interview questions

### AI Recommendation Canvas
- Problem + Hypothesis + Positioning + Risks + Justification + Metrics

## Attribution

Based on [product-manager-prompts](https://github.com/deanpeters/product-manager-prompts) by Dean Peters. Frameworks inspired by:
- Osterwalder's Value Proposition Canvas
- Mike Cohn's User Story format
- Geoffrey Moore's "Crossing the Chasm"
- Amazon's Working Backwards methodology
- Francis Joseph Aguilar's PEST analysis
- Jeff Patton's Story Mapping
- Productside PM courses

Licensed under MIT License.
