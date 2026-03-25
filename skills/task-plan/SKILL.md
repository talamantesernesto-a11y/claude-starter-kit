---
name: task-plan
description: >
  File-based task management system using tasks/todo.md and tasks/lessons.md.
  This skill should be used when starting any non-trivial implementation task,
  when the user says "plan this", "let's plan", "track this", "create a task plan",
  or when beginning a feature, refactor, or multi-step bug fix. Also trigger
  when resuming work on an existing project that has a tasks/ directory.
  DO NOT TRIGGER for single-file edits, quick questions, or tasks completable
  in fewer than 3 steps.
---

# Task Plan — File-Based Task Management

Manage implementation work through `tasks/todo.md` and `tasks/lessons.md` files that persist across sessions and provide clear progress tracking.

## When to Use

- Starting any non-trivial implementation (3+ steps)
- Resuming work on a project with existing `tasks/` directory
- When the user asks to plan, track, or organize work
- Before any architectural change or multi-file refactor

## The Workflow

### Phase 1: Plan First

Create or update `tasks/todo.md` with checkable items:

```markdown
# Task: [Title]

## Objective
[1-2 sentence description of what we're building/fixing and WHY]

## Plan
- [ ] Step 1: [Specific, actionable item]
- [ ] Step 2: [Specific, actionable item]
- [ ] Step 3: [Specific, actionable item]

## Dependencies
- [List any blockers or prerequisites]

## Risks
- [What could go wrong]
```

Rules for writing plan items:
- Each item must be independently verifiable
- Each item should take no more than one focused work block
- Order items by dependency (prerequisites first)
- Include verification steps as their own items (e.g., "Run tests for auth module")

### Phase 2: Verify Plan

Before starting implementation, present the plan to the user:
- Show the `tasks/todo.md` contents
- Confirm scope and ordering
- Adjust based on feedback
- Do NOT start coding until plan is approved

### Phase 3: Track Progress

As work progresses:
- Mark items complete (`[x]`) immediately after finishing each one
- Add notes inline if something changed from the plan
- If a step reveals new work, add new items to the plan rather than doing unplanned work

```markdown
- [x] Step 1: Set up database schema
- [x] Step 2: Create API endpoints (added pagination, wasn't in original plan)
- [ ] Step 2b: Add rate limiting (discovered during step 2)
- [ ] Step 3: Write integration tests
```

### Phase 4: Explain Changes

At each major milestone (not every line change):
- Provide a 1-2 sentence summary of what was done and why
- Flag anything that deviated from the plan
- Note any decisions made during implementation

### Phase 5: Document Results

When all items are complete, add a review section to `tasks/todo.md`:

```markdown
## Review
- **Status**: Complete / Partial / Blocked
- **Changes from plan**: [What changed and why]
- **Test results**: [Summary of test outcomes]
- **Notes for future work**: [Anything left undone or to revisit]
```

### Phase 6: Capture Lessons

If the user corrected the approach during implementation, update `tasks/lessons.md` (see the `self-correct` skill for the full lesson-capture workflow).

## File Structure

```
tasks/
├── todo.md       # Current task plan with checkable items
└── lessons.md    # Accumulated lessons from corrections
```

## Re-Planning Protocol

If something goes sideways during implementation:

1. STOP immediately — do not keep pushing a broken approach
2. Update `tasks/todo.md` with what went wrong
3. Cross out or remove the broken steps
4. Write new steps based on current understanding
5. Get user approval before resuming

Mark re-plans clearly:

```markdown
## Plan (Revised — original approach failed at step 3)
- [x] Step 1: ...
- [x] Step 2: ...
- [ ] ~~Step 3: Original approach~~ Failed because [reason]
- [ ] Step 3: New approach based on [what we learned]
- [ ] Step 4: ...
```
