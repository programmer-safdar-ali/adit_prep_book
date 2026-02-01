# Data Model: ADIT Preparation Guide Entities

**Feature**: 001-baseline-spec
**Date**: 2026-01-31
**Purpose**: Define entities, attributes, relationships, and validation rules for content management

---

## Entity Relationship Diagram

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                            BOOK                                             │
│  - title: "Assistant Director IT Preparation Guide"                         │
│  - version: "1.0"                                                           │
│  - total_pages: 1307                                                        │
│  - total_mcqs: 5000                                                         │
└─────────────────────────────────────────────────────────────────────────────┘
           │ contains
           ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           PART (1:5)                                        │
│  - number: 1-5                                                              │
│  - title: "Foundation", "Infrastructure & Cloud", etc.                      │
└─────────────────────────────────────────────────────────────────────────────┘
           │ contains
           ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                         CHAPTER (1:30)                                      │
│  - number, title, domain, priority                                          │
│  - page_target, mcq_target, lab_target, diagram_target                      │
│  - status: outline | draft | review | revision | approved                   │
│  - author, reviewer                                                         │
└─────────────────────────────────────────────────────────────────────────────┘
           │ contains (1:N)
           ├──────────────────┬──────────────────┬──────────────────┐
           ▼                  ▼                  ▼                  ▼
┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
│     SECTION      │  │       MCQ        │  │     DIAGRAM      │  │       LAB        │
│  - number        │  │  - id            │  │  - figure_number │  │  - id            │
│  - title         │  │  - stem          │  │  - title         │  │  - title         │
│  - difficulty    │  │  - options[4]    │  │  - type          │  │  - objective     │
│  - content       │  │  - correct       │  │  - source_file   │  │  - prerequisites │
└──────────────────┘  │  - difficulty    │  │  - caption       │  │  - steps[]       │
                      │  - explanation   │  └──────────────────┘  │  - validation[]  │
                      │  - source_ref    │                        │  - troubleshoot[]│
                      └──────────────────┘                        └──────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│                          REVIEW (1:3 per Chapter)                           │
│  - type: technical | editorial | quality_gate                               │
│  - checklist: ChecklistItem[]                                               │
│  - status: pending | pass | fail                                            │
│  - reviewer, date, comments                                                 │
└─────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────┐
│                         APPENDIX (A-H)                                      │
│  - letter: A-H                                                              │
│  - title, page_target, content                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Entity Definitions

### 1. Chapter

Represents a complete learning unit covering one knowledge domain.

| Attribute | Type | Required | Validation |
|-----------|------|----------|------------|
| number | Integer | Yes | 1-30 |
| title | String | Yes | Max 80 chars |
| domain | String | Yes | One of 25 domains |
| priority | Enum | Yes | High, Medium, Lower, Setup, Assessment, Reference |
| page_target | Integer | Yes | 15-60 based on priority |
| mcq_target | Integer | Yes | 0-250 based on priority |
| lab_target | Integer | Yes | 0-6 based on domain |
| diagram_target | Integer | Yes | 5-25 based on content |
| status | Enum | Yes | outline, draft, technical_review, editorial_review, revision, quality_gate, approved |
| author | String | Yes | Author identifier |
| reviewer | String | No | Assigned after draft |
| created_date | Date | Yes | ISO 8601 |
| modified_date | Date | Yes | ISO 8601 |

**State Transitions:**
```
outline → draft → technical_review → revision → editorial_review → revision → quality_gate → approved
                        ↓                              ↓                           ↓
                   (fail: revision)              (fail: revision)            (fail: revision)
```

**Business Rules:**
- Chapter cannot enter quality_gate until technical_review = pass AND editorial_review = pass
- Only chapters with status = approved count toward completion metrics
- Priority determines page/MCQ allocation per FR-020/FR-021

---

### 2. MCQ (Multiple Choice Question)

Represents a single assessment question within a chapter.

| Attribute | Type | Required | Validation |
|-----------|------|----------|------------|
| id | String | Yes | Format: `MCQ-[chapter]-[sequence]` (e.g., MCQ-02-015) |
| chapter_number | Integer | Yes | Reference to parent chapter |
| stem | String | Yes | Min 20 chars, no negative wording |
| option_a | String | Yes | Non-empty |
| option_b | String | Yes | Non-empty |
| option_c | String | Yes | Non-empty |
| option_d | String | Yes | Non-empty |
| correct_answer | Enum | Yes | A, B, C, or D |
| difficulty | Enum | Yes | B, I, A, E |
| explanation | String | Yes | Min 50 words |
| explanation_a | String | Yes | Why A is incorrect (if not correct) |
| explanation_b | String | Yes | Why B is incorrect (if not correct) |
| explanation_c | String | Yes | Why C is incorrect (if not correct) |
| explanation_d | String | Yes | Why D is incorrect (if not correct) |
| source_reference | String | Yes | Citation per FR-013 |
| related_section | String | Yes | Section reference (e.g., 2.3) |
| tags | String[] | No | Topic keywords |

**Business Rules:**
- Each chapter must have exactly mcq_target MCQs
- Difficulty distribution per chapter: 25% B, 35% I, 30% A, 10% E (±5%)
- Stem must NOT contain: "NOT", "EXCEPT", "All of the above", "None of the above"
- All four options must be grammatically parallel
- Explanation for correct answer must be ≥50 words

---

### 3. Diagram

Represents a visual element within a chapter.

| Attribute | Type | Required | Validation |
|-----------|------|----------|------------|
| figure_number | String | Yes | Format: `[chapter].[sequence]` (e.g., 2.3) |
| chapter_number | Integer | Yes | Reference to parent chapter |
| title | String | Yes | Descriptive, 10-100 chars |
| type | Enum | Yes | flowchart, architecture, comparison, process, topology, table, infographic |
| source_file | String | Yes | Path to source file (SVG, PNG, or draw.io) |
| caption | String | No | Additional context |
| legend_required | Boolean | Yes | True if uses symbols/colors |
| legend | String | Conditional | Required if legend_required = true |
| adapted_from | String | No | Source citation if adapted |
| width_inches | Decimal | No | Default: 6.0, Max: 7.5 |
| resolution_dpi | Integer | No | Minimum: 300 for print |

**Business Rules:**
- Figure numbers must be sequential within chapter
- Diagrams with symbols or color coding MUST include legend
- All text in diagram must be readable at 100% zoom (min 10pt equivalent)

---

### 4. Lab

Represents a hands-on practical exercise within a chapter.

| Attribute | Type | Required | Validation |
|-----------|------|----------|------------|
| id | String | Yes | Format: `Lab-[chapter]-[sequence]` (e.g., Lab-02-01) |
| chapter_number | Integer | Yes | Reference to parent chapter |
| title | String | Yes | Action-oriented, max 80 chars |
| objective | String | Yes | What reader will accomplish |
| time_required | String | Yes | Format: "X-Y minutes" |
| prerequisites | String[] | Yes | List of required knowledge/setup |
| environment | String | Yes | Required software/hardware |
| difficulty | Enum | Yes | B, I, A, E |
| steps | Step[] | Yes | Minimum 3 steps |
| validation_checklist | String[] | Yes | Minimum 2 checkpoints |
| troubleshooting | TroubleshootItem[] | Yes | Minimum 2 common issues |

**Step Object:**
| Attribute | Type | Required |
|-----------|------|----------|
| number | Integer | Yes |
| instruction | String | Yes |
| code_block | String | No |
| expected_output | String | Yes |

**TroubleshootItem Object:**
| Attribute | Type | Required |
|-----------|------|----------|
| issue | String | Yes |
| cause | String | Yes |
| solution | String | Yes |

**Business Rules:**
- Each domain chapter must have ≥3 labs (except Chapter 1)
- Labs must be completable independently
- All code/commands must be tested on specified platform

---

### 5. Section

Represents a content section within a chapter.

| Attribute | Type | Required | Validation |
|-----------|------|----------|------------|
| number | String | Yes | Format: `[chapter].[sequence]` (e.g., 2.3) |
| chapter_number | Integer | Yes | Reference to parent chapter |
| title | String | Yes | Topic name, max 60 chars |
| difficulty | Enum | Yes | B, I, A, E |
| content | String | Yes | Markdown content |
| subsections | Section[] | No | Nested subsections (max depth: 2) |
| examples | Example[] | No | Practical examples |

**Business Rules:**
- Content must progress from lower to higher difficulty within chapter
- Each section must be marked with difficulty indicator
- Minimum 10 examples per chapter (FR-004)

---

### 6. Review

Represents a quality checkpoint for a chapter.

| Attribute | Type | Required | Validation |
|-----------|------|----------|------------|
| id | String | Yes | Format: `Review-[chapter]-[type]` |
| chapter_number | Integer | Yes | Reference to parent chapter |
| type | Enum | Yes | technical, editorial, quality_gate |
| status | Enum | Yes | pending, pass, fail |
| reviewer | String | Yes | Reviewer identifier |
| date | Date | Yes | ISO 8601 |
| checklist | ChecklistItem[] | Yes | Type-specific items |
| comments | String | No | General feedback |
| issues | Issue[] | No | Specific issues found |

**ChecklistItem Object:**
| Attribute | Type | Required |
|-----------|------|----------|
| item | String | Yes |
| status | Enum | Yes | pass, fail, na |
| note | String | No |

**Business Rules:**
- Technical review must verify: accuracy, completeness, currency, citations
- Editorial review must verify: readability, formatting, consistency
- Quality gate must verify: page count, MCQ count, diagram count, lab count, readability score
- Chapter cannot be approved until all three reviews pass

---

### 7. Appendix

Represents supplementary reference material.

| Attribute | Type | Required | Validation |
|-----------|------|----------|------------|
| letter | Char | Yes | A-H |
| title | String | Yes | Max 60 chars |
| page_target | Integer | Yes | 8-30 based on content |
| content | String | Yes | Markdown content |
| entries | Entry[] | Conditional | For glossary/acronym appendices |

**Entry Object (for Appendix A/B):**
| Attribute | Type | Required |
|-----------|------|----------|
| term | String | Yes |
| definition | String | Yes |
| see_also | String[] | No |

**Business Rules:**
- Appendix A (Glossary) must have ≥500 terms
- Appendix B (Acronyms) must cover all acronyms used in book
- Each appendix must be self-contained and referenceable

---

## Relationships Summary

| Parent | Child | Cardinality | Constraint |
|--------|-------|-------------|------------|
| Book | Part | 1:5 | Exactly 5 parts |
| Part | Chapter | 1:N | Variable (4-9 chapters per part) |
| Chapter | Section | 1:N | Variable based on page target |
| Chapter | MCQ | 1:N | Exactly mcq_target MCQs |
| Chapter | Diagram | 1:N | Approximately diagram_target |
| Chapter | Lab | 1:N | Exactly lab_target labs |
| Chapter | Review | 1:3 | One per review type |
| Book | Appendix | 1:8 | Exactly 8 appendices |

---

## Validation Summary

### Chapter-Level Validations
- [ ] All 11 required sections present (FR-001)
- [ ] Learning objectives use Bloom's verbs (FR-002)
- [ ] Content progresses B → I → A → E (FR-003)
- [ ] Minimum 10 examples (FR-004)
- [ ] Labs have all 5 components (FR-005)
- [ ] Page count ≥95% of target
- [ ] MCQ count = 100% of target
- [ ] Diagram count ≥90% of target
- [ ] Lab count = 100% of target
- [ ] Flesch score 50-60 (FR-014)

### MCQ-Level Validations
- [ ] Clear positive stem (FR-019)
- [ ] Exactly 4 options
- [ ] Difficulty marked (FR-016)
- [ ] Explanation ≥50 words (FR-017)
- [ ] All distractors explained (FR-017)
- [ ] Source reference present (FR-010)

### Diagram-Level Validations
- [ ] Figure number format correct (FR-006)
- [ ] Title is descriptive
- [ ] Legend present if symbols used
- [ ] Text readable at 100% zoom
- [ ] Source cited if adapted

---

**Data Model Status**: COMPLETE
**Next**: Contract Schemas
