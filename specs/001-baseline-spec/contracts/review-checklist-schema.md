# Review Checklist Schema: Validation Contract

**Purpose**: Define the three-phase review process and checklist requirements

---

## Review Process Overview

Each chapter must pass three sequential reviews before approval:

```
Chapter Draft
     │
     ▼
┌────────────────────┐
│  Technical Review  │ ← SME validates accuracy
│  (2-3 days)        │
└────────────────────┘
     │ PASS
     ▼
┌────────────────────┐
│  Editorial Review  │ ← Editor validates readability
│  (1-2 days)        │
└────────────────────┘
     │ PASS
     ▼
┌────────────────────┐
│   Quality Gate     │ ← PM validates metrics
│   (1 day)          │
└────────────────────┘
     │ PASS
     ▼
   APPROVED
```

---

## Phase 1: Technical Review Checklist

**Reviewer**: Subject Matter Expert (different from author)
**Focus**: Accuracy, completeness, currency
**Duration**: 2-3 days

```markdown
# Technical Review: Chapter [N] - [Title]

**Reviewer**: [Name]
**Date**: [Date]
**Author**: [Author Name]

## Technical Accuracy

| # | Item | Status | Notes |
|---|------|--------|-------|
| 1 | All facts verified against authoritative sources | ☐ Pass ☐ Fail | |
| 2 | No technical errors or inaccuracies | ☐ Pass ☐ Fail | |
| 3 | Technology versions are current (within 2 major versions) | ☐ Pass ☐ Fail | |
| 4 | Commands and code tested and functional | ☐ Pass ☐ Fail | |
| 5 | Standards correctly cited (RFC, ISO, etc.) | ☐ Pass ☐ Fail | |
| 6 | Industry terminology used correctly | ☐ Pass ☐ Fail | |

## Completeness

| # | Item | Status | Notes |
|---|------|--------|-------|
| 7 | All topics from domain covered | ☐ Pass ☐ Fail | |
| 8 | No critical subtopics missing | ☐ Pass ☐ Fail | |
| 9 | Difficulty progression complete (B→I→A→E) | ☐ Pass ☐ Fail | |
| 10 | Practical examples demonstrate concepts | ☐ Pass ☐ Fail | |
| 11 | Labs are complete and testable | ☐ Pass ☐ Fail | |

## MCQ Quality

| # | Item | Status | Notes |
|---|------|--------|-------|
| 12 | Questions test relevant concepts | ☐ Pass ☐ Fail | |
| 13 | Correct answers are verified accurate | ☐ Pass ☐ Fail | |
| 14 | Explanations are technically sound | ☐ Pass ☐ Fail | |
| 15 | Distractors are plausible but incorrect | ☐ Pass ☐ Fail | |
| 16 | Difficulty ratings are appropriate | ☐ Pass ☐ Fail | |

## Citations

| # | Item | Status | Notes |
|---|------|--------|-------|
| 17 | Minimum 2 sources per major claim (FR-011) | ☐ Pass ☐ Fail | |
| 18 | All citations are to authoritative sources | ☐ Pass ☐ Fail | |
| 19 | Citation format follows FR-013 | ☐ Pass ☐ Fail | |
| 20 | URLs are valid and accessible | ☐ Pass ☐ Fail | |

## Issues Found

| # | Section/MCQ | Issue | Severity | Suggested Fix |
|---|-------------|-------|----------|---------------|
| 1 | | | ☐ Critical ☐ Major ☐ Minor | |
| 2 | | | ☐ Critical ☐ Major ☐ Minor | |
| 3 | | | ☐ Critical ☐ Major ☐ Minor | |

## Overall Result

- [ ] **PASS** - Ready for Editorial Review
- [ ] **FAIL** - Return to Author for Revision

**Critical Issues**: [Count]
**Major Issues**: [Count]
**Minor Issues**: [Count]

**Comments**:
[General feedback for author]

---
**Reviewer Signature**: _____________________
**Date**: _____________________
```

---

## Phase 2: Editorial Review Checklist

**Reviewer**: Editorial Team Member
**Focus**: Readability, formatting, consistency
**Duration**: 1-2 days

```markdown
# Editorial Review: Chapter [N] - [Title]

**Reviewer**: [Name]
**Date**: [Date]
**Author**: [Author Name]

## Readability

| # | Item | Status | Notes |
|---|------|--------|-------|
| 1 | Flesch Reading Ease score 50-60 | ☐ Pass ☐ Fail | Score: ___ |
| 2 | Average sentence length 15-20 words | ☐ Pass ☐ Fail | |
| 3 | Paragraphs 3-5 sentences | ☐ Pass ☐ Fail | |
| 4 | Technical jargon explained on first use | ☐ Pass ☐ Fail | |
| 5 | Clear, professional language throughout | ☐ Pass ☐ Fail | |

## Formatting Consistency

| # | Item | Status | Notes |
|---|------|--------|-------|
| 6 | Heading hierarchy consistent (H1→H2→H3→H4) | ☐ Pass ☐ Fail | |
| 7 | Section numbering correct | ☐ Pass ☐ Fail | |
| 8 | Figure numbering follows convention | ☐ Pass ☐ Fail | |
| 9 | Table formatting consistent | ☐ Pass ☐ Fail | |
| 10 | Code blocks properly formatted | ☐ Pass ☐ Fail | |
| 11 | Bullet/numbered list formatting consistent | ☐ Pass ☐ Fail | |

## Structure Compliance

| # | Item | Status | Notes |
|---|------|--------|-------|
| 12 | All 11 required sections present | ☐ Pass ☐ Fail | |
| 13 | Sections in correct order | ☐ Pass ☐ Fail | |
| 14 | Learning objectives use Bloom's verbs | ☐ Pass ☐ Fail | |
| 15 | Key Takeaways = exactly 5 | ☐ Pass ☐ Fail | |
| 16 | MCQ format matches schema | ☐ Pass ☐ Fail | |

## Visual Elements

| # | Item | Status | Notes |
|---|------|--------|-------|
| 17 | Diagrams have descriptive titles | ☐ Pass ☐ Fail | |
| 18 | Legends present where needed | ☐ Pass ☐ Fail | |
| 19 | Text in diagrams readable | ☐ Pass ☐ Fail | |
| 20 | Tables have captions | ☐ Pass ☐ Fail | |

## Grammar and Style

| # | Item | Status | Notes |
|---|------|--------|-------|
| 21 | No spelling errors | ☐ Pass ☐ Fail | |
| 22 | No grammar errors | ☐ Pass ☐ Fail | |
| 23 | Consistent terminology | ☐ Pass ☐ Fail | |
| 24 | Active voice preferred | ☐ Pass ☐ Fail | |

## Issues Found

| # | Location | Issue | Category | Suggested Fix |
|---|----------|-------|----------|---------------|
| 1 | | | ☐ Format ☐ Grammar ☐ Style | |
| 2 | | | ☐ Format ☐ Grammar ☐ Style | |
| 3 | | | ☐ Format ☐ Grammar ☐ Style | |

## Overall Result

- [ ] **PASS** - Ready for Quality Gate
- [ ] **FAIL** - Return to Author for Revision

**Readability Score**: [Score]
**Format Issues**: [Count]
**Grammar Issues**: [Count]

**Comments**:
[General feedback for author]

---
**Reviewer Signature**: _____________________
**Date**: _____________________
```

---

## Phase 3: Quality Gate Checklist

**Reviewer**: Project Manager / Quality Lead
**Focus**: Metrics compliance, final verification
**Duration**: 1 day

```markdown
# Quality Gate: Chapter [N] - [Title]

**Reviewer**: [Name]
**Date**: [Date]
**Author**: [Author Name]

## Prerequisite Reviews

| Review | Status | Reviewer | Date |
|--------|--------|----------|------|
| Technical Review | ☐ Pass ☐ Pending | | |
| Editorial Review | ☐ Pass ☐ Pending | | |

**Note**: Quality Gate CANNOT proceed unless both reviews show PASS.

## Content Metrics

| Metric | Target | Actual | % | Status |
|--------|--------|--------|---|--------|
| Page Count | [Target] | | | ☐ Pass (≥95%) ☐ Fail |
| MCQ Count | [Target] | | | ☐ Pass (100%) ☐ Fail |
| Diagram Count | [Target] | | | ☐ Pass (≥90%) ☐ Fail |
| Lab Count | [Target] | | | ☐ Pass (100%) ☐ Fail |
| Example Count | 10 | | | ☐ Pass (≥10) ☐ Fail |

## MCQ Difficulty Distribution

| Level | Target % | Actual Count | Actual % | Status |
|-------|----------|--------------|----------|--------|
| Beginner | 25% | | | ☐ Pass (20-30%) ☐ Fail |
| Intermediate | 35% | | | ☐ Pass (30-40%) ☐ Fail |
| Advanced | 30% | | | ☐ Pass (25-35%) ☐ Fail |
| Expert | 10% | | | ☐ Pass (5-15%) ☐ Fail |

## Quality Scores

| Metric | Target | Actual | Status |
|--------|--------|--------|--------|
| Flesch Reading Ease | 50-60 | | ☐ Pass ☐ Fail |
| Technical Review | PASS | | ☐ Pass ☐ Fail |
| Editorial Review | PASS | | ☐ Pass ☐ Fail |

## Final Checks

| # | Item | Status |
|---|------|--------|
| 1 | No placeholder content remaining | ☐ Pass ☐ Fail |
| 2 | All TODO markers resolved | ☐ Pass ☐ Fail |
| 3 | All cross-references valid | ☐ Pass ☐ Fail |
| 4 | Chapter integrates with book structure | ☐ Pass ☐ Fail |
| 5 | Assets (diagrams, code) in correct locations | ☐ Pass ☐ Fail |

## Gate Decision

### Pass Criteria
All of the following must be true:
- [ ] Technical Review = PASS
- [ ] Editorial Review = PASS
- [ ] Page Count ≥ 95% of target
- [ ] MCQ Count = 100% of target
- [ ] Diagram Count ≥ 90% of target
- [ ] Lab Count = 100% of target
- [ ] Example Count ≥ 10
- [ ] MCQ Difficulty within tolerance (±5%)
- [ ] Flesch Score 50-60
- [ ] No placeholder content
- [ ] All final checks pass

### Result

- [ ] **APPROVED** - Chapter ready for integration
- [ ] **CONDITIONAL** - Minor fixes required (list below)
- [ ] **REJECTED** - Return to revision phase

**Conditions (if CONDITIONAL)**:
1. [Condition]
2. [Condition]

**Rejection Reasons (if REJECTED)**:
1. [Reason]
2. [Reason]

---
**Quality Gate Approver**: _____________________
**Date**: _____________________
**Chapter Status**: ☐ Draft ☐ Revision ☐ **Approved**
```

---

## Review Assignment Rules

1. **Technical Reviewer**: Must be SME in the domain, different from author
2. **Editorial Reviewer**: Consistent editor across all chapters for style consistency
3. **Quality Gate Reviewer**: Project manager or designated quality lead

## Escalation Path

```
Issue Found
    │
    ├─ Minor → Author fixes, re-submit to same phase
    │
    ├─ Major → Author revises, restart from Technical Review
    │
    └─ Critical → Escalate to project lead for decision
```

## Review Cadence

- **Weekly**: Quality Gate reviews (batch processing)
- **As-submitted**: Technical and Editorial reviews
- **Target turnaround**: 5 business days per review cycle

---

**Schema Version**: 1.0
**Last Updated**: 2026-01-31
