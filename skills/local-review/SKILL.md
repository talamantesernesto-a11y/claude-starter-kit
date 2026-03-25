---
name: local-review
description: Run a local code review on the current branch's diff before committing or creating a PR. Use when the user says "review my code", "check my changes", "review before commit", "code review", or when finishing a feature branch. Also trigger proactively before any git push or PR creation to catch issues early. Especially useful for solo developers who don't have a team to review their code.
---

# Local Code Review

Run a thorough code review on the current branch's diff, catching issues before they reach production.

## When to Use

- Before committing significant changes
- Before creating a pull request
- When the user asks for a code review
- After completing a feature or bug fix

## Review Process

### Step 1: Gather the Diff

```bash
# Get the diff against the base branch
git diff $(git merge-base HEAD main)...HEAD

# Also check unstaged changes
git diff

# And untracked files
git status
```

### Step 2: Run Parallel Review Passes

Perform these 4 review passes on the diff:

#### Pass 1: Bug Detection
Look for:
- Logic errors, off-by-one errors, race conditions
- Null/undefined handling gaps
- Missing error handling or swallowed errors
- Incorrect async/await usage
- Resource leaks (unclosed connections, missing cleanup)
- Hardcoded values that should be configurable

#### Pass 2: Security Review
Look for:
- Hardcoded secrets, API keys, tokens
- SQL injection, XSS, CSRF vulnerabilities
- Missing input validation
- Insecure authentication/authorization
- Sensitive data in logs or error messages
- Missing rate limiting on new endpoints

#### Pass 3: Code Quality
Look for:
- Functions doing too many things (>30 lines is a yellow flag)
- Duplicated logic that should be extracted
- Missing TypeScript types or `any` usage
- Inconsistent naming conventions
- Dead code or commented-out code
- Missing or misleading comments on complex logic

#### Pass 4: Architecture & Patterns
Look for:
- Consistency with existing codebase patterns
- Proper separation of concerns
- Appropriate abstraction level (not over/under-engineered)
- Missing tests for new functionality
- Breaking changes to public APIs
- Performance concerns (N+1 queries, unnecessary re-renders, large bundles)

### Step 3: Score and Report

For each finding, assign a confidence score (0-100). Only report findings with confidence >= 80.

#### Severity Levels
- **Critical** — Must fix before merging (bugs, security issues)
- **Warning** — Should fix, but won't break things
- **Suggestion** — Nice to have, improves code quality
- **Praise** — Something done well (include 1-2 per review for morale)

### Step 4: Present Findings

Format as:

```
## Code Review Summary

**Files changed:** X
**Lines added/removed:** +Y / -Z

### Critical Issues (X)
- [file:line] Description of issue and suggested fix

### Warnings (X)
- [file:line] Description and recommendation

### Suggestions (X)
- [file:line] Improvement opportunity

### What's Good
- Highlight 1-2 things done well
```

### Step 5: Auto-Fix Critical & Warning

Despues de presentar el reporte, corregir automaticamente sin preguntar:

1. **Critical** — Corregir inmediatamente todos. Sin consultar.
2. **Warning** — Corregir inmediatamente todos. Sin consultar.
3. **Suggestions** — Presentar al usuario y preguntar cuales quiere aplicar. Estos son opcionales.

Despues de cada ronda de fixes, re-correr el review solo sobre los archivos modificados para verificar que no se introdujeron nuevos issues.

Si un fix es ambiguo (multiples formas validas de resolverlo), elegir la mas conservadora — la que cambie menos codigo y mantenga el comportamiento existente.

## Key Principles

- **Be specific** — Point to exact lines, don't be vague
- **Explain why** — Don't just say "bad", explain the consequence
- **Suggest fixes** — Don't just identify problems, propose solutions
- **Stay relevant** — Only review changed code, not the entire codebase
- **Be constructive** — Include praise, not just criticism
- **Confidence threshold** — Only flag issues you're 80%+ sure about
