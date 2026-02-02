# Chapter 12: IT Governance & Policy Development

## Overview

IT Governance establishes the framework through which organizations ensure that IT investments support business objectives, resources are used responsibly, and risks are appropriately managed. For Assistant Directors IT in public service, mastering IT governance is crucial as government agencies must demonstrate accountability, transparency, and compliance while delivering efficient IT services. This chapter covers ITIL v4 practices, IT policy development, governance frameworks like COBIT, service management, change management, and the critical aspects of vendor and financial management in public sector IT.

## Learning Objectives

After completing this chapter, you will be able to:

- Apply ITIL v4 Service Value System concepts to IT service delivery
- Develop and implement IT policies appropriate for government organizations
- Utilize COBIT 2019 for IT governance and management
- Design effective Service Level Agreements (SLAs) and measure performance
- Implement change management processes that balance agility with control
- Manage IT risks through structured assessment and mitigation
- Oversee vendor relationships and IT financial management

---

## 12.1 ITIL Framework v4

### Introduction to ITIL v4

**ITIL (Information Technology Infrastructure Library)** is the most widely adopted framework for IT Service Management (ITSM). ITIL v4, released in 2019, evolved from process-based to a holistic approach emphasizing value co-creation.

### Service Value System (SVS)

The SVS represents how organizational components work together to enable value creation.

**SVS Components**:
```
                    ┌─────────────────────────────┐
                    │     Guiding Principles      │
                    └─────────────────────────────┘
                                  │
┌──────────┐    ┌─────────────────────────────────────┐    ┌─────────┐
│          │    │                                     │    │         │
│ Demand / │───►│        SERVICE VALUE CHAIN          │───►│  Value  │
│Opportunity│    │                                     │    │         │
│          │    └─────────────────────────────────────┘    └─────────┘
└──────────┘              │              │
                         │              │
              ┌──────────▼──────────────▼──────────┐
              │         ITIL Practices            │
              └───────────────────────────────────┘
                         │              │
              ┌──────────▼──────────────▼──────────┐
              │       Governance                   │
              └───────────────────────────────────┘
                                  │
              ┌───────────────────▼───────────────┐
              │    Continual Improvement          │
              └───────────────────────────────────┘
```

### ITIL Guiding Principles

| Principle | Description | Application |
|-----------|-------------|-------------|
| Focus on value | Everything should link to stakeholder value | Justify IT investments by business outcomes |
| Start where you are | Assess current state before changes | Don't start from scratch unnecessarily |
| Progress iteratively | Make small, manageable improvements | Agile approach to service improvement |
| Collaborate | Work across boundaries | Break down silos between teams |
| Think holistically | Consider entire system | Understand dependencies and impacts |
| Keep it simple | Avoid unnecessary complexity | Minimum viable solutions |
| Optimize and automate | Maximize efficiency | Automate repetitive tasks |

### Four Dimensions of Service Management

**1. Organizations and People**:
- Organizational structure and culture
- Roles, responsibilities, and authorities
- Skills and competencies
- Communication and collaboration

**2. Information and Technology**:
- Information for service management
- Technologies supporting services
- Knowledge management
- Automation tools

**3. Partners and Suppliers**:
- Supplier relationships and contracts
- Outsourcing arrangements
- Integration with external parties
- Service integration

**4. Value Streams and Processes**:
- Activities that create value
- Process workflows
- Procedures and work instructions
- Automation of activities

### ITIL Practices Overview

ITIL v4 defines 34 practices organized into three categories:

#### General Management Practices
| Practice | Purpose |
|----------|---------|
| Architecture management | Understand organizational elements and relationships |
| Continual improvement | Align practices with changing business needs |
| Information security management | Protect information |
| Knowledge management | Share and utilize knowledge |
| Measurement and reporting | Support decision-making with data |
| Organizational change management | Manage human aspects of change |
| Portfolio management | Ensure optimal resource allocation |
| Project management | Deliver projects successfully |
| Relationship management | Establish stakeholder relationships |
| Risk management | Identify and address risks |
| Service financial management | Manage IT budgets and accounting |
| Strategy management | Define organizational direction |
| Supplier management | Manage supplier relationships |
| Workforce and talent management | Ensure skilled personnel |

#### Service Management Practices
| Practice | Purpose |
|----------|---------|
| Availability management | Ensure services meet availability needs |
| Business analysis | Analyze business needs |
| Capacity and performance management | Ensure service performance |
| Change enablement | Maximize successful changes |
| Incident management | Restore normal service quickly |
| IT asset management | Manage asset lifecycle |
| Monitoring and event management | Observe services and components |
| Problem management | Reduce incident likelihood and impact |
| Release management | Make services available for use |
| Service catalogue management | Provide service information |
| Service configuration management | Manage configuration information |
| Service continuity management | Ensure service availability in disasters |
| Service design | Design fit-for-purpose services |
| Service desk | Capture demand for services |
| Service level management | Set and manage service levels |
| Service request management | Handle service requests |
| Service validation and testing | Ensure services meet requirements |

#### Technical Management Practices
| Practice | Purpose |
|----------|---------|
| Deployment management | Move components to live environments |
| Infrastructure and platform management | Oversee infrastructure |
| Software development and management | Build and maintain applications |

### Key ITIL Practices in Detail

#### Incident Management

**Objective**: Restore normal service operation as quickly as possible.

**Incident Lifecycle**:
```
[Detection] → [Logging] → [Categorization] → [Prioritization]
      ↓
[Initial Diagnosis] → [Escalation (if needed)] → [Investigation]
      ↓
[Resolution] → [Recovery] → [Closure]
```

**Priority Matrix**:
| Impact | Urgency: High | Urgency: Medium | Urgency: Low |
|--------|---------------|-----------------|--------------|
| High | P1 - Critical | P2 - High | P3 - Medium |
| Medium | P2 - High | P3 - Medium | P4 - Low |
| Low | P3 - Medium | P4 - Low | P5 - Planning |

**Major Incident Management**:
- Separate process for high-impact incidents
- Dedicated major incident manager
- Frequent stakeholder communication
- Post-incident review mandatory

#### Problem Management

**Objective**: Reduce likelihood and impact of incidents by identifying root causes.

**Key Concepts**:
- **Problem**: Cause of one or more incidents
- **Known Error**: Problem with documented root cause and workaround
- **KEDB (Known Error Database)**: Repository of known errors

**Problem Analysis Techniques**:
1. **5 Whys**: Repeatedly asking "Why?" to reach root cause
2. **Fishbone Diagram**: Categorizing potential causes
3. **Fault Tree Analysis**: Logical diagram of failures
4. **Pareto Analysis**: Focusing on most significant causes

#### Change Enablement

**Objective**: Maximize successful IT changes by assessing risks and impacts.

**Change Types**:
| Type | Description | Approval |
|------|-------------|----------|
| Standard | Pre-approved, low-risk, routine | Pre-authorized |
| Normal | Requires assessment and approval | CAB or delegated |
| Emergency | Must be implemented immediately | Emergency CAB |

**Change Advisory Board (CAB)**:
- Reviews and approves normal changes
- Assesses risk and impact
- Membership: IT representatives, business stakeholders
- Meeting frequency: Weekly or as needed

**Emergency CAB (ECAB)**:
- Subset of CAB for urgent decisions
- Available 24/7 for emergency changes
- Streamlined approval process

#### Service Level Management

**Objective**: Ensure services meet agreed performance levels.

**Key Documents**:
| Document | Parties | Purpose |
|----------|---------|---------|
| SLA | IT and Customer | Service commitments |
| OLA | IT teams internally | Internal support agreements |
| Underpinning Contract | IT and Vendor | External supplier commitments |

**SLA Components**:
```
1. Service Description
2. Service Hours
3. Availability Targets
4. Performance Metrics
5. Support Response Times
6. Escalation Procedures
7. Service Credits/Penalties
8. Review Process
```

---

## 12.2 IT Policies

### Policy Development Framework

**Policy Hierarchy**:
```
              ┌─────────────┐
              │   Policy    │  ← What must be done
              └──────┬──────┘
                     │
              ┌──────▼──────┐
              │  Standards  │  ← Mandatory requirements
              └──────┬──────┘
                     │
              ┌──────▼──────┐
              │ Guidelines  │  ← Recommended practices
              └──────┬──────┘
                     │
              ┌──────▼──────┐
              │ Procedures  │  ← How to do it
              └─────────────┘
```

### Essential IT Policies

#### Acceptable Use Policy (AUP)

**Purpose**: Define acceptable and prohibited uses of IT resources.

**Key Elements**:
- Authorized use of systems and data
- Personal use limitations
- Prohibited activities (illegal content, harassment)
- Monitoring and privacy expectations
- Consequences of violations

**Government Considerations**:
- Use of public resources
- Political activities restrictions
- Records retention requirements
- Public information responsibilities

#### Password Policy

**Components**:
| Requirement | Standard | Enhanced |
|-------------|----------|----------|
| Minimum Length | 8 characters | 12 characters |
| Complexity | 3 of 4 types | 4 of 4 types |
| Expiration | 90 days | 60 days |
| History | Last 10 | Last 24 |
| Lockout | 5 attempts | 3 attempts |
| MFA Required | Privileged accounts | All accounts |

#### Data Classification Policy

**Classification Levels** (Government):
| Level | Description | Examples |
|-------|-------------|----------|
| Top Secret | Grave damage to national security | Military operations |
| Secret | Serious damage if disclosed | Intelligence data |
| Confidential | Damage if disclosed | Internal memos |
| Restricted | Limited distribution | Personnel records |
| Public | Available to all | Press releases |

**Handling Requirements by Classification**:
- Storage requirements
- Transmission encryption
- Access controls
- Disposal methods
- Breach notification

#### Incident Response Policy

**Key Components**:
1. Incident classification and severity levels
2. Reporting procedures and timelines
3. Response team structure and contacts
4. Communication protocols
5. Evidence preservation requirements
6. Recovery procedures
7. Post-incident review process

#### Access Control Policy

**Principles**:
- Least privilege: Minimum access necessary
- Need to know: Access based on job requirements
- Separation of duties: Critical functions divided
- Regular access reviews: Periodic validation

**Access Types**:
| Access Type | Description | Approval |
|-------------|-------------|----------|
| User | Standard system access | Manager |
| Privileged | Administrative rights | IT Director |
| Emergency | Temporary elevated access | CISO |
| Service | Application accounts | System owner |

#### Remote Access Policy

**Requirements**:
- VPN mandatory for network access
- MFA required for all remote connections
- Approved devices only
- Encryption requirements
- Session timeout limits
- Geographic restrictions (if applicable)

#### BYOD Policy

**Bring Your Own Device Considerations**:
| Aspect | Corporate Approach |
|--------|-------------------|
| Device Types | Approved list of devices |
| Security Requirements | MDM enrollment, encryption |
| Data Separation | Containerization |
| Support | Limited to corporate apps |
| Liability | User responsible for device |
| Exit Process | Remote wipe of corporate data |

---

## 12.3 Governance Frameworks

### COBIT 2019

**COBIT (Control Objectives for Information and Related Technologies)** provides a comprehensive framework for IT governance and management.

**COBIT Principles**:
1. **Meeting Stakeholder Needs**: Governance system satisfies stakeholder needs
2. **Covering the Enterprise End-to-End**: Governance covers all functions
3. **Applying a Single Integrated Framework**: Aligns with other standards
4. **Enabling a Holistic Approach**: Considers all components
5. **Separating Governance from Management**: Clear distinction

**Governance vs. Management**:
| Governance | Management |
|------------|------------|
| Evaluate, Direct, Monitor | Plan, Build, Run, Monitor |
| Setting direction | Achieving objectives |
| Board/Executive level | Operational level |
| Strategic focus | Tactical focus |

**COBIT Goals Cascade**:
```
Stakeholder Needs
       ↓
Enterprise Goals
       ↓
Alignment Goals
       ↓
Governance and Management Objectives
```

**COBIT Governance Objectives**:
| Domain | Code | Objectives |
|--------|------|------------|
| Evaluate, Direct, Monitor | EDM01 | Ensured Governance Framework |
| | EDM02 | Ensured Benefits Delivery |
| | EDM03 | Ensured Risk Optimization |
| | EDM04 | Ensured Resource Optimization |
| | EDM05 | Ensured Stakeholder Engagement |

**COBIT Management Objectives**:
| Domain | Focus |
|--------|-------|
| APO - Align, Plan, Organize | Strategy, architecture, innovation |
| BAI - Build, Acquire, Implement | Requirements, solutions, changes |
| DSS - Deliver, Service, Support | Operations, requests, problems |
| MEA - Monitor, Evaluate, Assess | Performance, compliance, assurance |

### ISO 38500 - IT Governance

**Principles**:
1. **Responsibility**: Clear understanding of responsibilities
2. **Strategy**: IT strategy aligned with business strategy
3. **Acquisition**: IT acquisitions are valid and justified
4. **Performance**: IT performs adequately
5. **Conformance**: IT complies with regulations
6. **Human Behavior**: Respect for human needs

**Governance Model**:
```
        EVALUATE
           ↓
DIRECT ←─────→ MONITOR
           ↑
    Business Processes
           ↑
      IT Processes
```

---

## 12.4 Service Management

### Service Level Agreements (SLAs)

**SLA Structure**:
```
1. INTRODUCTION
   - Parties involved
   - Service overview
   - Agreement period

2. SERVICE DESCRIPTION
   - Scope of services
   - Service hours
   - Support levels

3. SERVICE LEVELS
   - Availability targets
   - Performance metrics
   - Response times
   - Resolution times

4. RESPONSIBILITIES
   - Provider responsibilities
   - Customer responsibilities

5. SERVICE REPORTING
   - Reports and frequency
   - Review meetings

6. SERVICE CREDITS
   - Penalty structure
   - Credit calculations

7. ESCALATION
   - Escalation matrix
   - Contact information
```

**Example SLA Metrics**:
| Metric | Target | Measurement |
|--------|--------|-------------|
| Availability | 99.9% | Monthly uptime |
| Response Time (P1) | 15 minutes | Time to acknowledge |
| Resolution Time (P1) | 4 hours | Time to resolve |
| Response Time (P2) | 1 hour | Time to acknowledge |
| Resolution Time (P2) | 8 hours | Time to resolve |
| Customer Satisfaction | 4.5/5 | Survey score |

### Operational Level Agreements (OLAs)

**Purpose**: Define internal service relationships.

**Example OLA**:
```
OLA: Network Team to Service Desk

Service: Network Connectivity Support

Response Times:
- P1 Issues: 10 minutes
- P2 Issues: 30 minutes
- P3 Issues: 2 hours

Escalation: Network Team Lead → Network Manager → IT Director
```

### Key Performance Indicators (KPIs)

**Service Delivery KPIs**:
| KPI | Formula | Target |
|-----|---------|--------|
| Availability | (Total Time - Downtime) / Total Time × 100 | 99.9% |
| MTBF | Total Uptime / Number of Failures | > 720 hours |
| MTTR | Total Downtime / Number of Incidents | < 2 hours |
| First Call Resolution | Incidents Resolved First Call / Total Incidents × 100 | > 70% |
| SLA Compliance | SLAs Met / Total SLAs × 100 | > 95% |

### Critical Success Factors (CSFs)

**Definition**: Factors essential for achieving objectives.

**Examples for IT Service Management**:
1. Executive sponsorship and support
2. Clear service catalog and SLAs
3. Skilled and trained staff
4. Effective communication processes
5. Appropriate tools and technology
6. Continuous improvement culture

---

## 12.5 Change Management

### Change Management Process

**Change Process Flow**:
```
[Request for Change (RFC)]
         ↓
[Log and Categorize]
         ↓
[Assess and Evaluate]
         ↓
[Authorize (CAB/ECAB)]
         ↓
[Plan and Build]
         ↓
[Test]
         ↓
[Implement]
         ↓
[Review and Close]
```

### Request for Change (RFC)

**RFC Contents**:
- Change description and reason
- Affected systems/services
- Risk assessment
- Implementation plan
- Rollback plan
- Testing requirements
- Resource requirements
- Requested implementation date

### Change Risk Assessment

**Risk Factors**:
| Factor | Low | Medium | High |
|--------|-----|--------|------|
| Complexity | Simple config | New component | Architecture change |
| Impact | Single user | Department | Organization |
| Reversibility | Easily reversed | Moderate effort | Difficult/impossible |
| Testing | Fully tested | Partially tested | Unable to test |
| Timing | Scheduled window | Off-hours | Business hours |

### Post-Implementation Review (PIR)

**Review Areas**:
1. Was the change successful?
2. Were objectives achieved?
3. Were there unexpected impacts?
4. Was the plan followed?
5. What lessons were learned?
6. Are improvements needed?

---

## 12.6 Configuration Management

### Configuration Management Database (CMDB)

**Purpose**: Central repository of configuration item information and relationships.

**Configuration Item (CI) Types**:
| Category | Examples |
|----------|----------|
| Hardware | Servers, network devices, storage |
| Software | Applications, operating systems |
| Documentation | Policies, procedures, diagrams |
| Services | Email, web hosting, databases |
| People | Key contacts, support teams |

**CI Attributes**:
- Unique identifier
- Name and description
- Type and category
- Location
- Owner
- Status
- Relationships
- Dependencies

**CMDB Relationships**:
```
[Application A]
      │
      ├── Runs on → [Server 1]
      │                 │
      │                 └── Connected to → [Switch 1]
      │
      └── Uses → [Database Server]
                      │
                      └── Stores on → [SAN Array]
```

### Configuration Baseline

**Definition**: Approved configuration used as reference for comparison.

**Use Cases**:
- System recovery
- Change impact assessment
- Compliance auditing
- Troubleshooting

---

## 12.7 Risk Management

### IT Risk Management Process

**Process Steps**:
```
1. Risk Identification
        ↓
2. Risk Analysis
        ↓
3. Risk Evaluation
        ↓
4. Risk Treatment
        ↓
5. Risk Monitoring
        ↓
6. Review and Improve
```

### Risk Assessment Methods

#### Qualitative Risk Analysis

**Probability × Impact Matrix**:
| Probability | Impact: Low | Impact: Medium | Impact: High |
|-------------|-------------|----------------|--------------|
| High | Medium | High | Critical |
| Medium | Low | Medium | High |
| Low | Low | Low | Medium |

#### Quantitative Risk Analysis

**Key Formulas**:
| Metric | Formula |
|--------|---------|
| SLE (Single Loss Expectancy) | Asset Value × Exposure Factor |
| ARO (Annual Rate of Occurrence) | Expected frequency per year |
| ALE (Annual Loss Expectancy) | SLE × ARO |

**Example Calculation**:
```
Asset: Server worth $50,000
Exposure Factor: 40% (partial damage)
Annual Rate of Occurrence: 0.5 (once every 2 years)

SLE = $50,000 × 0.4 = $20,000
ALE = $20,000 × 0.5 = $10,000 per year
```

### Risk Treatment Options

| Strategy | Description | Example |
|----------|-------------|---------|
| Avoid | Eliminate the risk | Don't implement risky technology |
| Mitigate | Reduce probability or impact | Implement security controls |
| Transfer | Shift risk to third party | Purchase insurance |
| Accept | Acknowledge and monitor | Accept minor risks |

### Risk Register

**Contents**:
| Column | Description |
|--------|-------------|
| Risk ID | Unique identifier |
| Risk Description | What could happen |
| Category | Type of risk (operational, security) |
| Probability | Likelihood rating |
| Impact | Severity rating |
| Risk Score | Probability × Impact |
| Owner | Person responsible |
| Treatment | Selected strategy |
| Controls | Mitigation measures |
| Status | Current state |
| Review Date | Next review |

---

## 12.8 Compliance & Audit

### IT Audit Process

**Audit Phases**:
```
1. PLANNING
   - Define scope and objectives
   - Identify key risks
   - Develop audit program

2. FIELDWORK
   - Gather evidence
   - Conduct interviews
   - Test controls
   - Document findings

3. REPORTING
   - Draft findings
   - Management response
   - Final report

4. FOLLOW-UP
   - Track remediation
   - Verify corrections
   - Close findings
```

### Types of IT Audits

| Audit Type | Focus | Frequency |
|------------|-------|-----------|
| General Controls (ITGC) | Overall IT environment | Annual |
| Application Controls | Specific applications | Annual/Biannual |
| Security Audit | Information security | Annual |
| Compliance Audit | Regulatory requirements | As required |
| Operational Audit | IT operations efficiency | Periodic |

### Compliance Monitoring

**Key Activities**:
- Regular control testing
- Policy compliance reviews
- License compliance tracking
- Regulatory change monitoring
- Training compliance tracking

---

## 12.9 Vendor Management

### Vendor Lifecycle Management

**Phases**:
```
1. Strategy → 2. Selection → 3. Contract → 4. Management → 5. Exit
```

### Vendor Selection Process

**Evaluation Criteria**:
| Category | Weight | Criteria |
|----------|--------|----------|
| Technical | 30% | Functionality, scalability, integration |
| Financial | 25% | Pricing, TCO, payment terms |
| Vendor | 20% | Stability, reputation, support |
| Compliance | 15% | Certifications, data handling |
| Strategic | 10% | Innovation, roadmap, partnership |

**Selection Steps**:
1. Define requirements
2. Develop RFI/RFP
3. Evaluate responses
4. Shortlist vendors
5. Conduct demonstrations
6. Reference checks
7. Final evaluation
8. Contract negotiation

### Vendor Performance Management

**Performance Metrics**:
| Metric | Target | Review Frequency |
|--------|--------|------------------|
| SLA Compliance | > 98% | Monthly |
| Response Time | Per SLA | Monthly |
| Quality Issues | < 5/month | Monthly |
| Customer Satisfaction | > 4/5 | Quarterly |
| Security Incidents | 0 | Continuous |

### Contract Management

**Key Contract Elements**:
- Scope of services
- Service levels and penalties
- Pricing and payment terms
- Intellectual property rights
- Confidentiality obligations
- Data protection requirements
- Termination provisions
- Dispute resolution

---

## 12.10 IT Financial Management

### IT Budgeting

**Budget Categories**:
| Category | Examples |
|----------|----------|
| Capital (CapEx) | Hardware, software licenses, infrastructure |
| Operational (OpEx) | Salaries, maintenance, cloud services |
| Project | New initiatives, implementations |
| Reserve | Contingency, emergency |

**Budget Process**:
```
1. Strategic Planning → 2. Requirements Gathering → 3. Cost Estimation
        ↓                                                    ↓
7. Monitor & Adjust ← 6. Execute ← 5. Approve ← 4. Review & Adjust
```

### Cost Allocation

**Chargeback vs. Showback**:
| Method | Description | Usage |
|--------|-------------|-------|
| Chargeback | Actual billing to business units | Full cost recovery |
| Showback | Informational cost reporting | Awareness only |

**Allocation Methods**:
- Direct allocation: Specific costs to specific users
- Tiered allocation: Based on service levels
- Usage-based: Per transaction/resource used
- Fixed allocation: Even distribution

### Financial Metrics

| Metric | Formula | Use |
|--------|---------|-----|
| ROI | (Gain - Cost) / Cost × 100 | Project justification |
| TCO | Acquisition + Operating + Hidden Costs | Full cost comparison |
| Payback Period | Initial Investment / Annual Cash Flow | Break-even timing |
| NPV | Σ(Cash Flow / (1 + r)^t) | Investment comparison |

**ROI Example**:
```
Project Cost: $100,000
Annual Benefit: $40,000
5-Year Benefit: $200,000

ROI = ($200,000 - $100,000) / $100,000 × 100 = 100%
Payback Period = $100,000 / $40,000 = 2.5 years
```

---

## Hands-On Labs

### Lab 12.1: SLA Development

**Scenario**: Create an SLA for a government email service.

**Exercise**:
1. Define service scope
2. Establish availability targets
3. Set response and resolution times
4. Create escalation matrix
5. Define service credits

**Solution Template**:
```
SERVICE LEVEL AGREEMENT
Email Service - Government Department XYZ

1. SERVICE SCOPE
   - Email sending/receiving
   - Calendar and contacts
   - 25GB mailbox quota
   - Mobile access

2. SERVICE AVAILABILITY
   - Target: 99.9% monthly
   - Maintenance: Sunday 02:00-06:00
   - Planned downtime excluded

3. SUPPORT LEVELS
   Priority 1 (Service Down): Response 15min, Resolve 4hr
   Priority 2 (Major Issue): Response 1hr, Resolve 8hr
   Priority 3 (Minor Issue): Response 4hr, Resolve 24hr
   Priority 4 (Request): Response 8hr, Resolve 72hr

4. SERVICE CREDITS
   < 99.9%: 5% credit
   < 99.5%: 10% credit
   < 99.0%: 25% credit
```

### Lab 12.2: Change Risk Assessment

**Scenario**: Assess a proposed server upgrade.

**Change Details**:
- Upgrade 5 production servers from Windows Server 2019 to 2022
- Affects HR, Finance, and IT applications
- Planned for maintenance window (Saturday 22:00-06:00)

**Risk Assessment Matrix**:
| Factor | Rating | Justification |
|--------|--------|---------------|
| Complexity | Medium | Multiple servers, known process |
| Impact | High | Affects core departments |
| Reversibility | Medium | Restore from backup (4+ hours) |
| Testing | Medium | Test environment validation done |
| Timing | Low | Scheduled maintenance window |

**Overall Risk**: Medium-High
**Recommendation**: Approve with enhanced monitoring and rollback plan

### Lab 12.3: RACI Matrix Creation

**Scenario**: Create RACI for incident management.

**RACI Matrix**:
| Activity | Service Desk | Tech Team | IT Manager | Business |
|----------|--------------|-----------|------------|----------|
| Log Incident | R | I | I | C |
| Classify/Prioritize | R | C | I | I |
| Initial Diagnosis | R/A | C | I | I |
| Escalation | R | A | I | I |
| Resolution | C | R | A | I |
| Communication | R | I | A | I |
| Closure | R | C | A | I |

**Legend**: R=Responsible, A=Accountable, C=Consulted, I=Informed

---

## Chapter Summary

- **ITIL v4** provides a comprehensive service management framework built on the Service Value System
- **IT Policies** establish rules and guidelines for acceptable use, security, and operations
- **COBIT 2019** separates governance (evaluate, direct, monitor) from management (plan, build, run)
- **SLAs** define service commitments with measurable targets and accountability
- **Change Management** balances control with agility through proper risk assessment and CAB processes
- **Configuration Management** maintains accurate CI information in the CMDB
- **Risk Management** requires ongoing identification, assessment, and treatment of IT risks
- **Vendor Management** covers the complete lifecycle from selection to exit
- **IT Financial Management** ensures proper budgeting, cost allocation, and ROI tracking

---

## Multiple Choice Questions

### Beginner Level

1. What is the PRIMARY purpose of ITIL?
   - A) Software development
   - B) IT service management
   - C) Network security
   - D) Hardware maintenance

   **Answer: B**
   *Explanation: ITIL is the most widely adopted framework for IT Service Management (ITSM).*

2. Which ITIL practice focuses on restoring normal service as quickly as possible?
   - A) Problem management
   - B) Change management
   - C) Incident management
   - D) Service level management

   **Answer: C**
   *Explanation: Incident management aims to restore normal service operation as quickly as possible.*

3. What document defines the service commitments between IT and the customer?
   - A) OLA
   - B) SLA
   - C) RFC
   - D) KEDB

   **Answer: B**
   *Explanation: Service Level Agreement (SLA) defines commitments between IT and customers.*

4. Which change type requires CAB approval?
   - A) Standard change
   - B) Normal change
   - C) Emergency change
   - D) Pre-approved change

   **Answer: B**
   *Explanation: Normal changes require assessment and CAB approval.*

5. What is the purpose of a CMDB?
   - A) Store user passwords
   - B) Track configuration items and relationships
   - C) Monitor network traffic
   - D) Backup system data

   **Answer: B**
   *Explanation: Configuration Management Database (CMDB) stores information about CIs and their relationships.*

### Intermediate Level

6. Which ITIL v4 guiding principle states "Focus on value"?
   - A) Avoid unnecessary complexity
   - B) Everything should link to stakeholder value
   - C) Make small improvements
   - D) Work across boundaries

   **Answer: B**
   *Explanation: "Focus on value" means everything should directly or indirectly link to value for stakeholders.*

7. What is the relationship between a Problem and a Known Error?
   - A) They are the same thing
   - B) A Known Error is a Problem with documented root cause and workaround
   - C) A Problem is a collection of Known Errors
   - D) Known Errors are more severe than Problems

   **Answer: B**
   *Explanation: A Known Error is a problem with documented root cause and workaround stored in the KEDB.*

8. In the risk formula ALE = SLE × ARO, what does ARO represent?
   - A) Asset Risk Optimization
   - B) Annual Rate of Occurrence
   - C) Aggregate Risk Outcome
   - D) Automated Recovery Option

   **Answer: B**
   *Explanation: ARO (Annual Rate of Occurrence) is the expected frequency of a risk event per year.*

9. Which document defines internal service support relationships?
   - A) SLA
   - B) OLA
   - C) RFC
   - D) BIA

   **Answer: B**
   *Explanation: Operational Level Agreement (OLA) defines internal service relationships between IT teams.*

10. What distinguishes COBIT's governance from management?
    - A) Governance is operational, management is strategic
    - B) Governance evaluates and directs, management plans and executes
    - C) They are identical concepts
    - D) Management requires board approval

    **Answer: B**
    *Explanation: COBIT separates governance (evaluate, direct, monitor) from management (plan, build, run, monitor).*

### Advanced Level

11. A service has 99.9% availability target. What is the maximum acceptable monthly downtime?
    - A) 4.3 hours
    - B) 43 minutes
    - C) 8.7 hours
    - D) 87 minutes

    **Answer: B**
    *Explanation: 30 days × 24 hours × 60 minutes = 43,200 minutes. 0.1% = 43.2 minutes ≈ 43 minutes.*

12. In ITIL v4, which dimension covers "Activities that create value"?
    - A) Organizations and People
    - B) Information and Technology
    - C) Partners and Suppliers
    - D) Value Streams and Processes

    **Answer: D**
    *Explanation: Value Streams and Processes covers the activities, workflows, and processes that create value.*

13. Calculate the ALE for an asset worth $200,000, exposure factor of 25%, occurring once every 4 years.
    - A) $50,000
    - B) $12,500
    - C) $25,000
    - D) $6,250

    **Answer: B**
    *Explanation: SLE = $200,000 × 0.25 = $50,000. ARO = 1/4 = 0.25. ALE = $50,000 × 0.25 = $12,500.*

14. Which practice is responsible for ensuring IT services can recover from disasters?
    - A) Availability management
    - B) Service continuity management
    - C) Capacity management
    - D) Service level management

    **Answer: B**
    *Explanation: IT Service Continuity Management ensures services can recover from disaster situations.*

15. Post-Implementation Review (PIR) is conducted after which process?
    - A) Incident management
    - B) Problem management
    - C) Change management
    - D) Request management

    **Answer: C**
    *Explanation: PIR evaluates whether changes achieved their objectives and identifies lessons learned.*

16. Which vendor management phase involves RFI/RFP activities?
    - A) Strategy
    - B) Selection
    - C) Contract
    - D) Management

    **Answer: B**
    *Explanation: RFI (Request for Information) and RFP (Request for Proposal) are selection phase activities.*

17. According to COBIT, EDM domains are associated with:
    - A) Management
    - B) Governance
    - C) Operations
    - D) Technical support

    **Answer: B**
    *Explanation: EDM (Evaluate, Direct, Monitor) domains are governance objectives in COBIT.*

18. What is the PRIMARY difference between chargeback and showback?
    - A) Chargeback is manual, showback is automated
    - B) Chargeback bills costs, showback only reports costs
    - C) Showback is more accurate
    - D) They serve different departments

    **Answer: B**
    *Explanation: Chargeback actually bills business units; showback only provides cost visibility without billing.*

19. In the change management process, what is the FIRST step after receiving an RFC?
    - A) Implementation
    - B) CAB review
    - C) Log and categorize
    - D) Testing

    **Answer: C**
    *Explanation: After receiving an RFC, the first step is to log it and categorize the change type.*

20. Which ISO standard specifically addresses IT Governance?
    - A) ISO 27001
    - B) ISO 20000
    - C) ISO 38500
    - D) ISO 9001

    **Answer: C**
    *Explanation: ISO 38500 is the international standard for corporate governance of IT.*

---

## References and Further Reading

1. ITIL 4 Foundation (AXELOS)
2. COBIT 2019 Framework (ISACA)
3. ISO/IEC 38500:2015 - Governance of IT for the Organization
4. "The ITSM Guide to IT Governance" by Office of Government Commerce
5. ISACA - www.isaca.org
6. IT Governance Institute (ITGI)
7. "Service Strategy" - ITIL Core Guidance

---

*Chapter 12 completed. IT Governance ensures that IT resources are utilized efficiently, risks are managed appropriately, and IT investments align with organizational objectives.*
