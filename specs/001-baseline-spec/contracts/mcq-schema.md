# MCQ Schema: Validation Contract

**Purpose**: Define mandatory structure and validation rules for all MCQ questions

---

## MCQ Format

Every MCQ MUST follow this exact format:

```markdown
**Question [Chapter].[Sequence]** [Difficulty: B/I/A/E]

[Question stem - clear, positive phrasing, single concept tested]

A. [Option A]
B. [Option B]
C. [Option C]
D. [Option D]

**Correct Answer**: [A/B/C/D]

**Explanation**:
[Why the correct answer is right - minimum 50 words explaining the concept
and why this answer best addresses the question]

**Why [incorrect option 1] is incorrect**: [Brief explanation]
**Why [incorrect option 2] is incorrect**: [Brief explanation]
**Why [incorrect option 3] is incorrect**: [Brief explanation]

**Reference**: [Source citation per FR-013]
**Related Topic**: Chapter [N], Section [N.X]
```

---

## Field Specifications

### Question ID

**Format**: `[Chapter].[Sequence]`
- Chapter: 2-digit chapter number (02, 03, ... 30)
- Sequence: 3-digit sequential number (001, 002, ... 250)

**Examples**: `02.001`, `02.250`, `10.150`

### Difficulty Level

| Code | Level | Bloom's | Description |
|------|-------|---------|-------------|
| B | Beginner | Remember, Understand | Recall facts, definitions, basic concepts |
| I | Intermediate | Apply | Use knowledge in new situations |
| A | Advanced | Analyze | Break down information, identify patterns |
| E | Expert | Evaluate, Create | Judge, justify, design solutions |

### Question Stem

**MUST:**
- Be a complete question or statement requiring completion
- Test a single concept
- Be positively phrased (what IS correct, not what is NOT)
- Be clear and unambiguous
- Minimum 20 characters

**MUST NOT:**
- Use negative stems ("Which is NOT...", "All EXCEPT...")
- Include trivial distinctions
- Use trick wording
- Reference specific vendor versions that may change
- Require memorization of arbitrary numbers

### Options (A, B, C, D)

**MUST:**
- Have exactly 4 options
- Be grammatically parallel (all same structure)
- Be plausible (based on common misconceptions)
- Be mutually exclusive
- Be consistent in length (no obvious longest answer)

**MUST NOT:**
- Include "All of the above"
- Include "None of the above"
- Include "Both A and B"
- Use absolute terms ("always", "never") unless factually accurate
- Have overlapping meanings

### Correct Answer

- Must be exactly one letter: A, B, C, or D
- Correct answer should be distributed roughly evenly across A/B/C/D across all MCQs

### Explanation (Correct Answer)

**MUST:**
- Be minimum 50 words
- Explain WHY the answer is correct
- Reference the underlying concept
- Provide additional context for learning

**Template:**
```
The correct answer is [X] because [explanation of the concept].
[Additional context about why this is important].
[Connection to real-world application or exam relevance].
```

### Distractor Explanations

For each incorrect option, explain why it's wrong:

**Template:**
```
**Why [X] is incorrect**: [Brief explanation, 15-30 words]
```

**Common distractor types:**
- Partially correct but incomplete
- Correct for a different context
- Common misconception
- Reversed or inverted concept
- Related but distinct term

### Reference

**Format**: `[Organization]. "[Title]." [Version/Edition]. [Year]. [URL if applicable]`

**Examples:**
- `IETF. "RFC 791 - Internet Protocol." 1981.`
- `Microsoft. "Windows Server 2022 Documentation." 2025.`
- `ISO. "ISO/IEC 27001:2022." 2022.`

### Related Topic

**Format**: `Chapter [N], Section [N.X]`

**Example**: `Chapter 2, Section 2.3`

---

## Difficulty Distribution Requirements

Per chapter, MCQs MUST be distributed as follows (±5% tolerance):

| Difficulty | Percentage | Purpose |
|------------|------------|---------|
| Beginner (B) | 25% | Build confidence, verify basics |
| Intermediate (I) | 35% | Core exam content |
| Advanced (A) | 30% | Differentiate strong candidates |
| Expert (E) | 10% | Challenge top performers |

**Example for 250 MCQ chapter:**
- B: 63 questions (25%)
- I: 88 questions (35%)
- A: 75 questions (30%)
- E: 24 questions (10%)

---

## Quality Criteria

### MUST Include (per FR-010, FR-016-019)

- [ ] Clear, unambiguous question stem
- [ ] Single concept tested per question
- [ ] All options grammatically parallel
- [ ] Plausible distractors based on common misconceptions
- [ ] Explanation for correct answer (minimum 50 words)
- [ ] Explanation for why each distractor is wrong
- [ ] Difficulty level indicator (B/I/A/E)
- [ ] Source reference for verification
- [ ] Related topic reference

### MUST Avoid (per FR-019)

- [ ] Negative stems ("Which is NOT correct...")
- [ ] "All of the above" / "None of the above"
- [ ] Absolute terms ("always", "never") unless factually accurate
- [ ] Trivial distinctions or trick questions
- [ ] Implementation-specific details that vary by version
- [ ] Questions requiring memorization of arbitrary numbers
- [ ] Ambiguous or vague wording
- [ ] Cultural or regional bias

---

## MCQ Examples

### Good Example (Intermediate)

```markdown
**Question 02.015** [Difficulty: I]

Which protocol operates at the Transport Layer and provides reliable,
connection-oriented data delivery?

A. UDP
B. TCP
C. IP
D. ICMP

**Correct Answer**: B

**Explanation**:
TCP (Transmission Control Protocol) operates at the Transport Layer (Layer 4)
of the OSI model and provides reliable, connection-oriented data delivery. It
establishes a connection using a three-way handshake before data transfer and
ensures data integrity through acknowledgments, sequencing, and retransmission
of lost packets. TCP is essential for applications requiring guaranteed delivery
such as web browsing, email, and file transfers.

**Why A is incorrect**: UDP is connectionless and does not guarantee delivery.
**Why C is incorrect**: IP operates at the Network Layer (Layer 3), not Transport.
**Why D is incorrect**: ICMP is a Network Layer protocol used for diagnostics.

**Reference**: IETF. "RFC 793 - Transmission Control Protocol." 1981.
**Related Topic**: Chapter 2, Section 2.4
```

### Bad Example (What NOT to do)

```markdown
❌ **Question 02.015** [Difficulty: I]

Which of the following is NOT a characteristic of TCP?

A. Connection-oriented
B. Reliable delivery
C. Fast transmission
D. Flow control

**Correct Answer**: C

**Explanation**:
TCP is not fast.

❌ Issues:
- Negative stem ("NOT")
- "Fast" is subjective and ambiguous
- Explanation too short (<50 words)
- No distractor explanations
- No reference
- No related topic
```

---

## Validation Checklist

For each MCQ, verify:

```markdown
## MCQ Validation: Question [Chapter].[Sequence]

### Format
- [ ] ID format correct ([Chapter].[Sequence])
- [ ] Difficulty indicator present (B/I/A/E)
- [ ] Exactly 4 options (A-D)
- [ ] Single correct answer indicated

### Stem Quality
- [ ] Positive phrasing (no "NOT", "EXCEPT")
- [ ] Single concept tested
- [ ] Clear and unambiguous
- [ ] Minimum 20 characters

### Options Quality
- [ ] Grammatically parallel
- [ ] Plausible distractors
- [ ] No "All/None of the above"
- [ ] No absolute terms misused

### Explanations
- [ ] Correct answer explanation ≥50 words
- [ ] All 3 distractors explained
- [ ] Explanations are educational

### References
- [ ] Source citation present
- [ ] Citation format correct
- [ ] Related topic specified

### Result
- [ ] PASS
- [ ] FAIL - [Reason]
```

---

**Schema Version**: 1.0
**Last Updated**: 2026-01-31
