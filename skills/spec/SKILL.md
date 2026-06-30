---
name: spec
description: Turn prompts into structured specs with requirements, design, and verifiable tasks — then implement task by task.
---

# Spec-Driven Development

Turn a prompt or feature request into a structured, verifiable spec with requirements, design, and sequenced tasks. This mirrors Kiro's spec workflow but writes plain Markdown files in your repo — no platform lock-in.

## Process

### 1. Understand the ask
If the user's request is vague, ask 1-3 clarifying questions before proceeding. Don't guess scope, don't assume constraints. If the user wants you to run autonomously, state your assumptions explicitly in the spec and flag them with `⚠️ Assumption:`.

### 2. Write `spec/<feature>/requirements.md`

```markdown
# Requirements: <feature name>

## Problem
<One sentence: what problem does this solve? For whom?>

## User stories
- As a <role>, I want <capability> so that <benefit>.
- ...

## Functional requirements
### FR1: <title>
- **Given** <precondition>
- **When** <action>
- **Then** <expected result>

### FR2: ...

## Non-functional requirements
- Performance: ...
- Security: ...
- Compatibility: ...

## Edge cases
- What happens when <boundary condition>?
- ...

## Out of scope
- Explicitly NOT doing: ...
```

### 3. Write `spec/<feature>/design.md`

```markdown
# Design: <feature name>

## Architecture
<How this fits into the existing codebase. Diagram in ASCII if helpful.>

## Key decisions
| Decision | Rationale | Alternatives considered |
|----------|-----------|------------------------|
| ... | ... | ... |

## Data model / API
<New types, functions, endpoints, schema changes.>

## Dependencies
<New crates, libraries, services needed.>

## Risks
| Risk | Likelihood | Mitigation |
|------|-----------|------------|
| ... | Low/Med/High | ... |
```

### 4. Write `spec/<feature>/tasks.md`

```markdown
# Tasks: <feature name>

## 1. <task name>
- [ ] <concrete step>
- [ ] <concrete step>
**Verify:** <how to confirm this task is done>

## 2. <task name>
- [ ] <concrete step>
**Verify:** <how to confirm>

...
```

Each task must be:
- **Small enough** to implement in one focused session
- **Verifiable** — a concrete check (test passes, command succeeds, output matches)
- **Ordered** — dependencies flow downward; no circular dependencies

### 5. Review with user
Present the spec as a summary. Highlight:
- The task count and estimated scope
- Any assumptions you made
- The verification gate for each task

Let the user approve, edit, or reject before implementing.

### 6. Implement task by task
When the user says go, work through tasks.md sequentially:
1. Pick the first unchecked task
2. Implement it
3. Run its verification gate
4. Check the box in tasks.md
5. Repeat until all tasks are checked

Stop and surface issues if a verification gate fails.

## Guardrails
- Spec files go in `spec/<slug>/` — don't pollute the repo root
- If `spec/` doesn't exist, create it
- Add `spec/` to `.gitignore` only if the user asks — specs ARE meant to be committed
- Don't over-spec: for a 1-hour feature, stop at 3-5 tasks. For a week-long feature, 10-15 tasks
- If the user rejects the spec, revise based on feedback, don't abandon the approach
