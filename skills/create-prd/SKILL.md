---
name: create-prd
description: >
  Write comprehensive Product Requirements Documents (PRDs) that align engineering,
  design, and business. Use this skill whenever the user needs a PRD, product spec,
  feature spec, requirements document, technical requirements, functional specification,
  or any document that defines what to build and why. Also trigger when the user says
  "write a PRD", "product requirements", "feature spec", "I need a spec", "spec this
  out", "define requirements", "what should we build", "document this feature",
  "write requirements", "product spec", "feature brief", "escríbeme un PRD",
  "especificación de producto", or when they describe a feature they want to build and
  need it formalized into a structured document before implementation. If the user
  is transitioning from "idea" to "build-ready specification", this skill applies.
  Pairs well with brainstorming (for ideation before the PRD) and tdd (for
  implementation after the PRD).
---

# Create PRD

Write PRDs that engineers actually read. A good PRD eliminates ambiguity, aligns stakeholders, and prevents scope creep. A bad PRD is either too vague to be useful or too bloated to be read.

---

## The PRD Philosophy

- **Clarity over completeness** — a 2-page PRD that everyone reads beats a 20-page PRD that nobody does
- **Why before what** — always lead with the problem, not the solution
- **Decisions, not descriptions** — the PRD's job is to record decisions that prevent back-and-forth during implementation
- **Living document** — the PRD should be updated as decisions change, not treated as a stone tablet

---

## PRD Template

### 1. Title and Metadata

```
# [Feature/Product Name]

Author:       [Name]
Status:       [Draft / In Review / Approved / In Progress / Shipped]
Created:      [Date]
Last Updated: [Date]
Target Ship:  [Date or Sprint]
```

### 2. Problem Statement (The "Why")

**This is the most important section.** If the problem isn't clear, the rest of the PRD is pointless.

Answer these questions:
- What problem are we solving?
- Who has this problem? (Be specific — name the persona)
- How painful is this problem? (Frequency × Intensity)
- What's the evidence this problem exists? (Data, research, user quotes, support tickets)
- What happens if we DON'T solve it?

**Format:**
> **Problem:** [One sentence describing the core problem]
>
> **Who:** [Specific user persona]
>
> **Evidence:** [Data, quotes, or observations that prove this is real]
>
> **Impact of inaction:** [What happens if we do nothing]

### 3. Goals and Success Metrics

Define what "done" looks like with measurable outcomes.

| Goal | Metric | Target | Measurement Method |
|------|--------|--------|--------------------|
| Primary goal | [Metric] | [Number] | [How you'll measure] |
| Secondary goal | [Metric] | [Number] | [How you'll measure] |

**Anti-pattern:** "Improve user experience" is not a goal. "Reduce waiver completion time from 8 minutes to under 3 minutes" is.

### 4. User Stories and Scenarios

Write stories in standard format with acceptance criteria:

```
As a [persona],
I want to [action],
So that [outcome/benefit].

Acceptance Criteria:
- Given [context], when [action], then [expected result]
- Given [context], when [action], then [expected result]
```

Include:
- **Happy path** — the main use case working perfectly
- **Edge cases** — unusual but possible scenarios
- **Error cases** — what happens when things go wrong
- **Permission boundaries** — who can and can't do what

### 5. Scope Definition

This section prevents scope creep. Be explicit about boundaries.

**In Scope:**
- [ ] [Feature/capability 1]
- [ ] [Feature/capability 2]
- [ ] [Feature/capability 3]

**Out of Scope (and why):**
- [ ] [Thing we're NOT building] — [Reason: future phase / not enough data / low impact]
- [ ] [Thing we're NOT building] — [Reason]

**Future Considerations (not now, but keep in mind):**
- [Thing that might matter later]

### 6. Proposed Solution

Describe the solution at the right altitude — enough detail to build, not so much that you're writing code.

**User Flow:**
1. User does X
2. System responds with Y
3. User sees Z

**Key Screens / States:**
- Describe each major view or state
- Include wireframes or mockups if available (reference file paths)
- Call out interactive behaviors and transitions

**Data Model Changes:**
- New tables/columns needed
- Relationships
- Migration considerations

**API Changes:**
- New endpoints
- Modified endpoints
- Breaking changes (if any)

### 7. Technical Considerations

Don't design the architecture — that's engineering's job. But DO flag:

- **Dependencies**: What must exist before this can be built?
- **Integrations**: External services, APIs, or systems involved
- **Performance**: Expected load, response time requirements
- **Security**: Auth requirements, data sensitivity, access control
- **Migration**: Data migration needs, backward compatibility
- **Infrastructure**: New services, queues, storage needed

### 8. Design Requirements

- **Responsive**: Which breakpoints matter?
- **Accessibility**: WCAG level, screen reader support
- **Internationalization**: Languages, RTL, locale-specific formatting
- **Brand**: Design system constraints, component library
- **States**: Loading, empty, error, success, partial data

### 9. Release Strategy

| Phase | What Ships | Target Date | Success Criteria |
|-------|-----------|-------------|-----------------|
| MVP / Phase 1 | [Minimum viable scope] | [Date] | [Metric] |
| Phase 2 | [Expanded scope] | [Date] | [Metric] |
| Full Release | [Complete vision] | [Date] | [Metric] |

- **Feature flag**: Yes / No — behind a flag for gradual rollout?
- **Beta / early access**: Who gets it first?
- **Rollback plan**: What happens if it breaks?

### 10. Open Questions

List unresolved decisions that block or affect implementation. For each:

| Question | Owner | Deadline | Decision |
|----------|-------|----------|----------|
| [Question] | [Who decides] | [By when] | [TBD / Decided: X] |

### 11. Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| [Risk description] | High/Med/Low | High/Med/Low | [What we'll do] |

---

## PRD Quick Mode

For smaller features that don't need a full PRD, use the condensed format:

```
## [Feature Name]

**Problem:** [One sentence]
**Solution:** [One paragraph]
**Scope:** [Bullet list of what's in and out]
**Success metric:** [One measurable outcome]
**Stories:**
- As a [user], I want [X] so that [Y]
  - AC: [Acceptance criteria]
**Open questions:** [List]
**Target:** [Date/Sprint]
```

---

## PRD Review Checklist

Before marking a PRD as "ready":

- [ ] Could someone build this without asking me questions? (Clarity test)
- [ ] Does every feature trace back to the problem statement? (Alignment test)
- [ ] Are the success metrics measurable and time-bound? (Accountability test)
- [ ] Is the scope explicitly bounded — both in and out? (Scope test)
- [ ] Are edge cases and error states covered? (Robustness test)
- [ ] Are open questions listed with owners and deadlines? (Completeness test)
- [ ] Is there a rollback plan? (Safety test)
- [ ] Did I write this for the reader, not for myself? (Empathy test)

---

## Tone

- Clear and direct — no corporate jargon
- Opinionated — make decisions, don't list options without recommending one
- Concise — respect the reader's time
- Honest about unknowns — mark them as open questions, don't hide them
