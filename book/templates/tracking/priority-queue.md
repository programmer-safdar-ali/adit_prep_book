# Chapter Priority Queue

**Last Updated**: 2026-02-01
**Queue Owner**: Project Manager

---

## Priority Framework

Chapters are prioritized based on:
1. **Content Volume**: Higher page/MCQ targets → higher priority
2. **Core Domains**: Networking, Security, Cloud are exam-heavy
3. **Dependencies**: Some chapters depend on others
4. **Resource Availability**: SME availability for review

---

## Queue Status Legend

| Status | Symbol | Description |
|--------|--------|-------------|
| Available | 🟢 | Ready to start |
| In Progress | 🟡 | Currently being worked on |
| Blocked | 🔴 | Waiting on dependency |
| Complete | ✅ | Approved and done |

---

## High Priority Queue

**Target**: Complete first for maximum content impact
**Characteristics**: 45-55 pages, 200-250 MCQs, 4-6 labs

| Order | Ch | Title | Pages | MCQs | Dependencies | Status | Owner |
|-------|-----|-------|-------|------|--------------|--------|-------|
| 1 | 2 | Core Networking Fundamentals | 55 | 250 | None | 🟡 | [Assigned] |
| 2 | 3 | Network Security & Infrastructure | 55 | 250 | Ch 2 | 🔴 | - |
| 3 | 10 | Cybersecurity & Information Security | 55 | 250 | Ch 3 | 🔴 | - |
| 4 | 9 | Cloud Computing & Virtualization | 55 | 250 | Ch 2, 4 | 🔴 | - |
| 5 | 4 | Server Administration | 50 | 220 | Ch 2 | 🔴 | - |
| 6 | 5 | Database Management | 50 | 220 | Ch 4 | 🔴 | - |
| 7 | 14 | Network Protocols | 45 | 200 | Ch 2 | 🔴 | - |
| 8 | 19 | Operating Systems | 45 | 200 | Ch 4 | 🔴 | - |

### High Priority Dependency Graph

```
Chapter 2 (Networking)
    │
    ├───► Chapter 3 (Network Security)
    │         │
    │         └───► Chapter 10 (Cybersecurity)
    │
    ├───► Chapter 14 (Network Protocols)
    │
    └───► Chapter 4 (Server Administration)
              │
              ├───► Chapter 5 (Database Management)
              │
              ├───► Chapter 9 (Cloud Computing)
              │
              └───► Chapter 19 (Operating Systems)
```

---

## Medium Priority Queue

**Target**: Complete after high-priority core domains
**Characteristics**: 35-45 pages, 170-200 MCQs, 2-4 labs

| Order | Ch | Title | Pages | MCQs | Dependencies | Status | Owner |
|-------|-----|-------|-------|------|--------------|--------|-------|
| 9 | 6 | Systems Integration | 40 | 180 | Ch 4, 5 | 🔴 | - |
| 10 | 8 | Enterprise Architecture | 40 | 180 | Ch 6, 7 | 🔴 | - |
| 11 | 7 | IT Project Management | 40 | 180 | None | 🟢 | - |
| 12 | 11 | Disaster Recovery & BCP | 40 | 175 | Ch 9, 10 | 🔴 | - |
| 13 | 12 | IT Service Management | 40 | 175 | Ch 7 | 🔴 | - |
| 14 | 15 | Data Communications | 40 | 180 | Ch 2, 14 | 🔴 | - |
| 15 | 16 | Web Technologies | 40 | 180 | Ch 14 | 🔴 | - |
| 16 | 18 | Software Engineering | 40 | 180 | None | 🟢 | - |
| 17 | 20 | System Analysis & Design | 40 | 180 | Ch 18 | 🔴 | - |
| 18 | 13 | IT Governance | 35 | 170 | Ch 7, 12 | 🔴 | - |
| 19 | 17 | Mobile Technologies | 35 | 170 | Ch 16 | 🔴 | - |
| 20 | 23 | E-Government & Digital Services | 35 | 170 | Ch 16 | 🔴 | - |
| 21 | 25 | Emerging Technologies | 35 | 170 | Ch 9 | 🔴 | - |

### Independent Medium Priority (No Dependencies)

These can start immediately without blocking:

| Ch | Title | Pages | MCQs | Status |
|----|-------|-------|------|--------|
| 7 | IT Project Management | 40 | 180 | 🟢 Available |
| 18 | Software Engineering | 40 | 180 | 🟢 Available |

---

## Lower Priority Queue

**Target**: Complete after medium-priority chapters
**Characteristics**: 30-35 pages, 150-165 MCQs, 2-3 labs

| Order | Ch | Title | Pages | MCQs | Dependencies | Status | Owner |
|-------|-----|-------|-------|------|--------------|--------|-------|
| 22 | 21 | Quality Assurance | 32 | 155 | Ch 18, 20 | 🔴 | - |
| 23 | 22 | IT Procurement | 32 | 155 | Ch 7 | 🔴 | - |
| 24 | 24 | Data Analytics | 35 | 160 | Ch 5 | 🔴 | - |
| 25 | 26 | IT Ethics & Legal | 30 | 150 | None | 🟢 | - |

### Independent Lower Priority

| Ch | Title | Pages | MCQs | Status |
|----|-------|-------|------|--------|
| 26 | IT Ethics & Legal | 30 | 150 | 🟢 Available |

---

## Setup & Reference Queue

**Target**: Complete last (except Ch 1 which can run in parallel)
**Characteristics**: No MCQs or organizing existing MCQs

| Order | Ch | Title | Pages | Dependencies | Status | Owner |
|-------|-----|-------|-------|--------------|--------|-------|
| 26 | 1 | Introduction to IT for Public Service | 20 | None | 🟢 | - |
| 27 | 29 | Study Plans | 20 | All domain chapters | 🔴 | - |
| 28 | 30 | Exam Strategy | 15 | All domain chapters | 🔴 | - |
| 29 | 27 | Assessment & Practice | 40 | All MCQs complete | 🔴 | - |
| 30 | 28 | Mock Examinations | 60 | Ch 27 | 🔴 | - |

---

## Appendices Queue

**Target**: Populate incrementally as chapters complete

| App | Title | Dependencies | Status | Notes |
|-----|-------|--------------|--------|-------|
| A | Glossary | Chapters 2-26 | 🟡 | Add terms as chapters complete |
| B | Acronyms | Chapters 2-26 | 🟡 | Add as chapters complete |
| C | Command Reference | Chapters 2-26 | 🔴 | After all chapters |
| D | Port Numbers | Ch 2, 14 | 🔴 | After networking chapters |
| E | RFC Quick Reference | Ch 2, 14, 15 | 🔴 | After protocol chapters |
| F | Certification Pathways | All | 🔴 | End of project |
| G | Additional Resources | All | 🔴 | End of project |
| H | Answer Keys | All MCQs | 🔴 | End of project |

---

## Current Sprint

**Sprint**: [Number]
**Period**: [Start] - [End]

### Active Work Items

| Ch | Title | Owner | Target | Status |
|----|-------|-------|--------|--------|
| 2 | Core Networking Fundamentals | [Name] | Complete Draft | 🟡 |

### Next Up (Ready to Start)

| Ch | Title | Est. Start | Prerequisites Met |
|----|-------|------------|-------------------|
| 7 | IT Project Management | [Date] | ✅ Yes |
| 18 | Software Engineering | [Date] | ✅ Yes |
| 26 | IT Ethics & Legal | [Date] | ✅ Yes |
| 1 | Introduction | [Date] | ✅ Yes |

---

## Queue Metrics

### Throughput (Last 4 Weeks)

| Week | Chapters Started | Chapters Completed | In Review |
|------|------------------|-------------------|-----------|
| W-4 | 0 | 0 | 0 |
| W-3 | 0 | 0 | 0 |
| W-2 | 0 | 0 | 0 |
| W-1 | 1 | 0 | 0 |

### Velocity Projection

| Priority | Chapters | Avg Days/Chapter | Est. Completion |
|----------|----------|------------------|-----------------|
| High | 8 | 15 | [Date] |
| Medium | 13 | 12 | [Date] |
| Lower | 4 | 10 | [Date] |
| Reference | 5 | 5 | [Date] |
| **Total** | **30** | - | **[Date]** |

---

## Assignment Guidelines

### Who Should Work on What

| Domain | Recommended Expertise |
|--------|----------------------|
| Networking (Ch 2, 3, 14, 15) | CCNA/CCNP background |
| Security (Ch 10, 11) | CISSP/CEH background |
| Cloud (Ch 9) | AWS/Azure certified |
| Database (Ch 5, 24) | DBA experience |
| Management (Ch 7, 12, 13) | PMP/ITIL background |
| Development (Ch 16, 18, 20) | Software development experience |

### Parallel Work Opportunities

These chapter groups can be worked on simultaneously by different authors:

**Group A**: Ch 2 → Ch 3 → Ch 10
**Group B**: Ch 7 → Ch 12 → Ch 13
**Group C**: Ch 18 → Ch 20 → Ch 21
**Group D**: Ch 1, Ch 26 (independent)

---

**Queue Version**: 1.0
**Review Frequency**: Weekly
**Next Review**: [Date]
