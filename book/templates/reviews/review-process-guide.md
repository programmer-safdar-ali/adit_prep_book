# Review Process Guide

**Purpose**: Document the three-phase review process, escalation paths, and reviewer responsibilities

---

## Overview

Every chapter must pass through three sequential review phases before approval:

```
                    ┌─────────────────────┐
                    │   Chapter Draft     │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
              ┌────►│  Technical Review   │ (2-3 days)
              │     │   SME Validation    │
              │     └──────────┬──────────┘
              │                │ PASS
     FAIL     │                ▼
    (Revise)  │     ┌─────────────────────┐
              │     │  Editorial Review   │ (1-2 days)
              ├────►│  Editor Validation  │
              │     └──────────┬──────────┘
              │                │ PASS
              │                ▼
              │     ┌─────────────────────┐
              └────►│   Quality Gate      │ (1 day)
                    │   PM Verification   │
                    └──────────┬──────────┘
                               │ PASS
                               ▼
                    ┌─────────────────────┐
                    │      APPROVED       │
                    └─────────────────────┘
```

---

## Phase 1: Technical Review

### Purpose
Validate technical accuracy, completeness, and currency of content.

### Duration
2-3 business days

### Reviewer Requirements
- Subject Matter Expert (SME) in the chapter's domain
- **Cannot be the content author**
- Familiar with current industry standards and best practices
- Access to verification resources (labs, documentation)

### Focus Areas
1. **Technical Accuracy** (20 items)
   - Facts and definitions
   - Currency of information
   - Commands and code
   - Terminology and standards

2. **Completeness** (8 items)
   - Topic coverage
   - Difficulty progression
   - Examples and labs

3. **MCQ Quality** (10 items)
   - Answer accuracy
   - Distractor plausibility
   - Explanation quality

4. **Citations** (6 items)
   - Source authority
   - Format compliance
   - Link validity

### Pass Criteria
- Score ≥45/50 (90%)
- Zero Critical issues
- No more than 3 Major issues

### Deliverable
Completed Technical Review Form with detailed feedback

---

## Phase 2: Editorial Review

### Purpose
Validate readability, formatting, and consistency.

### Duration
1-2 business days

### Prerequisite
Technical Review = PASS

### Reviewer Requirements
- Editorial experience
- Consistent editor across chapters (for style consistency)
- Access to readability analysis tools

### Focus Areas
1. **Readability** (8 items)
   - Flesch score 50-60
   - Sentence/paragraph length
   - Clarity and flow

2. **Formatting** (24 items)
   - Heading hierarchy
   - Section numbering
   - Visual elements
   - Code formatting

3. **Structure** (5 items)
   - 11 required sections
   - Section order
   - Schema compliance

4. **Grammar and Style** (8 items)
   - Spelling and grammar
   - Terminology consistency
   - Professional tone

### Pass Criteria
- Score ≥40/45 (89%)
- Flesch Reading Ease 50-60
- All 11 sections present

### Deliverable
Completed Editorial Review Form with readability metrics

---

## Phase 3: Quality Gate

### Purpose
Final verification of metrics and sign-off for approval.

### Duration
1 business day

### Prerequisites
- Technical Review = PASS
- Editorial Review = PASS

### Reviewer Requirements
- Project Manager or designated Quality Lead
- Authority to approve chapters
- Access to all metrics and tracking systems

### Focus Areas
1. **Metric Verification**
   - Page count ≥95% of target
   - MCQ count = 100% of target
   - Diagram count ≥90% of target
   - Lab count = 100% of target
   - Example count ≥10

2. **MCQ Distribution**
   - B: 25% (±5%)
   - I: 35% (±5%)
   - A: 30% (±5%)
   - E: 10% (±5%)

3. **Final Checks**
   - No placeholder content
   - All references valid
   - Assets in correct locations

4. **Constitution Compliance**
   - Spot-check against principles

### Pass Criteria
- All metrics within tolerance
- Both prerequisite reviews PASS
- All final checks PASS

### Deliverable
Completed Quality Gate Form with final approval

---

## Escalation Path

### Issue Severity Definitions

| Severity | Definition | Examples |
|----------|------------|----------|
| **Critical** | Factually incorrect; could mislead readers significantly | Wrong protocol behavior, incorrect security advice, broken code |
| **Major** | Incomplete or unclear content affecting learning | Missing section, confusing explanation, unclear lab steps |
| **Minor** | Cosmetic issues; minor inaccuracies | Typos, formatting inconsistencies, minor style issues |

### Escalation Actions

```
Issue Found
    │
    ├─── Minor ──► Author fixes in current cycle
    │              Re-submit to same phase
    │              Target: 1 day turnaround
    │
    ├─── Major ──► Author revises content
    │              Restart from Technical Review
    │              Target: 3-5 days turnaround
    │
    └─── Critical ► Escalate to Project Lead
                    Decision on scope/approach
                    May require SME consultation
                    Target: Case-by-case
```

### Escalation Contacts

| Level | Role | Responsibility |
|-------|------|----------------|
| Level 1 | Reviewer | Initial issue identification |
| Level 2 | Author | Issue resolution |
| Level 3 | Lead Author/Editor | Complex issues, disputes |
| Level 4 | Project Lead | Critical issues, timeline decisions |

---

## Review Cadence and Timing

### Standard Review Schedule

| Phase | Start | Duration | Target Completion |
|-------|-------|----------|-------------------|
| Technical Review | Day 1 | 2-3 days | Day 3 |
| Revision (if needed) | Day 4 | 1-2 days | Day 5 |
| Editorial Review | Day 6 | 1-2 days | Day 7 |
| Revision (if needed) | Day 8 | 1 day | Day 8 |
| Quality Gate | Day 9 | 1 day | Day 9 |
| **Total (no revision)** | | | **5-6 days** |
| **Total (with revisions)** | | | **7-9 days** |

### Weekly Quality Gate Schedule

Quality Gates are processed in batches:

- **Submission Deadline**: Friday 5 PM
- **Quality Gate Review**: Monday
- **Results Published**: Monday 5 PM
- **Revisions Due**: Wednesday 5 PM

### Priority Queue

During high-priority periods, reviews are processed in this order:

1. Chapters blocking other work
2. High-priority chapters (2, 3, 9, 10)
3. Medium-priority chapters
4. Lower-priority chapters
5. Reference chapters and appendices

---

## Reviewer Assignment Guidelines

### Technical Review

| Domain | Preferred Reviewer Profile |
|--------|---------------------------|
| Networking (Ch 2, 14) | CCNA/CCNP certified or equivalent |
| Security (Ch 3, 10) | CISSP/CEH certified or equivalent |
| Cloud (Ch 9) | AWS/Azure/GCP certified |
| Database (Ch 5) | DBA experience |
| Systems (Ch 4, 19) | Senior sysadmin experience |

### Editorial Review

- Assign consistent editor to related chapter groups
- Rotate editors monthly to prevent fatigue
- Pair new editors with experienced reviewers

### Quality Gate

- Project Manager or designated alternate
- Backup approver identified for absences
- Two-person sign-off for first 5 chapters (calibration)

---

## Review Tools

### Required Tools

| Tool | Purpose | Access |
|------|---------|--------|
| Hemingway Editor | Readability scoring | hemingwayapp.com |
| Markdown Preview | Formatting verification | VS Code / Editor |
| Git | Version tracking | Repository access |

### Optional Tools

| Tool | Purpose | Notes |
|------|---------|-------|
| Grammarly | Grammar checking | Premium recommended |
| Packet Tracer | Lab testing | Networking chapters |
| Cloud consoles | Command testing | Cloud chapters |

---

## Revision Workflow

### After Technical Review Failure

1. Reviewer provides detailed feedback
2. Author receives notification with issues list
3. Author addresses all Critical and Major issues
4. Author submits revision with change log
5. **Restart from Technical Review**

### After Editorial Review Failure

1. Reviewer provides marked-up document
2. Author addresses formatting/style issues
3. Author submits revision
4. **Restart from Editorial Review**

### After Quality Gate Failure

**CONDITIONAL** (minor issues):
1. Author has 24 hours to fix
2. Re-submit for expedited review
3. Same-day turnaround if submitted by noon

**REJECTED**:
1. Author addresses fundamental issues
2. **Restart from Technical Review**

---

## Review Metrics Tracking

### Per-Chapter Metrics

| Metric | Target | Tracked In |
|--------|--------|------------|
| Technical Review Pass Rate | >80% first attempt | Progress tracker |
| Editorial Review Pass Rate | >90% first attempt | Progress tracker |
| Quality Gate Pass Rate | >95% first attempt | Progress tracker |
| Average Review Cycle | ≤7 days | Progress tracker |

### Reviewer Metrics

| Metric | Target | Purpose |
|--------|--------|---------|
| Reviews completed on time | >90% | Reliability |
| Issue detection accuracy | Validated quarterly | Quality |
| Feedback quality | Author satisfaction survey | Improvement |

---

## Forms and Templates

| Form | Location | Purpose |
|------|----------|---------|
| Technical Review Form | `templates/reviews/technical-review-form.md` | Phase 1 |
| Editorial Review Form | `templates/reviews/editorial-review-form.md` | Phase 2 |
| Quality Gate Form | `templates/reviews/quality-gate-form.md` | Phase 3 |

---

**Guide Version**: 1.0
**Last Updated**: 2026-02-01
