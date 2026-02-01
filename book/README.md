# ADIT Preparation Guide - Content Repository

**Version**: 1.0 (Draft)
**Last Updated**: 2026-02-01

---

## Overview

This repository contains the source content for the **Assistant Director IT Preparation Guide**, a comprehensive study resource covering 25 IT knowledge domains across 30 chapters with 5,000+ multiple-choice questions.

---

## Repository Structure

```
book/
├── chapters/           # 30 chapter directories (01-30)
│   ├── 01/            # Chapter 1: Introduction
│   ├── 02/            # Chapter 2: Core Networking Fundamentals
│   │   ├── content.md # Main chapter content
│   │   ├── mcqs.md    # Multiple choice questions
│   │   ├── labs/      # Hands-on lab exercises
│   │   └── assets/    # Diagrams, figures, images
│   └── ...
├── appendices/         # Supplementary reference material (A-H)
│   ├── A-glossary.md
│   ├── B-acronyms.md
│   └── ...
├── assessments/        # Practice tests and mock exams
│   ├── mock-exams/     # Full-length mock examinations
│   └── practice-tests/ # Topic-specific practice tests
├── templates/          # Standardized templates for content creation
│   ├── chapter-template.md
│   ├── mcq-template.md
│   ├── lab-template.md
│   ├── review-checklist.md
│   ├── reviews/        # Review form templates
│   └── tracking/       # Progress tracking templates
└── assets/             # Shared assets across chapters
    ├── diagrams/
    ├── tables/
    └── figures/
```

---

## Content Targets

| Category | Target |
|----------|--------|
| Total Pages | 1,307 |
| Total MCQs | 5,000 |
| Total Labs | 91 |
| Total Diagrams | 499 |
| Chapters | 30 |
| Appendices | 8 |

---

## Chapter Priority

### High Priority (Start First)
- Chapter 2: Core Networking Fundamentals (55 pages, 250 MCQs)
- Chapter 3: Network Security & Infrastructure Protection (55 pages, 250 MCQs)
- Chapter 9: Cloud Computing & Virtualization (55 pages, 250 MCQs)
- Chapter 10: Cybersecurity & Information Security (55 pages, 250 MCQs)

### Medium Priority
- Chapters 4, 5, 6, 7, 8, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 23, 25

### Lower Priority
- Chapters 21, 22, 24, 26

### Reference (No MCQs)
- Chapters 27-30, Appendices A-H

---

## Getting Started

### For Content Authors

1. Read the project constitution: `.specify/memory/constitution.md`
2. Review the specification: `specs/001-baseline-spec/spec.md`
3. Follow the quickstart guide: `specs/001-baseline-spec/quickstart.md`
4. Use templates from `book/templates/`

### Content Development Workflow

```
1. Select chapter from priority queue
2. Copy chapter-template.md to chapter directory
3. Fill outline (1-2 days)
4. Submit outline for approval
5. Draft content (5-10 days)
6. Self-review against checklist
7. Submit for Technical Review
8. Address feedback
9. Quality Gate verification
10. APPROVED → Next chapter
```

---

## Quality Standards

### Chapter Requirements
- All 11 required sections present
- Learning objectives use Bloom's verbs
- Difficulty progression: B → I → A → E
- Minimum 10 practical examples
- Minimum 3 labs per domain chapter

### MCQ Requirements
- Clear, positive question stems
- 4 options (A-D) only
- Explanation ≥50 words for correct answer
- All distractors explained
- Difficulty distribution: 25% B, 35% I, 30% A, 10% E

### Readability
- Flesch Reading Ease: 50-60
- Average sentence length: 15-20 words
- Technical jargon explained on first use

---

## Review Process

Each chapter passes through three review phases:

1. **Technical Review** (2-3 days) - SME validates accuracy
2. **Editorial Review** (1-2 days) - Editor validates readability
3. **Quality Gate** (1 day) - PM validates metrics

See `templates/review-checklist.md` for detailed checklists.

---

## File Naming Conventions

### Content Files
- Chapter content: `content.md`
- MCQs: `mcqs.md`
- Labs: `lab-[chapter]-[sequence]-[slug].md`

### Assets
- Diagrams: `figure-[chapter]-[sequence]-[slug].svg`
- Tables: `table-[chapter]-[sequence]-[slug].md`

---

## Citation Format

```
[Organization]. "[Title]." [Version/Edition]. [Year]. [URL]
```

Examples:
- IETF. "RFC 791 - Internet Protocol." 1981. https://tools.ietf.org/html/rfc791
- Microsoft. "Windows Server 2022 Documentation." 2025. https://docs.microsoft.com/windows-server
- ISO. "ISO/IEC 27001:2022." 2022.

---

## Related Documents

- Project Constitution: `.specify/memory/constitution.md`
- Feature Specification: `specs/001-baseline-spec/spec.md`
- Implementation Plan: `specs/001-baseline-spec/plan.md`
- Data Model: `specs/001-baseline-spec/data-model.md`
- Contract Schemas: `specs/001-baseline-spec/contracts/`

---

## Contributing

1. Create content in the appropriate chapter directory
2. Use the provided templates
3. Follow the quality standards
4. Submit for review when complete

---

**Status**: Repository Structure Complete
**Next Step**: Begin content development with high-priority chapters
