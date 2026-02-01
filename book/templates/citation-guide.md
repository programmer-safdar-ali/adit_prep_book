# Citation Format Reference Guide

**Purpose**: Ensure consistent, authoritative sourcing across all ADIT Preparation Guide content

---

## Standard Citation Format

```
[Organization/Author]. "[Title]." [Version/Edition]. [Year]. [URL if applicable]
```

---

## Citation Examples by Source Type

### 1. RFC/IETF Standards (Highest Authority)

```markdown
IETF. "RFC 791 - Internet Protocol." 1981. https://tools.ietf.org/html/rfc791
IETF. "RFC 793 - Transmission Control Protocol." 1981. https://tools.ietf.org/html/rfc793
IETF. "RFC 2616 - HTTP/1.1." 1999. https://tools.ietf.org/html/rfc2616
IETF. "RFC 5246 - TLS 1.2." 2008. https://tools.ietf.org/html/rfc5246
```

### 2. ISO/IEC Standards

```markdown
ISO. "ISO/IEC 27001:2022 - Information Security Management." 2022.
ISO. "ISO/IEC 27002:2022 - Information Security Controls." 2022.
ISO. "ISO 9001:2015 - Quality Management Systems." 2015.
IEEE. "IEEE 802.11-2020 - Wireless LAN." 2020.
```

### 3. Vendor Official Documentation

```markdown
Microsoft. "Windows Server 2022 Documentation." 2025. https://docs.microsoft.com/windows-server
Cisco. "Cisco IOS Configuration Guide." Version 17.x. 2024. https://www.cisco.com/c/en/us/support
Amazon Web Services. "AWS Well-Architected Framework." 2025. https://aws.amazon.com/architecture/well-architected
Google Cloud. "Google Cloud Architecture Framework." 2025. https://cloud.google.com/architecture/framework
```

### 4. Industry Frameworks

```markdown
ISACA. "COBIT 2019 Framework." 2019. https://www.isaca.org/cobit
AXELOS. "ITIL 4 Foundation." 2019. https://www.axelos.com/itil
PMI. "PMBOK Guide." 7th Edition. 2021.
NIST. "Cybersecurity Framework." Version 1.1. 2018. https://www.nist.gov/cyberframework
```

### 5. Academic Textbooks

```markdown
Tanenbaum, Andrew S. "Computer Networks." 6th Edition. 2021.
Stallings, William. "Cryptography and Network Security." 8th Edition. 2022.
Kurose, James F. and Ross, Keith W. "Computer Networking: A Top-Down Approach." 8th Edition. 2020.
```

### 6. NIST Special Publications

```markdown
NIST. "SP 800-53 Rev. 5 - Security and Privacy Controls." 2020. https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final
NIST. "SP 800-171 Rev. 2 - Protecting CUI." 2020. https://csrc.nist.gov/publications/detail/sp/800-171/rev-2/final
NIST. "SP 800-37 Rev. 2 - Risk Management Framework." 2018. https://csrc.nist.gov/publications/detail/sp/800-37/rev-2/final
```

### 7. Government/Regulatory

```markdown
CISA. "Cybersecurity Best Practices." 2024. https://www.cisa.gov/cybersecurity-best-practices
GDPR. "General Data Protection Regulation." 2018. https://gdpr-info.eu
PCI SSC. "PCI DSS v4.0." 2022. https://www.pcisecuritystandards.org
```

---

## Source Priority Order

When multiple sources are available, prefer in this order:

| Priority | Source Type | When to Use |
|----------|-------------|-------------|
| 1 | RFC/ISO/IEEE Standards | Protocol specifications, technical standards |
| 2 | NIST Publications | Security controls, best practices, frameworks |
| 3 | Vendor Official Documentation | Product-specific features, configurations |
| 4 | Industry Frameworks | Governance, processes, methodologies |
| 5 | Academic Textbooks | Theoretical concepts, foundational knowledge |
| 6 | Industry Best Practice Guides | Implementation guidance, practical approaches |

---

## Citation Requirements

### Per Chapter
- **Minimum**: 5 references
- **Recommended**: 10-15 references for domain chapters

### Per Major Claim
- **Requirement**: 2+ authoritative sources (FR-011)
- **Exception**: Well-established facts (e.g., "TCP uses 3-way handshake")

### For MCQs
- **Requirement**: 1 source reference per MCQ
- **Format**: Abbreviated citation in MCQ Reference field

---

## In-Text Citation Style

### For Statements
```markdown
According to RFC 793, TCP establishes connections using a three-way handshake.
```

### For Figures/Diagrams
```markdown
*Figure 2.3 - OSI Model Layers. Adapted from ISO/IEC 7498-1.*
```

### For Tables
```markdown
*Table 2.1 - Common Port Numbers. Source: IANA Service Name Registry.*
```

---

## Currency Guidelines

| Content Type | Maximum Age | Notes |
|--------------|-------------|-------|
| Standards (RFC, ISO) | No limit | Standards remain valid until superseded |
| Vendor Docs | 2 versions | Must be within 2 major versions of current |
| Security/Compliance | 3 years | Must reflect current threat landscape |
| Textbooks | 5 years | Unless concepts unchanged |
| Technology Products | 2 years | Fast-changing; mark with "As of [date]" |

---

## "As of [Date]" Markers

For rapidly changing content, include currency markers:

```markdown
As of January 2026, Windows Server 2022 supports the following encryption algorithms...

Note: Cloud service pricing and features change frequently. Verify current
offerings at the vendor's official documentation.
```

---

## Common Errors to Avoid

| Error | Correct Approach |
|-------|------------------|
| Wikipedia as primary source | Use Wikipedia only for discovery; cite original sources |
| Broken URLs | Test all URLs before submission |
| Outdated vendor docs | Verify version currency |
| Missing publication year | Always include year |
| Citing opinion blogs | Use official documentation or standards |
| Single source for major claims | Provide 2+ independent sources |

---

## Reference Section Template

```markdown
## References

### Standards and Specifications
- IETF. "RFC [Number] - [Title]." [Year]. [URL]
- ISO. "[Standard Number] - [Title]." [Year].

### Vendor Documentation
- [Vendor]. "[Documentation Title]." [Version/Year]. [URL]

### Industry Frameworks
- [Organization]. "[Framework Name]." [Edition]. [Year]. [URL]

### Academic Sources
- [Author Last, First]. "[Book Title]." [Edition]. [Year].
```

---

**Guide Version**: 1.0
**Last Updated**: 2026-02-01
