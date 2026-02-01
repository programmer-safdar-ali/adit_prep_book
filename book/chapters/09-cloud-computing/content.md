# Chapter 9: Cloud Computing & Virtualization

---

## Chapter Overview

- **Domain**: Cloud Infrastructure and Services
- **Estimated Study Time**: 7-8 hours
- **Prerequisites**: Chapter 2 (Networking), Chapter 4 (Server Administration)
- **Difficulty Progression**: Beginner → Intermediate → Advanced → Expert

---

## Learning Objectives

By the end of this chapter, you will be able to:

1. **Define** cloud computing and **explain** service models (IaaS, PaaS, SaaS) and deployment models (B)
2. **Describe** key services from major cloud providers (AWS, Azure, GCP) (B)
3. **Implement** virtual networks, compute instances, and storage solutions in cloud environments (I)
4. **Configure** container orchestration using Kubernetes (I)
5. **Analyze** cloud security requirements and **apply** IAM best practices (A)
6. **Evaluate** cloud migration strategies and calculate total cost of ownership (A)
7. **Design** multi-region, highly available cloud architectures (E)
8. **Assess** serverless computing patterns and event-driven architectures (E)

---

## Introduction

Cloud computing has transformed how organizations procure, deploy, and manage IT infrastructure. As an Assistant Director IT, understanding cloud technologies is essential for making strategic decisions about infrastructure modernization, cost optimization, and service delivery.

Government agencies worldwide are adopting cloud computing to improve efficiency, reduce costs, and enhance service delivery. However, cloud adoption requires careful consideration of security, compliance, data sovereignty, and vendor lock-in risks.

This chapter covers cloud fundamentals, major provider services, virtualization technologies, containerization, and cloud architecture patterns. These concepts connect to server administration (Chapter 4), security (Chapter 10), and disaster recovery (Chapter 23).

---

## Section 9.1: Cloud Computing Fundamentals (B)

### 9.1.1 Cloud Service Models

**IaaS (Infrastructure as a Service)**:
- Provides virtualized computing resources
- Customer manages: OS, applications, data
- Provider manages: Hardware, networking, virtualization
- Examples: AWS EC2, Azure VMs, Google Compute Engine

**PaaS (Platform as a Service)**:
- Provides development and deployment platform
- Customer manages: Applications, data
- Provider manages: Runtime, middleware, OS, infrastructure
- Examples: AWS Elastic Beanstalk, Azure App Service, Google App Engine

**SaaS (Software as a Service)**:
- Provides complete applications
- Customer manages: User data, configurations
- Provider manages: Everything else
- Examples: Microsoft 365, Salesforce, Google Workspace

**FaaS (Function as a Service/Serverless)**:
- Run code without managing servers
- Pay only for execution time
- Auto-scales to demand
- Examples: AWS Lambda, Azure Functions, Google Cloud Functions

**DaaS (Desktop as a Service)**:
- Virtual desktop infrastructure in cloud
- Centralized desktop management
- Examples: Amazon WorkSpaces, Azure Virtual Desktop

### 9.1.2 Cloud Deployment Models

| Model | Description | Use Case |
|-------|-------------|----------|
| Public Cloud | Shared infrastructure, multi-tenant | General workloads, cost-sensitive |
| Private Cloud | Dedicated infrastructure, single tenant | Sensitive data, compliance |
| Hybrid Cloud | Combination of public and private | Mixed requirements |
| Community Cloud | Shared by organizations with common concerns | Government, healthcare |
| Multi-Cloud | Multiple cloud providers | Avoid vendor lock-in |

### 9.1.3 Cloud Benefits and Challenges

**Benefits**:
- **Scalability**: Scale resources up/down on demand
- **Cost Efficiency**: Pay-as-you-go, no capital expenditure
- **Reliability**: Provider-managed redundancy
- **Speed**: Rapid provisioning of resources
- **Global Reach**: Deploy in regions worldwide
- **Security**: Enterprise-grade security capabilities

**Challenges**:
- **Security Concerns**: Data protection, access control
- **Compliance**: Regulatory requirements, data residency
- **Vendor Lock-in**: Migration difficulty
- **Network Dependency**: Requires reliable connectivity
- **Cost Management**: Can exceed expectations if not managed
- **Skill Gap**: Requires cloud expertise

### Practical Example 9.1: Service Model Selection

**Scenario**: A government agency needs to host different applications. Match to appropriate service model.

| Application | Requirements | Recommended Model |
|-------------|--------------|-------------------|
| Custom ERP system | Full control over OS and networking | IaaS |
| Web application | Focus on code, not infrastructure | PaaS |
| Email and productivity | No management burden | SaaS |
| Event processing | Sporadic, unpredictable load | FaaS |

---

## Section 9.2: Major Cloud Providers (B)

### 9.2.1 Amazon Web Services (AWS)

**Key Services**:

| Category | Service | Purpose |
|----------|---------|---------|
| Compute | EC2 | Virtual servers |
| Compute | Lambda | Serverless functions |
| Storage | S3 | Object storage |
| Storage | EBS | Block storage |
| Database | RDS | Managed relational database |
| Database | DynamoDB | NoSQL database |
| Networking | VPC | Virtual network |
| Networking | Route 53 | DNS service |
| Security | IAM | Identity and access management |
| Monitoring | CloudWatch | Monitoring and logging |

**AWS Global Infrastructure**:
- Regions: Geographic areas (e.g., us-east-1)
- Availability Zones: Data centers within regions
- Edge Locations: CDN and caching points

### 9.2.2 Microsoft Azure

**Key Services**:

| Category | Service | Purpose |
|----------|---------|---------|
| Compute | Virtual Machines | Virtual servers |
| Compute | Azure Functions | Serverless |
| Storage | Blob Storage | Object storage |
| Storage | Azure Disk | Block storage |
| Database | SQL Database | Managed SQL |
| Database | Cosmos DB | Multi-model NoSQL |
| Networking | Virtual Network | Virtual network |
| Security | Azure AD | Identity management |
| Monitoring | Azure Monitor | Monitoring |

**Azure Benefits for Enterprise**:
- Strong integration with Microsoft products
- Hybrid cloud with Azure Stack
- Enterprise agreements

### 9.2.3 Google Cloud Platform (GCP)

**Key Services**:

| Category | Service | Purpose |
|----------|---------|---------|
| Compute | Compute Engine | Virtual servers |
| Compute | Cloud Functions | Serverless |
| Storage | Cloud Storage | Object storage |
| Database | Cloud SQL | Managed SQL |
| Database | BigQuery | Data warehouse |
| Analytics | Dataflow | Stream/batch processing |
| AI/ML | Vertex AI | Machine learning |
| Networking | VPC | Virtual network |

**GCP Strengths**:
- Big data and analytics
- Machine learning capabilities
- Kubernetes (originated at Google)

### Practical Example 9.2: Multi-Cloud Strategy

**Scenario**: Government agency using multiple clouds.

**Workload Distribution**:
| Workload | Provider | Reason |
|----------|----------|--------|
| Primary applications | AWS | Mature, comprehensive |
| Microsoft workloads | Azure | Integration with M365, AD |
| Big data analytics | GCP | BigQuery capabilities |
| CDN | Multi | Best regional coverage |

---

## Section 9.3: Cloud Compute Services (I)

### 9.3.1 Virtual Machines

**Instance Types** (AWS EC2 example):

| Family | Use Case | Example |
|--------|----------|---------|
| General Purpose | Balanced compute/memory | t3, m6i |
| Compute Optimized | CPU-intensive workloads | c6i |
| Memory Optimized | Memory-intensive applications | r6i |
| Storage Optimized | High I/O workloads | i3 |
| GPU | Machine learning, graphics | p4, g5 |

**Pricing Models**:
| Model | Description | Savings |
|-------|-------------|---------|
| On-Demand | Pay by the hour/second | Baseline |
| Reserved | 1-3 year commitment | 30-75% |
| Spot/Preemptible | Unused capacity, can be terminated | 60-90% |
| Savings Plans | Flexible commitment | 20-72% |

### 9.3.2 Auto Scaling

Auto scaling automatically adjusts compute capacity based on demand.

**Scaling Types**:
- **Horizontal (Scale Out/In)**: Add/remove instances
- **Vertical (Scale Up/Down)**: Resize instances

**Scaling Policies**:
- **Target Tracking**: Maintain specific metric value
- **Step Scaling**: Scale based on metric thresholds
- **Scheduled**: Scale at specific times

### Practical Example 9.3: Auto Scaling Configuration

**Scenario**: Configure auto scaling for a government web portal.

**Configuration**:
```yaml
Auto Scaling Group:
  Minimum: 2 instances
  Maximum: 10 instances
  Desired: 4 instances

Scaling Policies:
  Scale Out:
    Metric: CPU Utilization
    Threshold: > 70% for 5 minutes
    Action: Add 2 instances
    Cooldown: 300 seconds

  Scale In:
    Metric: CPU Utilization
    Threshold: < 30% for 10 minutes
    Action: Remove 1 instance
    Cooldown: 300 seconds

Health Check:
  Type: ELB health check
  Interval: 30 seconds
  Unhealthy threshold: 2
```

---

## Section 9.4: Cloud Storage Services (I)

### 9.4.1 Storage Types

**Object Storage** (S3, Blob Storage, Cloud Storage):
- Unstructured data (files, images, videos)
- Accessed via HTTP/REST APIs
- Highly scalable and durable
- Storage classes for cost optimization

**Block Storage** (EBS, Azure Disk):
- Attached to compute instances
- Formatted with file system
- Low-latency access
- Snapshots for backup

**File Storage** (EFS, Azure Files):
- Network file system
- Shared across instances
- POSIX-compliant

### 9.4.2 Storage Classes and Lifecycle

**AWS S3 Storage Classes**:

| Class | Access | Durability | Use Case |
|-------|--------|------------|----------|
| Standard | Frequent | 99.999999999% | Active data |
| Intelligent-Tiering | Variable | 99.999999999% | Unknown patterns |
| Standard-IA | Infrequent | 99.999999999% | Backups |
| Glacier Instant | Archive | 99.999999999% | Compliance archives |
| Glacier Deep Archive | Rare | 99.999999999% | Long-term retention |

**Lifecycle Policy Example**:
```json
{
  "Rules": [
    {
      "ID": "ArchiveOldData",
      "Status": "Enabled",
      "Transitions": [
        {"Days": 30, "StorageClass": "STANDARD_IA"},
        {"Days": 90, "StorageClass": "GLACIER"},
        {"Days": 365, "StorageClass": "DEEP_ARCHIVE"}
      ],
      "Expiration": {"Days": 2555}
    }
  ]
}
```

---

## Section 9.5: Cloud Networking (I)

### 9.5.1 Virtual Private Cloud (VPC)

A VPC is an isolated virtual network in the cloud.

**Components**:
- **Subnets**: IP address ranges within VPC
- **Route Tables**: Control traffic routing
- **Internet Gateway**: Connect to internet
- **NAT Gateway**: Outbound internet for private subnets
- **Security Groups**: Instance-level firewall
- **Network ACLs**: Subnet-level firewall

### Practical Example 9.4: VPC Architecture

**Scenario**: Design VPC for a three-tier application.

```
VPC: 10.0.0.0/16
├── Public Subnet 1 (10.0.1.0/24) - AZ-a
│   ├── NAT Gateway
│   └── Load Balancer
├── Public Subnet 2 (10.0.2.0/24) - AZ-b
│   └── Load Balancer
├── Private Subnet 1 (10.0.10.0/24) - AZ-a
│   └── Web Servers
├── Private Subnet 2 (10.0.11.0/24) - AZ-b
│   └── Web Servers
├── Private Subnet 3 (10.0.20.0/24) - AZ-a
│   └── Application Servers
├── Private Subnet 4 (10.0.21.0/24) - AZ-b
│   └── Application Servers
├── Private Subnet 5 (10.0.30.0/24) - AZ-a
│   └── Database Primary
└── Private Subnet 6 (10.0.31.0/24) - AZ-b
    └── Database Standby
```

### 9.5.2 Load Balancing

**Load Balancer Types**:

| Type | Layer | Use Case |
|------|-------|----------|
| Application (ALB) | 7 | HTTP/HTTPS routing |
| Network (NLB) | 4 | High-performance TCP/UDP |
| Classic (CLB) | 4/7 | Legacy |
| Gateway (GWLB) | 3 | Third-party appliances |

### 9.5.3 VPN and Direct Connect

**Site-to-Site VPN**:
- Encrypted connection over internet
- Quick to set up
- Variable performance

**Direct Connect / ExpressRoute**:
- Dedicated private connection
- Consistent performance
- Higher cost, longer setup

---

## Section 9.6: Containerization and Kubernetes (I)

### 9.6.1 Container Orchestration

**Kubernetes (K8s)** is the industry-standard container orchestration platform.

**Key Concepts**:

| Concept | Description |
|---------|-------------|
| Pod | Smallest deployable unit (1+ containers) |
| Deployment | Manages pod replicas |
| Service | Network endpoint for pods |
| Namespace | Logical cluster partition |
| ConfigMap | Configuration data |
| Secret | Sensitive data |
| PersistentVolume | Storage |
| Ingress | External access to services |

### 9.6.2 Kubernetes Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         Kubernetes Cluster                       │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │                      Control Plane                         │ │
│  │  ┌──────────┐ ┌───────────┐ ┌──────────┐ ┌─────────────┐  │ │
│  │  │API Server│ │Controller │ │Scheduler │ │    etcd     │  │ │
│  │  └──────────┘ │ Manager   │ └──────────┘ └─────────────┘  │ │
│  │               └───────────┘                               │ │
│  └────────────────────────────────────────────────────────────┘ │
│                                                                  │
│  ┌───────────────────────────┐ ┌───────────────────────────┐   │
│  │        Worker Node 1       │ │        Worker Node 2       │   │
│  │ ┌────────┐ ┌────────┐     │ │ ┌────────┐ ┌────────┐     │   │
│  │ │  Pod   │ │  Pod   │     │ │ │  Pod   │ │  Pod   │     │   │
│  │ └────────┘ └────────┘     │ │ └────────┘ └────────┘     │   │
│  │ ┌───────────────────────┐ │ │ ┌───────────────────────┐ │   │
│  │ │kubelet│kube-proxy│cri │ │ │ │kubelet│kube-proxy│cri │ │   │
│  │ └───────────────────────┘ │ │ └───────────────────────┘ │   │
│  └───────────────────────────┘ └───────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

### 9.6.3 Managed Kubernetes Services

| Provider | Service |
|----------|---------|
| AWS | EKS (Elastic Kubernetes Service) |
| Azure | AKS (Azure Kubernetes Service) |
| GCP | GKE (Google Kubernetes Engine) |

### Practical Example 9.5: Kubernetes Deployment

**Scenario**: Deploy a web application to Kubernetes.

```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web-app
  template:
    metadata:
      labels:
        app: web-app
    spec:
      containers:
      - name: web-app
        image: myregistry/web-app:v1.0
        ports:
        - containerPort: 8080
        resources:
          requests:
            memory: "256Mi"
            cpu: "250m"
          limits:
            memory: "512Mi"
            cpu: "500m"
        livenessProbe:
          httpGet:
            path: /health
            port: 8080
          initialDelaySeconds: 30
          periodSeconds: 10

---
# service.yaml
apiVersion: v1
kind: Service
metadata:
  name: web-app-service
spec:
  type: LoadBalancer
  ports:
  - port: 80
    targetPort: 8080
  selector:
    app: web-app
```

---

## Section 9.7: Cloud Security (A)

### 9.7.1 Shared Responsibility Model

| Layer | IaaS | PaaS | SaaS |
|-------|------|------|------|
| Data | Customer | Customer | Customer |
| Applications | Customer | Customer | Provider |
| Runtime | Customer | Provider | Provider |
| Middleware | Customer | Provider | Provider |
| Operating System | Customer | Provider | Provider |
| Virtualization | Provider | Provider | Provider |
| Hardware | Provider | Provider | Provider |
| Network | Provider | Provider | Provider |
| Facilities | Provider | Provider | Provider |

### 9.7.2 Identity and Access Management (IAM)

**IAM Best Practices**:
1. **Least Privilege**: Grant minimum necessary permissions
2. **Use Roles**: Prefer roles over long-term credentials
3. **Enable MFA**: Require multi-factor authentication
4. **Rotate Credentials**: Regular rotation of access keys
5. **Audit Access**: Regular review of permissions
6. **Use Groups**: Manage permissions through groups

**IAM Policy Example** (AWS):
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::my-bucket",
        "arn:aws:s3:::my-bucket/*"
      ],
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": "10.0.0.0/8"
        }
      }
    }
  ]
}
```

### 9.7.3 Data Protection

**Encryption**:
- **At Rest**: Server-side encryption (SSE)
- **In Transit**: TLS/SSL
- **Key Management**: KMS, HSM

**Data Classification**:
- Identify sensitive data
- Apply appropriate controls
- Monitor access

### 9.7.4 Compliance and Governance

**Compliance Frameworks**:
- SOC 2
- ISO 27001
- HIPAA
- PCI-DSS
- FedRAMP (Government)

**Governance Tools**:
- AWS Config, Organizations, Control Tower
- Azure Policy, Blueprints
- GCP Organization Policy

---

## Section 9.8: Cloud Migration (A)

### 9.8.1 Migration Strategies (6 R's)

| Strategy | Description | Use Case |
|----------|-------------|----------|
| Rehost | Lift and shift | Quick migration |
| Replatform | Lift and optimize | Minor modifications |
| Repurchase | Move to SaaS | Replace with cloud-native |
| Refactor | Re-architect | Cloud-native benefits |
| Retain | Keep as-is | Not ready to migrate |
| Retire | Decommission | No longer needed |

### 9.8.2 Cloud Readiness Assessment

**Assessment Areas**:
1. Application inventory
2. Dependency mapping
3. Technical requirements
4. Security and compliance
5. Cost analysis
6. Skills assessment

### Practical Example 9.6: Migration Planning

**Scenario**: Migrate legacy applications to cloud.

**Application Portfolio**:
| Application | Strategy | Rationale |
|-------------|----------|-----------|
| Static website | Rehost | Simple, quick win |
| Custom CRM | Repurchase | SaaS alternative available |
| Core database | Replatform | Use managed RDS |
| Monolithic ERP | Refactor | Break into microservices |
| Legacy system | Retain | Too complex, EOL planned |

---

## Section 9.9: Serverless Computing (E)

### 9.9.1 Serverless Architecture

**Characteristics**:
- No server management
- Auto-scaling
- Pay-per-execution
- Event-driven

**Services**:
| Provider | Compute | API | Database |
|----------|---------|-----|----------|
| AWS | Lambda | API Gateway | DynamoDB |
| Azure | Functions | API Management | Cosmos DB |
| GCP | Cloud Functions | Apigee | Firestore |

### 9.9.2 Event-Driven Architecture

**Event Sources**:
- HTTP requests (API Gateway)
- Message queues (SQS, EventBridge)
- Storage events (S3, Blob)
- Database changes (DynamoDB Streams)
- Scheduled events (CloudWatch Events)

### Practical Example 9.7: Serverless Application

**Scenario**: Image processing pipeline.

```
                   ┌──────────────┐
                   │   S3 Bucket  │
                   │ (Image Upload)│
                   └──────┬───────┘
                          │ Trigger
                          ▼
                   ┌──────────────┐
                   │    Lambda    │
                   │(Process Image)│
                   └──────┬───────┘
                          │
            ┌─────────────┴─────────────┐
            ▼                           ▼
     ┌──────────────┐           ┌──────────────┐
     │   S3 Bucket  │           │   DynamoDB   │
     │(Thumbnails)  │           │ (Metadata)   │
     └──────────────┘           └──────────────┘
```

---

## Section 9.10: Cloud Architecture Patterns (E)

### 9.10.1 High Availability Architecture

**Multi-AZ Deployment**:
```
              Region: us-east-1
    ┌──────────────────────────────────────┐
    │                                      │
    │  AZ-a                    AZ-b        │
    │  ┌─────────┐            ┌─────────┐  │
    │  │ Web     │            │ Web     │  │
    │  │ Servers │            │ Servers │  │
    │  └────┬────┘            └────┬────┘  │
    │       │                      │       │
    │       └──────────┬───────────┘       │
    │                  │                   │
    │            ┌─────┴─────┐             │
    │            │    ALB    │             │
    │            └───────────┘             │
    │                                      │
    │  ┌─────────┐            ┌─────────┐  │
    │  │   DB    │◄──────────►│   DB    │  │
    │  │ Primary │ Replication│ Standby │  │
    │  └─────────┘            └─────────┘  │
    └──────────────────────────────────────┘
```

### 9.10.2 Multi-Region Architecture

**Active-Passive**:
- Primary region handles traffic
- Secondary region on standby
- DNS failover on disaster

**Active-Active**:
- Both regions handle traffic
- Global load balancing
- Data replication between regions

### 9.10.3 Well-Architected Framework

**AWS Well-Architected Pillars**:

1. **Operational Excellence**: Run and monitor systems
2. **Security**: Protect information and systems
3. **Reliability**: Ensure workload performs correctly
4. **Performance Efficiency**: Use resources efficiently
5. **Cost Optimization**: Avoid unnecessary costs
6. **Sustainability**: Minimize environmental impact

---

## Hands-on Labs

### Lab 9.1: VPC and EC2 Setup

See [labs/lab-09-01-vpc-ec2.md](labs/lab-09-01-vpc-ec2.md) for complete lab instructions.

**Objective**: Create a VPC with public and private subnets, launch EC2 instances.

### Lab 9.2: S3 and Storage Configuration

See [labs/lab-09-02-storage.md](labs/lab-09-02-storage.md) for complete lab instructions.

**Objective**: Configure S3 buckets with lifecycle policies and access controls.

### Lab 9.3: Kubernetes Deployment

See [labs/lab-09-03-kubernetes.md](labs/lab-09-03-kubernetes.md) for complete lab instructions.

**Objective**: Deploy an application to Kubernetes with services and ingress.

### Lab 9.4: Serverless Application

See [labs/lab-09-04-serverless.md](labs/lab-09-04-serverless.md) for complete lab instructions.

**Objective**: Build a serverless API with Lambda and API Gateway.

### Lab 9.5: Cloud Security Configuration

See [labs/lab-09-05-security.md](labs/lab-09-05-security.md) for complete lab instructions.

**Objective**: Configure IAM policies, encryption, and security groups.

---

## Chapter Summary

Key points covered in this chapter:

- Cloud service models (IaaS, PaaS, SaaS, FaaS) offer different levels of abstraction and management responsibility.
- Deployment models (public, private, hybrid, multi-cloud) address different organizational requirements.
- Major cloud providers (AWS, Azure, GCP) offer similar services with different strengths.
- Virtual machines support various instance types and pricing models (on-demand, reserved, spot).
- Auto scaling adjusts capacity based on demand using horizontal or vertical scaling.
- Cloud storage options include object, block, and file storage with tiered classes for cost optimization.
- VPC networking provides isolated virtual networks with subnets, gateways, and security controls.
- Kubernetes orchestrates containers with deployments, services, and managed offerings from all major providers.
- Cloud security follows the shared responsibility model with IAM, encryption, and compliance requirements.
- Migration strategies (6 R's) guide moving workloads to cloud based on application characteristics.
- Serverless computing enables event-driven architectures without managing infrastructure.
- Well-Architected Framework provides guidance for building secure, reliable, efficient systems.

---

## Key Takeaways

1. **Understand the shared responsibility model**: Know what you manage vs. what the provider manages for each service model.

2. **Right-size resources and use appropriate pricing**: Over-provisioning wastes money; reserved capacity saves money for stable workloads.

3. **Design for failure**: Use multiple availability zones, auto scaling, and load balancing for resilience.

4. **Security is paramount**: Apply least privilege, enable encryption, and audit access regularly.

5. **Cloud is not automatically cheaper**: Calculate TCO carefully and manage costs proactively.

---

## Self-Assessment Questions

Answer these questions in your own words (2-3 paragraphs each):

1. **Compare IaaS, PaaS, and SaaS** with examples. When would a government agency choose each? (B/I)

2. **Design a VPC architecture** for a three-tier web application with high availability across two availability zones. Include subnets, security groups, and routing. (I/A)

3. **Explain the shared responsibility model** for IaaS. What security controls are customer responsibilities vs. provider responsibilities? (A)

4. **Evaluate different cloud migration strategies** (6 R's) for a government agency with 50 legacy applications. How would you prioritize the migration? (A/E)

5. **Design a multi-region, highly available architecture** for a critical government service with RPO of 5 minutes and RTO of 15 minutes. Include specific AWS/Azure/GCP services and data replication strategy. (E)

---

## Chapter MCQs

See [mcqs.md](mcqs.md) for complete MCQ set with:
- 55 Beginner (B) questions (25%)
- 77 Intermediate (I) questions (35%)
- 66 Advanced (A) questions (30%)
- 22 Expert (E) questions (10%)

Total: 220 MCQs

---

## References

- AWS. "AWS Documentation." 2025. https://docs.aws.amazon.com/
- Microsoft. "Azure Documentation." 2025. https://docs.microsoft.com/azure/
- Google Cloud. "Google Cloud Documentation." 2025. https://cloud.google.com/docs/
- AWS. "AWS Well-Architected Framework." 2025. https://aws.amazon.com/architecture/well-architected/
- NIST. "SP 800-145 - The NIST Definition of Cloud Computing." 2011.
- Kubernetes. "Kubernetes Documentation." 2025. https://kubernetes.io/docs/
- Burns, Brendan. "Kubernetes: Up and Running." 3rd Edition. O'Reilly, 2022.
- Wittig, Michael, and Andreas Wittig. "Amazon Web Services in Action." 3rd Edition. Manning, 2023.

---

**Chapter Status**: Draft
**Last Updated**: 2026-02-01
**Author**: Content Development Team
**Reviewer**: Pending Technical Review
