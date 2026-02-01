# Tasks: Baseline Specification for ADIT Preparation Guide

**Input**: Design documents from `/specs/001-baseline-spec/`
**Prerequisites**: plan.md (required), spec.md (required), research.md, data-model.md, contracts/, quickstart.md

**Tests**: No automated tests requested - this is a content development project with manual quality checklists.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3, US4)
- Include exact file paths in descriptions

## Path Conventions

This is a documentation/content development project. Paths follow the content repository structure:

```
book/
├── chapters/          # 30 chapter directories
├── appendices/        # A-H appendix files
├── assessments/       # Mock exams and practice tests
├── templates/         # Chapter, MCQ, lab, review templates
└── assets/            # Shared diagrams, tables, figures
```

---

## Phase 1: Setup (Project Infrastructure)

**Purpose**: Create content repository structure and master templates

- [x] T001 Create book directory structure per plan.md in book/
- [x] T002 [P] Create chapter directory skeleton for chapters 1-30 in book/chapters/
- [x] T003 [P] Create appendices directory structure for A-H in book/appendices/
- [x] T004 [P] Create assessments directory structure in book/assessments/
- [x] T005 [P] Create shared assets directory structure in book/assets/
- [x] T006 Create chapter-template.md in book/templates/chapter-template.md
- [x] T007 [P] Create mcq-template.md in book/templates/mcq-template.md
- [x] T008 [P] Create lab-template.md in book/templates/lab-template.md
- [x] T009 [P] Create review-checklist.md template in book/templates/review-checklist.md
- [x] T010 Create README.md with project overview in book/README.md

---

## Phase 2: Foundational (Content Standards)

**Purpose**: Core templates and standards that MUST be complete before ANY chapter content can be created

**⚠️ CRITICAL**: No chapter content work can begin until this phase is complete

- [x] T011 Populate chapter-template.md with all 11 required sections per contracts/chapter-schema.md in book/templates/chapter-template.md
- [x] T012 [P] Add Bloom's Taxonomy verb reference to chapter-template.md in book/templates/chapter-template.md
- [x] T013 [P] Add difficulty indicator guide (B/I/A/E) to chapter-template.md in book/templates/chapter-template.md
- [x] T014 Populate mcq-template.md with full format per contracts/mcq-schema.md in book/templates/mcq-template.md
- [x] T015 [P] Add distractor explanation section to mcq-template.md in book/templates/mcq-template.md
- [x] T016 [P] Add difficulty distribution guide to mcq-template.md in book/templates/mcq-template.md
- [x] T017 Populate lab-template.md with 5-section structure per research.md in book/templates/lab-template.md
- [x] T018 [P] Add troubleshooting table format to lab-template.md in book/templates/lab-template.md
- [x] T019 Populate review-checklist.md with 3-phase review process per contracts/review-checklist-schema.md in book/templates/review-checklist.md
- [x] T020 [P] Create technical review checklist section in book/templates/review-checklist.md
- [x] T021 [P] Create editorial review checklist section in book/templates/review-checklist.md
- [x] T022 [P] Create quality gate checklist section in book/templates/review-checklist.md
- [x] T023 Create citation format reference document in book/templates/citation-guide.md
- [x] T024 [P] Create diagram labeling convention guide in book/templates/diagram-guide.md

**Checkpoint**: Foundation ready - content authors can now create chapters using standardized templates

---

## Phase 3: User Story 1 - Content Author Creates Chapter Content (Priority: P1) 🎯 MVP

**Goal**: Enable a content author to create a complete, high-quality chapter following standardized templates

**Independent Test**: Have an author create Chapter 2 (Core Networking Fundamentals) using templates and validate against quality checklist. Delivers a complete, usable chapter readers can study.

### Implementation for User Story 1

#### 3.1: High-Priority Chapter Scaffolding

- [x] T025 [P] [US1] Create Chapter 2 directory structure in book/chapters/02-networking/
- [x] T026 [P] [US1] Create Chapter 3 directory structure in book/chapters/03-network-security/
- [x] T027 [P] [US1] Create Chapter 9 directory structure in book/chapters/09-cloud-computing/
- [x] T028 [P] [US1] Create Chapter 10 directory structure in book/chapters/10-cybersecurity/

#### 3.2: Chapter 2 - Core Networking Fundamentals (55 pages, 250 MCQs, 5 labs)

- [x] T029 [US1] Copy chapter-template.md to book/chapters/02-networking/content.md
- [x] T030 [US1] Fill Chapter 2 Overview section (domain, study time, prerequisites) in book/chapters/02-networking/content.md
- [x] T031 [US1] Write Chapter 2 Learning Objectives (4+ using Bloom's verbs) in book/chapters/02-networking/content.md
- [x] T032 [US1] Write Chapter 2 Introduction (2-3 paragraphs, ADIT relevance) in book/chapters/02-networking/content.md
- [x] T033 [US1] Write Section 2.1: Network Models and Architecture (B) in book/chapters/02-networking/content.md
- [x] T034 [US1] Write Section 2.2: IP Addressing and Subnetting (I) in book/chapters/02-networking/content.md
- [x] T035 [US1] Write Section 2.3: Network Devices and Topologies (I) in book/chapters/02-networking/content.md
- [x] T036 [US1] Write Section 2.4: Network Protocols (A) in book/chapters/02-networking/content.md
- [x] T037 [US1] Write Section 2.5: Enterprise Network Design (E) in book/chapters/02-networking/content.md
- [x] T038 [US1] Add 12-15 practical examples throughout Chapter 2 sections in book/chapters/02-networking/content.md
- [x] T039 [US1] Write Chapter 2 Summary and Key Takeaways (5 items) in book/chapters/02-networking/content.md
- [x] T040 [US1] Write Chapter 2 Self-Assessment Questions (3-5 open-ended) in book/chapters/02-networking/content.md

#### 3.3: Chapter 2 MCQs (250 questions)

- [x] T041 [US1] Create mcqs.md file from mcq-template.md in book/chapters/02-networking/mcqs.md
- [ ] T042 [US1] Write 63 Beginner (B) MCQs for Chapter 2 in book/chapters/02-networking/mcqs.md
- [ ] T043 [US1] Write 88 Intermediate (I) MCQs for Chapter 2 in book/chapters/02-networking/mcqs.md
- [ ] T044 [US1] Write 75 Advanced (A) MCQs for Chapter 2 in book/chapters/02-networking/mcqs.md
- [ ] T045 [US1] Write 24 Expert (E) MCQs for Chapter 2 in book/chapters/02-networking/mcqs.md
- [ ] T046 [US1] Add source references to all 250 MCQs in book/chapters/02-networking/mcqs.md
- [ ] T047 [US1] Add distractor explanations to all 250 MCQs in book/chapters/02-networking/mcqs.md

#### 3.4: Chapter 2 Labs (5 exercises)

- [x] T048 [US1] Create labs directory in book/chapters/02-networking/labs/
- [x] T049 [US1] Write Lab 2.1: IPv4 Subnetting Exercise in book/chapters/02-networking/labs/lab-02-01-subnetting.md
- [ ] T050 [US1] Write Lab 2.2: Configure VLANs in book/chapters/02-networking/labs/lab-02-02-vlans.md
- [ ] T051 [US1] Write Lab 2.3: Packet Analysis with Wireshark in book/chapters/02-networking/labs/lab-02-03-wireshark.md
- [ ] T052 [US1] Write Lab 2.4: Basic Router Configuration in book/chapters/02-networking/labs/lab-02-04-router-config.md
- [ ] T053 [US1] Write Lab 2.5: Network Troubleshooting in book/chapters/02-networking/labs/lab-02-05-troubleshooting.md

#### 3.5: Chapter 2 Diagrams (25 figures)

- [ ] T054 [US1] Create assets directory in book/chapters/02-networking/assets/
- [ ] T055 [P] [US1] Create Figure 2.1 - OSI Model Seven Layers in book/chapters/02-networking/assets/figure-02-01-osi-model.svg
- [ ] T056 [P] [US1] Create Figure 2.2 - TCP/IP Stack Comparison in book/chapters/02-networking/assets/figure-02-02-tcpip-stack.svg
- [ ] T057 [P] [US1] Create Figure 2.3 - Subnet Mask Visualization in book/chapters/02-networking/assets/figure-02-03-subnet-mask.svg
- [ ] T058 [P] [US1] Create Figure 2.4 - VLAN Architecture in book/chapters/02-networking/assets/figure-02-04-vlan-architecture.svg
- [ ] T059 [P] [US1] Create remaining 21 diagrams for Chapter 2 in book/chapters/02-networking/assets/

#### 3.6: Chapter 2 References

- [ ] T060 [US1] Compile References section with citations per FR-013 in book/chapters/02-networking/content.md
- [ ] T061 [US1] Verify all claims have 2+ authoritative sources per FR-011 in book/chapters/02-networking/content.md

**Checkpoint**: Chapter 2 complete - represents a full MVP chapter that can be validated and used

---

## Phase 4: User Story 2 - Reviewer Validates Chapter Quality (Priority: P2)

**Goal**: Enable a peer reviewer to systematically validate chapter quality against standards

**Independent Test**: Have a reviewer validate completed Chapter 2 using the review checklist process. Delivers a quality-assured chapter ready for publication.

### Implementation for User Story 2

#### 4.1: Review Process Templates

- [ ] T062 [US2] Create technical review form from review-checklist.md in book/templates/reviews/technical-review-form.md
- [ ] T063 [P] [US2] Add technical accuracy checklist (20 items) in book/templates/reviews/technical-review-form.md
- [ ] T064 [P] [US2] Add MCQ quality checklist per mcq-schema.md in book/templates/reviews/technical-review-form.md
- [ ] T065 [P] [US2] Add citation verification checklist in book/templates/reviews/technical-review-form.md
- [ ] T066 [US2] Create editorial review form in book/templates/reviews/editorial-review-form.md
- [ ] T067 [P] [US2] Add readability checklist (Flesch 50-60 target) in book/templates/reviews/editorial-review-form.md
- [ ] T068 [P] [US2] Add formatting consistency checklist in book/templates/reviews/editorial-review-form.md
- [ ] T069 [P] [US2] Add structure compliance checklist (11 sections) in book/templates/reviews/editorial-review-form.md
- [ ] T070 [US2] Create quality gate form in book/templates/reviews/quality-gate-form.md
- [ ] T071 [P] [US2] Add metrics verification checklist (page/MCQ/diagram/lab counts) in book/templates/reviews/quality-gate-form.md
- [ ] T072 [P] [US2] Add MCQ difficulty distribution verification in book/templates/reviews/quality-gate-form.md
- [ ] T073 [P] [US2] Add final sign-off section in book/templates/reviews/quality-gate-form.md

#### 4.2: Review Workflow Documentation

- [ ] T074 [US2] Create review process guide in book/templates/reviews/review-process-guide.md
- [ ] T075 [P] [US2] Document escalation path (minor/major/critical) in book/templates/reviews/review-process-guide.md
- [ ] T076 [P] [US2] Document review cadence and timing expectations in book/templates/reviews/review-process-guide.md
- [ ] T077 [P] [US2] Create reviewer assignment guidelines in book/templates/reviews/review-process-guide.md

#### 4.3: Sample Review (Chapter 2)

- [ ] T078 [US2] Create Chapter 2 reviews directory in book/chapters/02-networking/reviews/
- [ ] T079 [US2] Perform technical review of Chapter 2 in book/chapters/02-networking/reviews/technical-review.md
- [ ] T080 [US2] Perform editorial review of Chapter 2 in book/chapters/02-networking/reviews/editorial-review.md
- [ ] T081 [US2] Complete quality gate verification of Chapter 2 in book/chapters/02-networking/reviews/quality-gate.md

**Checkpoint**: Review process validated - can be applied to all subsequent chapters

---

## Phase 5: User Story 3 - Reader Studies a Topic Systematically (Priority: P3)

**Goal**: Enable readers to study effectively with clear navigation, progressive difficulty, and self-assessment

**Independent Test**: Have a reader work through Chapter 2, Section 2.2 (IP Addressing), complete Lab 2.1, and answer 10 MCQs. Measures learning effectiveness.

### Implementation for User Story 3

#### 5.1: Navigation and Readability Enhancements

- [ ] T082 [US3] Add chapter navigation aids (difficulty markers) to Chapter 2 in book/chapters/02-networking/content.md
- [ ] T083 [P] [US3] Add section cross-references within Chapter 2 in book/chapters/02-networking/content.md
- [ ] T084 [P] [US3] Add "Prerequisites" callout boxes at section starts in book/chapters/02-networking/content.md
- [ ] T085 [P] [US3] Add "Estimated Time" indicators per section in book/chapters/02-networking/content.md

#### 5.2: Reader Experience Enhancements

- [ ] T086 [US3] Add learning path indicators (B→I→A→E progression) in book/chapters/02-networking/content.md
- [ ] T087 [P] [US3] Add "Key Concept" highlight boxes in book/chapters/02-networking/content.md
- [ ] T088 [P] [US3] Add "Real-World Application" callout boxes in book/chapters/02-networking/content.md
- [ ] T089 [P] [US3] Add "Exam Tip" callout boxes for important concepts in book/chapters/02-networking/content.md

#### 5.3: Self-Assessment Integration

- [ ] T090 [US3] Group MCQs by section for targeted practice in book/chapters/02-networking/mcqs.md
- [ ] T091 [P] [US3] Add section reference to each MCQ per mcq-schema.md in book/chapters/02-networking/mcqs.md
- [ ] T092 [P] [US3] Verify all MCQ explanations are educational (not just correct/incorrect) in book/chapters/02-networking/mcqs.md

#### 5.4: Appendix Support for Readers

- [ ] T093 [US3] Create Glossary (Appendix A) structure in book/appendices/A-glossary.md
- [ ] T094 [P] [US3] Add Chapter 2 terms to Glossary (50+ terms) in book/appendices/A-glossary.md
- [ ] T095 [US3] Create Acronyms (Appendix B) structure in book/appendices/B-acronyms.md
- [ ] T096 [P] [US3] Add Chapter 2 acronyms (OSI, TCP, IP, etc.) in book/appendices/B-acronyms.md

**Checkpoint**: Reader experience validated - content is navigable, progressive, and self-assessable

---

## Phase 6: User Story 4 - Project Manager Tracks Progress (Priority: P4)

**Goal**: Enable project manager to track development progress and quality metrics across all chapters

**Independent Test**: PM can view deliverables matrix showing Chapter 2 completion status with all metrics (pages, MCQs, diagrams, labs, review status).

### Implementation for User Story 4

#### 6.1: Progress Tracking Templates

- [ ] T097 [US4] Create deliverables matrix template in book/templates/tracking/deliverables-matrix.md
- [ ] T098 [P] [US4] Add all 30 chapters with targets per spec.md in book/templates/tracking/deliverables-matrix.md
- [ ] T099 [P] [US4] Add all 8 appendices with targets in book/templates/tracking/deliverables-matrix.md
- [ ] T100 [P] [US4] Add status columns (outline/draft/review/approved) in book/templates/tracking/deliverables-matrix.md
- [ ] T101 [P] [US4] Add metrics columns (actual vs target for pages/MCQs/diagrams/labs) in book/templates/tracking/deliverables-matrix.md

#### 6.2: Progress Report Templates

- [ ] T102 [US4] Create progress report template in book/templates/tracking/progress-report.md
- [ ] T103 [P] [US4] Add completion percentage calculation in book/templates/tracking/progress-report.md
- [ ] T104 [P] [US4] Add chapters-by-status breakdown in book/templates/tracking/progress-report.md
- [ ] T105 [P] [US4] Add quality gate pass/fail summary in book/templates/tracking/progress-report.md

#### 6.3: Priority Queue Management

- [ ] T106 [US4] Create chapter priority queue document in book/templates/tracking/priority-queue.md
- [ ] T107 [P] [US4] List high-priority chapters (2,3,4,5,9,10,14,19) with dependencies in book/templates/tracking/priority-queue.md
- [ ] T108 [P] [US4] List medium-priority chapters with dependencies in book/templates/tracking/priority-queue.md
- [ ] T109 [P] [US4] List lower-priority chapters with dependencies in book/templates/tracking/priority-queue.md

#### 6.4: Sample Progress Update

- [ ] T110 [US4] Update deliverables matrix with Chapter 2 actual metrics in book/templates/tracking/deliverables-matrix.md
- [ ] T111 [US4] Generate sample progress report showing Chapter 2 completion in book/templates/tracking/progress-report.md

**Checkpoint**: Project tracking established - PM can monitor progress across all content

---

## Phase 7: Polish & Cross-Cutting Concerns

**Purpose**: Improvements that affect all user stories and chapters

- [ ] T112 [P] Verify all templates cross-reference each other consistently in book/templates/
- [ ] T113 [P] Create master index template for book-wide navigation in book/templates/index-template.md
- [ ] T114 [P] Create table of contents generator guide in book/templates/toc-guide.md
- [ ] T115 Validate quickstart.md against actual workflow experience in specs/001-baseline-spec/quickstart.md
- [ ] T116 [P] Update research.md with any new findings during implementation in specs/001-baseline-spec/research.md
- [ ] T117 Run readability analysis on Chapter 2 (target: Flesch 50-60) in book/chapters/02-networking/content.md
- [ ] T118 Verify Chapter 2 meets all 13 constitution principles in .specify/memory/constitution.md
- [ ] T119 [P] Create author onboarding checklist in book/templates/author-onboarding.md
- [ ] T120 Document lessons learned from Chapter 2 development in specs/001-baseline-spec/lessons-learned.md

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS all user stories
- **User Story 1 (Phase 3)**: Depends on Foundational phase completion
- **User Story 2 (Phase 4)**: Depends on User Story 1 (needs a completed chapter to review)
- **User Story 3 (Phase 5)**: Depends on User Story 1 (needs content to navigate)
- **User Story 4 (Phase 6)**: Can start after Foundational; fully useful after User Story 1
- **Polish (Phase 7)**: Depends on all user stories being complete

### User Story Dependencies

```
Setup (Phase 1)
     │
     ▼
Foundational (Phase 2) ──── BLOCKS ALL ────┐
     │                                      │
     ▼                                      ▼
User Story 1 (P1) ◄─────────────── User Story 4 (P4) can start
     │                                   templates
     ├─────────────────┐
     ▼                 ▼
User Story 2 (P2)  User Story 3 (P3)
     │                 │
     └────────┬────────┘
              ▼
         Polish (Phase 7)
```

### Within User Story 1 (Content Creation)

1. Chapter scaffolding (T025-T028) can run in parallel
2. Content sections (T029-T040) must be sequential (outline → draft)
3. MCQs (T041-T047) can start after content sections complete
4. Labs (T048-T053) can run in parallel with MCQs
5. Diagrams (T054-T059) can run in parallel with MCQs and Labs
6. References (T060-T061) must be final (after all content exists)

### Parallel Opportunities

#### Phase 1 (Setup)
```bash
# Run in parallel:
T002 Create chapter directories
T003 Create appendices directories
T004 Create assessments directories
T005 Create assets directories
```

#### Phase 2 (Foundational)
```bash
# Run in parallel:
T012 Add Bloom's verbs reference
T013 Add difficulty indicator guide
# Then:
T015 Add distractor explanation
T016 Add difficulty distribution guide
# Then:
T020 Create technical review checklist
T021 Create editorial review checklist
T022 Create quality gate checklist
```

#### Phase 3 (User Story 1)
```bash
# Run in parallel (chapter scaffolding):
T025 Create Chapter 2 directory
T026 Create Chapter 3 directory
T027 Create Chapter 9 directory
T028 Create Chapter 10 directory

# Run in parallel (diagrams):
T055 Create OSI Model diagram
T056 Create TCP/IP Stack diagram
T057 Create Subnet Mask diagram
T058 Create VLAN Architecture diagram
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup (T001-T010)
2. Complete Phase 2: Foundational (T011-T024)
3. Complete Phase 3: User Story 1 - Chapter 2 (T025-T061)
4. **STOP and VALIDATE**: Review Chapter 2 against all quality checklists
5. Deploy Chapter 2 as proof-of-concept

### Incremental Delivery

1. Setup + Foundational → Templates ready
2. User Story 1 (Chapter 2) → First complete chapter → **MVP!**
3. User Story 2 → Review process validated
4. User Story 3 → Reader experience validated
5. User Story 4 → Project tracking established
6. Repeat Phase 3 pattern for Chapters 3, 9, 10 (high priority)
7. Continue with medium and lower priority chapters

### Chapter Development Velocity

After MVP (Chapter 2), expected velocity per chapter:

| Priority | Pages | MCQs | Labs | Estimated Effort |
|----------|-------|------|------|------------------|
| High | 50-60 | 250 | 5-6 | 12-15 days |
| Medium | 35-45 | 170-200 | 3-4 | 8-12 days |
| Lower | 30-35 | 150-160 | 2-3 | 6-10 days |

---

## Summary

| Phase | Tasks | Parallel Tasks | Key Deliverable |
|-------|-------|----------------|-----------------|
| Phase 1: Setup | 10 | 5 | Repository structure |
| Phase 2: Foundational | 14 | 10 | Master templates |
| Phase 3: User Story 1 (P1) | 37 | 12 | Chapter 2 complete |
| Phase 4: User Story 2 (P2) | 20 | 15 | Review process |
| Phase 5: User Story 3 (P3) | 15 | 11 | Reader experience |
| Phase 6: User Story 4 (P4) | 15 | 10 | Progress tracking |
| Phase 7: Polish | 9 | 6 | Final validation |
| **TOTAL** | **120** | **69** | |

### MVP Scope

- **Minimum Viable Product**: Phase 1 + Phase 2 + Phase 3 (User Story 1)
- **Tasks for MVP**: 61 tasks
- **Deliverable**: Complete Chapter 2 (Core Networking Fundamentals) with 55 pages, 250 MCQs, 5 labs, 25 diagrams

### Independent Test Criteria per User Story

| Story | Independent Test | Verification |
|-------|------------------|--------------|
| US1 | Create Chapter 2 using templates | Chapter passes all schema validations |
| US2 | Review Chapter 2 using checklists | All three review phases documented |
| US3 | Reader completes Chapter 2 study | Navigation works, MCQs assessable |
| US4 | PM generates progress report | Metrics accurate, status visible |

---

**Tasks Status**: COMPLETE
**Total Tasks**: 120
**Parallel Opportunities**: 69 tasks can run in parallel within their phases
**Next Step**: Begin with Phase 1: Setup (T001-T010)
