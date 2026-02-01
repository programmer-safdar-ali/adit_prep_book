# Quickstart Guide: Content Development

**Feature**: 001-baseline-spec
**Date**: 2026-01-31
**Purpose**: Get started creating chapter content for the ADIT Preparation Guide

---

## Overview

This guide walks you through creating your first chapter using the standardized templates and processes defined in the baseline specification.

---

## Prerequisites

Before starting:

1. **Read the Constitution**: `.specify/memory/constitution.md` - understand the 13 core principles
2. **Review the Specification**: `specs/001-baseline-spec/spec.md` - understand requirements
3. **Access Templates**: `book/templates/` - chapter, MCQ, lab templates
4. **Setup Tools**:
   - Markdown editor (VS Code recommended)
   - Diagramming tool (draw.io, Mermaid)
   - Readability analyzer (Hemingway Editor or hemingwayapp.com)

---

## Content Development Workflow

### Phase 1: Setup (Day 0)

```bash
# 1. Navigate to chapters directory
cd book/chapters/

# 2. Create chapter directory
mkdir 02-networking
cd 02-networking

# 3. Copy templates
cp ../../templates/chapter-template.md content.md
cp ../../templates/mcq-template.md mcqs.md
mkdir labs assets
```

### Phase 2: Outline (Days 1-2)

1. **Open `content.md`** and fill in Chapter Overview:
   ```markdown
   ## Chapter Overview

   - **Domain**: Core Networking Fundamentals
   - **Estimated Study Time**: 5-6 hours
   - **Prerequisites**: Chapter 1 (Introduction), Basic computer literacy
   - **Difficulty Progression**: Beginner → Intermediate → Advanced → Expert
   ```

2. **Define Learning Objectives** (minimum 4):
   ```markdown
   ## Learning Objectives

   By the end of this chapter, you will be able to:
   1. Define the OSI and TCP/IP models and explain each layer's function (B)
   2. Implement subnetting calculations for IPv4 networks (I)
   3. Analyze network traffic to identify protocols and troubleshoot issues (A)
   4. Design a multi-site enterprise network topology (E)
   ```

3. **Create Section Outline**:
   ```markdown
   ## Section 2.1: Network Models and Architecture (B)
   ## Section 2.2: IP Addressing and Subnetting (I)
   ## Section 2.3: Network Devices and Topologies (I)
   ## Section 2.4: Network Protocols (A)
   ## Section 2.5: Enterprise Network Design (E)
   ```

4. **List Labs** (minimum 3):
   - Lab 2.1: Subnetting Exercise
   - Lab 2.2: Configure VLANs
   - Lab 2.3: Packet Analysis with Wireshark

5. **List Diagrams** (target: 25):
   - OSI Model, TCP/IP Stack, Subnet Masks, VLAN Architecture, etc.

6. **Submit Outline for Approval**

### Phase 3: Draft (Days 3-12)

#### Writing Content

For each section, follow this pattern:

```markdown
## Section 2.1: Network Models and Architecture (B)

[Introduction paragraph explaining the section topic and its importance]

### 2.1.1 The OSI Model

The Open Systems Interconnection (OSI) model is a conceptual framework...

[Detailed content explaining the concept]

### Practical Example 2.1: Tracing a Web Request Through OSI Layers

When you enter a URL in your browser, the request travels through all seven
OSI layers. Here's how it works:

1. **Application Layer (Layer 7)**: Browser generates HTTP request...
[Continue through all layers]

This example demonstrates how...
```

#### Writing MCQs

For each section, create MCQs following the schema:

```markdown
**Question 02.001** [Difficulty: B]

Which OSI layer is responsible for routing packets between networks?

A. Data Link Layer
B. Transport Layer
C. Network Layer
D. Session Layer

**Correct Answer**: C

**Explanation**:
The Network Layer (Layer 3) is responsible for routing packets between
different networks. It determines the best path for data to travel from
source to destination using logical addressing (IP addresses) and routing
protocols. Routers operate at this layer, making decisions based on
destination addresses and routing tables.

**Why A is incorrect**: Data Link Layer handles node-to-node delivery, not routing.
**Why B is incorrect**: Transport Layer handles end-to-end delivery, not routing.
**Why D is incorrect**: Session Layer manages sessions, not network routing.

**Reference**: IETF. "RFC 791 - Internet Protocol." 1981.
**Related Topic**: Chapter 2, Section 2.1
```

#### Creating Labs

Use the lab template for each hands-on exercise:

```markdown
## Hands-on Lab 2.1: IPv4 Subnetting Exercise

**Objective**: Calculate subnet masks, network addresses, and host ranges

**Time Required**: 30-45 minutes

**Prerequisites**:
- Completed Section 2.2: IP Addressing
- Understanding of binary-decimal conversion

**Environment**:
- Calculator (physical or Windows Calculator in Programmer mode)
- Pen and paper for working

### Steps:

1. **Given Network**: 192.168.10.0/24, create 4 equal subnets

   *Calculate*: New subnet mask
   *Expected Result*: /26 (255.255.255.192)

2. **List the four subnet ranges**

   *Expected Result*:
   - Subnet 1: 192.168.10.0 - 192.168.10.63
   - Subnet 2: 192.168.10.64 - 192.168.10.127
   - Subnet 3: 192.168.10.128 - 192.168.10.191
   - Subnet 4: 192.168.10.192 - 192.168.10.255

[Continue with more steps...]

### Validation Checklist:
- [ ] Calculated correct subnet mask (/26)
- [ ] Identified all 4 subnet ranges correctly
- [ ] Determined correct broadcast address for each subnet
- [ ] Calculated usable host range for each subnet

### Troubleshooting:

| Issue | Possible Cause | Solution |
|-------|---------------|----------|
| Wrong subnet count | Incorrect bit calculation | Review powers of 2 |
| Wrong host range | Forgot network/broadcast | First and last IPs are reserved |
```

#### Creating Diagrams

1. Create diagrams in `assets/` directory
2. Use consistent naming: `figure-02-01-osi-model.svg`
3. Include in content:
   ```markdown
   ![Figure 2.1 - OSI Model Seven Layers](assets/figure-02-01-osi-model.svg)

   *Figure 2.1 - OSI Model Seven Layers showing protocols at each level*
   ```

### Phase 4: Self-Review (Day 13)

Before submitting, verify:

1. **Run Readability Check**:
   - Paste content into Hemingway Editor
   - Target: Grade 10-12 (Flesch 50-60)
   - Fix highlighted sentences

2. **Count Metrics**:
   - Pages: Use word count (≈300 words/page)
   - MCQs: Count in mcqs.md
   - Diagrams: Count in assets/
   - Labs: Count in labs/

3. **Verify Structure**:
   - All 11 sections present
   - Learning objectives use Bloom's verbs
   - Difficulty progresses B→I→A→E
   - Examples ≥ 10

4. **Check MCQs**:
   - Difficulty distribution: 25/35/30/10
   - All explanations ≥50 words
   - All distractors explained
   - References present

### Phase 5: Submit for Review (Day 14+)

1. **Create Pull Request** or submit chapter directory
2. **Notify Technical Reviewer**
3. **Await Technical Review** (2-3 days)
4. **Address Feedback** (Revision phase)
5. **Await Editorial Review** (1-2 days)
6. **Address Feedback** (if any)
7. **Quality Gate** (1 day)
8. **Approved!**

---

## Quick Reference: Targets by Chapter Priority

| Priority | Pages | MCQs | Labs | Diagrams | Examples |
|----------|-------|------|------|----------|----------|
| High (Ch 2,3,9,10) | 50-60 | 250 | 5-6 | 20-25 | 12-15 |
| Medium | 35-45 | 170-200 | 3-4 | 15-20 | 10-12 |
| Lower | 30-35 | 150-160 | 2-3 | 10-15 | 10 |

---

## Quick Reference: Difficulty Indicators

| Code | Level | Bloom's Verbs | MCQ % |
|------|-------|---------------|-------|
| B | Beginner | Define, describe, identify, list | 25% |
| I | Intermediate | Apply, calculate, demonstrate, implement | 35% |
| A | Advanced | Analyze, compare, troubleshoot, differentiate | 30% |
| E | Expert | Design, evaluate, propose, recommend | 10% |

---

## Common Mistakes to Avoid

1. **MCQs**: Using negative stems ("Which is NOT...")
2. **Content**: Skipping difficulty progression
3. **Labs**: Missing validation checkpoints
4. **Diagrams**: No legends for symbols
5. **Citations**: Missing source references
6. **Examples**: Less than 10 per chapter

---

## Getting Help

- **Template Issues**: Check `contracts/` schemas
- **Content Questions**: Review `research.md`
- **Process Questions**: Check this quickstart
- **Technical Questions**: Consult domain SME

---

## Checklist: Ready to Submit?

- [ ] All 11 sections complete
- [ ] Learning objectives use Bloom's verbs
- [ ] Content progresses B→I→A→E
- [ ] Minimum 10 examples
- [ ] Labs have all 5 components
- [ ] MCQs meet count target
- [ ] MCQ difficulty distribution correct
- [ ] All MCQs have full explanations
- [ ] Diagrams labeled correctly
- [ ] Readability score 50-60
- [ ] All references present
- [ ] No TODO/placeholder content

**If all boxes checked: Submit for Technical Review!**

---

**Guide Version**: 1.0
**Last Updated**: 2026-01-31
