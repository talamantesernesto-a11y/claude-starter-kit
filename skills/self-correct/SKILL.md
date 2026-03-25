---
name: self-correct
description: >
  Real-time self-improvement loop that captures user corrections into tasks/lessons.md
  and prevents repeated mistakes. This skill should be used AUTOMATICALLY whenever the
  user corrects an approach, says "no not that", "that's wrong", "don't do it that way",
  "I told you before", or provides any guidance that changes the current approach.
  Also trigger at session start to review existing lessons for the current project.
  Different from continuous-learning (session-end extraction) — this captures corrections
  in real-time as they happen.
---

# Self-Correct — Real-Time Improvement Loop

Capture every user correction as a reusable lesson in `tasks/lessons.md` so the same mistake never happens twice.

## When to Activate

- **AUTOMATICALLY** after ANY correction from the user
- At session start — review existing `tasks/lessons.md` for the current project
- When the user says "remember this", "don't do that again", "I already told you"
- When an approach fails and a new one succeeds

## The Correction Capture Loop

### Step 1: Detect the Correction

Recognize when the user is correcting behavior:
- Direct correction: "No, don't use X, use Y instead"
- Implicit correction: User undoes or changes something just done
- Approach rejection: "That's too complex", "This is hacky"
- Repeated instruction: User has to explain the same thing again

### Step 2: Extract the Pattern

For each correction, identify:
- **What was done wrong** (the mistake)
- **What should be done instead** (the fix)
- **Why** (the reasoning, if given — this is the most valuable part)
- **When this applies** (scope: always, this project, this language, etc.)

### Step 3: Write to lessons.md

Append to `tasks/lessons.md` using this format:

```markdown
### [Date] — [Short title]

**Mistake**: [What was done wrong]
**Correction**: [What to do instead]
**Why**: [Reasoning from the user]
**Scope**: [always | project-specific | language-specific]

---
```

Example:

```markdown
### 2026-03-14 — Don't mock the database

**Mistake**: Used mock database in integration tests
**Correction**: Always use a real database connection for integration tests
**Why**: Mock/prod divergence caused a broken migration to pass tests last quarter
**Scope**: always

---
```

### Step 4: Write a Prevention Rule

After capturing the lesson, internalize it as a behavioral rule for the current session:
- State the rule clearly in the response
- Apply it immediately to any in-progress work
- Reference it if the same situation arises again

### Step 5: Acknowledge Briefly

Confirm the correction without being verbose:
- "Got it — [brief restatement of correction]. Captured in lessons.md."
- Do NOT over-apologize or write paragraphs about the mistake

## Session Start Protocol

At the beginning of each session:

1. Check if `tasks/lessons.md` exists for the current project
2. If it exists, read it silently
3. Apply all lessons to the current session's behavior
4. Do NOT list the lessons to the user unless asked

## Lesson Maintenance

Over time, lessons accumulate. Periodically:
- Remove lessons that have been incorporated into project rules or CLAUDE.md
- Merge duplicate lessons
- Promote frequently-triggered lessons to project-level rules
- Mark lessons as "resolved" if the underlying issue was fixed structurally

## File Location

```
tasks/
└── lessons.md    # Accumulated lessons from user corrections
```

If `tasks/` does not exist, create it when the first correction is captured.
