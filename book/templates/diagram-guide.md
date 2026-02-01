# Diagram Labeling Convention Guide

**Purpose**: Ensure consistent, professional visual elements across all ADIT Preparation Guide content

---

## Figure Numbering Format

```
Figure [Chapter].[Sequence] - [Descriptive Title]
```

### Examples
- Figure 2.1 - OSI Model Seven Layers
- Figure 2.3 - TCP Three-Way Handshake Process
- Figure 9.15 - Cloud Service Models Comparison (IaaS, PaaS, SaaS)

---

## Diagram Types

| Type | Use For | Example |
|------|---------|---------|
| Flowchart | Processes, decision trees | Network troubleshooting flow |
| Architecture | System layouts, components | Enterprise network topology |
| Comparison | Side-by-side analysis | OSI vs TCP/IP model |
| Process | Step-by-step sequences | DHCP lease process |
| Topology | Network layouts | Star, mesh, ring topologies |
| Table/Matrix | Structured data comparison | Port numbers reference |
| Infographic | Summary/overview | Chapter concept map |

---

## File Naming Convention

```
figure-[chapter]-[sequence]-[slug].svg
```

### Examples
- `figure-02-01-osi-model.svg`
- `figure-02-03-tcpip-handshake.svg`
- `figure-09-15-cloud-service-models.svg`

---

## Required Elements

### Every Diagram MUST Have

1. **Figure Number**: `Figure [Ch].[Seq]` format
2. **Descriptive Title**: Clear, specific (10-100 chars)
3. **Caption** (if needed): Additional context below diagram

### Conditional Requirements

| Condition | Requirement |
|-----------|-------------|
| Uses symbols/colors | Legend REQUIRED |
| Adapted from source | Source citation REQUIRED |
| Contains abbreviations | Define in legend or caption |

---

## Legend Format

When a diagram uses symbols, colors, or abbreviations, include a legend:

```
Legend:
├── Blue boxes: Network devices
├── Green arrows: Data flow
├── Red dashed lines: Firewall boundaries
└── Yellow cylinders: Databases
```

### Legend Placement
- **Preferred**: Below diagram, within figure boundary
- **Alternative**: Right side of diagram if space permits
- **Never**: Separate from diagram

---

## Technical Specifications

### File Formats

| Format | Use Case | Notes |
|--------|----------|-------|
| SVG | Primary (preferred) | Scalable, editable |
| PNG | Fallback | Minimum 300 DPI |
| draw.io | Source files | Keep in separate folder |

### Dimensions

| Property | Requirement |
|----------|-------------|
| Maximum Width | 6 inches (single column) |
| Minimum Resolution | 300 DPI (for print) |
| Text Size | Minimum 10pt equivalent |

### Color Guidelines

| Purpose | Recommended Color |
|---------|-------------------|
| Primary elements | Blue (#0066CC) |
| Data flow | Green (#28A745) |
| Security/Warning | Red (#DC3545) |
| Neutral/Background | Gray (#6C757D) |
| Highlight/Emphasis | Yellow (#FFC107) |

---

## In-Content Reference Format

### Standard Reference
```markdown
As shown in Figure 2.3, the TCP three-way handshake involves...

![Figure 2.3 - TCP Three-Way Handshake](assets/figure-02-03-tcp-handshake.svg)

*Figure 2.3 - TCP Three-Way Handshake showing SYN, SYN-ACK, and ACK packets*
```

### Cross-Chapter Reference
```markdown
Refer to Figure 3.5 in Chapter 3 for the firewall placement diagram.
```

---

## Accessibility Requirements

1. **Alt Text**: Every diagram needs descriptive alt text
2. **Text Contrast**: Minimum 4.5:1 ratio
3. **Color Independence**: Don't rely solely on color to convey meaning
4. **Screen Reader**: Key content should be in caption/alt text

### Alt Text Example
```markdown
![Figure 2.1 - OSI Model showing seven layers from Physical (Layer 1)
at bottom to Application (Layer 7) at top, with protocols at each layer](...)
```

---

## Diagram Checklist

Before submitting a diagram, verify:

- [ ] Figure number follows `[Chapter].[Sequence]` format
- [ ] Title is descriptive and 10-100 characters
- [ ] Legend present if symbols/colors used
- [ ] All text readable at 100% zoom
- [ ] Resolution ≥300 DPI (for raster images)
- [ ] Source cited if adapted from another work
- [ ] Alt text provided for accessibility
- [ ] Filename follows convention
- [ ] File saved in chapter's `assets/` directory

---

## Common Diagram Examples

### Network Topology

```
Figure 2.5 - Star Network Topology

       [Switch]
      /   |   \
     /    |    \
   [PC1] [PC2] [PC3]

Legend:
- Rectangle: Network device
- Lines: Ethernet connections
```

### Process Flow

```
Figure 2.8 - DHCP Lease Process

[Client] --DISCOVER--> [Server]
[Client] <--OFFER---- [Server]
[Client] --REQUEST--> [Server]
[Client] <--ACK------ [Server]

Legend:
- Solid arrows: Client to Server
- Dashed arrows: Server to Client
```

### Comparison Diagram

```
Figure 2.2 - OSI vs TCP/IP Model Comparison

    OSI Model          TCP/IP Model
┌───────────────┐    ┌───────────────┐
│ Application   │    │               │
├───────────────┤    │  Application  │
│ Presentation  │    │               │
├───────────────┤    ├───────────────┤
│ Session       │    │               │
├───────────────┤    │   Transport   │
│ Transport     │    │               │
├───────────────┤    ├───────────────┤
│ Network       │    │   Internet    │
├───────────────┤    ├───────────────┤
│ Data Link     │    │               │
├───────────────┤    │ Network Access│
│ Physical      │    │               │
└───────────────┘    └───────────────┘
```

---

## Tools Recommended

| Tool | Best For | Format Output |
|------|----------|---------------|
| draw.io | Architecture, flowcharts | SVG, PNG |
| Mermaid | Inline diagrams in markdown | SVG |
| Lucidchart | Complex diagrams | SVG, PNG |
| Microsoft Visio | Enterprise diagrams | SVG, PNG |
| PlantUML | Technical/UML diagrams | SVG, PNG |

---

## Version Control

- Keep source files (`.drawio`, `.plantuml`) in separate `source/` folder
- Export final SVG/PNG to chapter `assets/` folder
- Include version in filename for major revisions: `figure-02-01-osi-model-v2.svg`

---

**Guide Version**: 1.0
**Last Updated**: 2026-02-01
