# Chapter Schema: Validation Contract

**Purpose**: Define mandatory structure and validation rules for all chapters

---

## Required Sections (In Order)

A valid chapter MUST contain these sections in the following order:

| # | Section | Required | Validation |
|---|---------|----------|------------|
| 1 | Chapter Overview | Yes | Domain, Study Time, Prerequisites, Difficulty Progression |
| 2 | Learning Objectives | Yes | Minimum 4 objectives using Bloom's verbs |
| 3 | Introduction | Yes | 2-3 paragraphs; relevance to ADIT role |
| 4 | Core Content Sections | Yes | Minimum 3 sections with B/I/A/E markers |
| 5 | Practical Examples | Yes | Minimum 10 examples embedded in content |
| 6 | Hands-on Labs | Conditional | Required for domain chapters (Ch 2-26); min 3 labs |
| 7 | Chapter Summary | Yes | Bulleted list of key points |
| 8 | Key Takeaways | Yes | Exactly 5 critical concepts |
| 9 | Self-Assessment Questions | Yes | 3-5 open-ended questions |
| 10 | Chapter MCQs | Conditional | Required for domain chapters; count per spec |
| 11 | References | Yes | Citations per FR-013 format |

---

## Section Specifications

### 1. Chapter Overview

```markdown
## Chapter Overview

- **Domain**: [Knowledge Domain from 25-domain list]
- **Estimated Study Time**: [X-Y hours]
- **Prerequisites**: [Previous chapters or knowledge]
- **Difficulty Progression**: Beginner → Intermediate → Advanced → Expert
```

**Validation:**
- [ ] Domain matches one of 25 defined domains
- [ ] Study time in hours, realistic for page count (approx 10 pages/hour)
- [ ] Prerequisites list specific chapter numbers or knowledge areas
- [ ] Difficulty progression statement present

### 2. Learning Objectives

```markdown
## Learning Objectives

By the end of this chapter, you will be able to:
1. [Bloom's verb] + [measurable outcome] (B)
2. [Bloom's verb] + [measurable outcome] (I)
3. [Bloom's verb] + [measurable outcome] (A)
4. [Bloom's verb] + [measurable outcome] (E)
```

**Bloom's Taxonomy Verbs by Level:**

| Level | Acceptable Verbs |
|-------|-----------------|
| B (Remember/Understand) | Define, describe, explain, identify, list, recognize, state |
| I (Apply) | Apply, calculate, demonstrate, implement, solve, use |
| A (Analyze) | Analyze, compare, contrast, differentiate, examine, troubleshoot |
| E (Evaluate/Create) | Assess, design, evaluate, justify, propose, recommend |

**Validation:**
- [ ] Minimum 4 learning objectives
- [ ] Each objective starts with approved Bloom's verb
- [ ] Each objective has difficulty indicator (B/I/A/E)
- [ ] At least one objective at each difficulty level

### 3. Introduction

**Validation:**
- [ ] 2-3 paragraphs (150-400 words)
- [ ] Explains relevance to Assistant Director IT role
- [ ] Provides real-world context
- [ ] Connects to adjacent chapters (prerequisites/next topics)

### 4. Core Content Sections

```markdown
## Section [N.1]: [Topic Name] (B)

[Content]

### Practical Example [N.1]
[Real-world scenario]

## Section [N.2]: [Topic Name] (I)

[Content]
```

**Validation:**
- [ ] Minimum 3 main sections per chapter
- [ ] Each section marked with difficulty (B/I/A/E)
- [ ] Difficulty progresses from lower to higher
- [ ] Each section has at least one practical example
- [ ] Total examples ≥ 10 per chapter

### 5. Hands-on Labs

**Validation:**
- [ ] Required for chapters 2-26 (domain chapters)
- [ ] Minimum 3 labs per domain chapter
- [ ] Each lab follows Lab Schema (see lab-schema.md)

### 6. Chapter Summary

**Validation:**
- [ ] Bulleted list format
- [ ] 8-15 key points
- [ ] Covers all main sections
- [ ] No new information introduced

### 7. Key Takeaways

```markdown
## Key Takeaways

1. [Critical concept 1]
2. [Critical concept 2]
3. [Critical concept 3]
4. [Critical concept 4]
5. [Critical concept 5]
```

**Validation:**
- [ ] Exactly 5 takeaways
- [ ] Each is a complete, standalone statement
- [ ] Represents most important concepts from chapter

### 8. Self-Assessment Questions

**Validation:**
- [ ] 3-5 open-ended questions
- [ ] Questions require paragraph-length answers
- [ ] Cover different difficulty levels
- [ ] Not answerable with single word/fact

### 9. Chapter MCQs

**Validation:**
- [ ] MCQ count matches chapter target
- [ ] Difficulty distribution: 25% B, 35% I, 30% A, 10% E (±5%)
- [ ] Each MCQ follows MCQ Schema (see mcq-schema.md)

### 10. References

```markdown
## References

- [Organization]. "[Title]." [Version/Edition]. [Year]. [URL]
```

**Validation:**
- [ ] All factual claims have citation
- [ ] Format follows FR-013
- [ ] Minimum 5 references per chapter
- [ ] Sources are authoritative (RFC, ISO, vendor docs, academic)

---

## Metrics Validation

| Metric | Formula | Pass Threshold |
|--------|---------|----------------|
| Page Count | Actual pages | ≥95% of target |
| MCQ Count | Number of MCQs | 100% of target |
| Diagram Count | Number of figures | ≥90% of target |
| Lab Count | Number of labs | 100% of target |
| Example Count | Practical examples | ≥10 |
| Readability | Flesch Reading Ease | 50-60 |

---

## Chapter Targets by Priority

| Priority | Chapters | Page Target | MCQ Target | Lab Target |
|----------|----------|-------------|------------|------------|
| High | 2,3,4,5,9,10,14,19 | 45-55 | 200-250 | 4-6 |
| Medium | 6,7,8,11,12,13,15,16,17,18,20,23,25 | 35-45 | 170-200 | 2-4 |
| Lower | 21,22,24,26 | 30-35 | 150-160 | 2-3 |
| Setup | 1 | 20 | 50 | 0 |
| Assessment | 27,28 | 40-60 | 0* | 0 |
| Reference | 29,30 | 15-20 | 0-50 | 0 |

*Chapters 27-28 organize existing MCQs; no new MCQs created

---

## Validation Checklist

Copy this checklist for each chapter review:

```markdown
## Chapter [N] Validation Checklist

**Chapter**: [Title]
**Author**: [Name]
**Date**: [Date]

### Structure Compliance
- [ ] All 11 required sections present
- [ ] Sections in correct order
- [ ] Section numbering consistent

### Learning Objectives
- [ ] Minimum 4 objectives
- [ ] Bloom's verbs used
- [ ] All difficulty levels represented
- [ ] Objectives are measurable

### Content Quality
- [ ] Difficulty progression B → I → A → E
- [ ] Minimum 10 practical examples
- [ ] No placeholder content
- [ ] Jargon explained on first use

### Labs (if applicable)
- [ ] Minimum 3 labs
- [ ] All labs follow schema
- [ ] Labs independently completable

### MCQs (if applicable)
- [ ] MCQ count meets target
- [ ] Difficulty distribution correct
- [ ] All MCQs follow schema

### References
- [ ] Minimum 5 citations
- [ ] Citation format correct
- [ ] Sources are authoritative

### Metrics
- [ ] Page count: [Actual] / [Target] = [%]
- [ ] MCQ count: [Actual] / [Target] = [%]
- [ ] Diagram count: [Actual] / [Target] = [%]
- [ ] Lab count: [Actual] / [Target] = [%]
- [ ] Flesch score: [Score]

### Result
- [ ] PASS - All validations met
- [ ] FAIL - Issues listed below

**Issues (if FAIL):**
1. [Issue description]
2. [Issue description]
```

---

**Schema Version**: 1.0
**Last Updated**: 2026-01-31
