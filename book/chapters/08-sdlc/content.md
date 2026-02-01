# Chapter 8: Software Development Methodologies

---

## Chapter Overview

- **Domain**: Software Engineering and Project Management
- **Estimated Study Time**: 5-6 hours
- **Prerequisites**: Basic understanding of software development, Chapter 7 (OOP concepts)
- **Difficulty Progression**: Beginner → Intermediate → Advanced → Expert

---

## Learning Objectives

By the end of this chapter, you will be able to:

1. **Describe** the phases of the Software Development Life Cycle (SDLC) and common SDLC models (B)
2. **Explain** Agile principles and **compare** Scrum and Kanban frameworks (B)
3. **Implement** Scrum ceremonies and artifacts in a software project (I)
4. **Apply** testing methodologies including TDD and BDD (I)
5. **Analyze** DevOps practices and CI/CD pipeline components (A)
6. **Evaluate** appropriate SDLC models for different project types and constraints (A)
7. **Design** a comprehensive software delivery pipeline integrating development and operations (E)
8. **Assess** version control strategies and branching models for enterprise software (E)

---

## Introduction

Software development methodologies provide structured approaches to planning, developing, and delivering software systems. As an Assistant Director IT, understanding these methodologies is essential for overseeing software projects, evaluating vendor proposals, setting realistic timelines, and ensuring quality deliverables.

The software industry has evolved from rigid, sequential approaches like Waterfall to flexible, iterative methodologies like Agile and DevOps. Each approach has strengths and appropriate use cases. Effective IT leadership requires understanding these trade-offs and matching methodologies to project requirements.

This chapter covers traditional SDLC models, Agile frameworks, testing methodologies, DevOps practices, and version control strategies. These concepts connect to project management (Chapter 16), programming (Chapter 25), and cloud computing (Chapter 9) for deployment.

---

## Section 8.1: Software Development Life Cycle (SDLC) (B)

The SDLC defines phases for developing software from initial concept to deployment and maintenance.

### 8.1.1 SDLC Phases

| Phase | Purpose | Key Activities |
|-------|---------|----------------|
| Planning | Define scope and feasibility | Requirements gathering, cost-benefit analysis, resource allocation |
| Analysis | Understand requirements | Business analysis, functional requirements, use cases |
| Design | Create architecture | System design, database design, UI/UX design |
| Implementation | Build the software | Coding, unit testing, code review |
| Testing | Verify quality | Integration testing, system testing, UAT |
| Deployment | Release to production | Installation, configuration, data migration |
| Maintenance | Ongoing support | Bug fixes, enhancements, updates |

### 8.1.2 Waterfall Model

The Waterfall model is a linear, sequential approach where each phase must complete before the next begins.

```
Requirements → Design → Implementation → Testing → Deployment → Maintenance
     ↓            ↓            ↓            ↓           ↓            ↓
  Complete    Complete    Complete    Complete    Complete    Ongoing
```

**Characteristics**:
- Sequential phases
- Heavy documentation
- Clear milestones
- Formal sign-offs between phases
- Difficult to accommodate changes

**When to Use**:
- Requirements are well-understood and stable
- Technology is mature and well-known
- Regulatory compliance requires documentation
- Short projects with clear scope

**Advantages**:
- Simple to understand and manage
- Clear milestones and deliverables
- Easy to measure progress
- Works well for small, defined projects

**Disadvantages**:
- Inflexible to changes
- Late testing discovers issues too late
- Working software delivered late
- Customer sees product only at the end

### 8.1.3 V-Model (Verification and Validation)

The V-Model extends Waterfall by associating each development phase with a corresponding testing phase.

```
Requirements Analysis ←────────────────→ Acceptance Testing
        ↓                                        ↑
    System Design ←────────────────→ System Testing
            ↓                                ↑
    Architecture Design ←──────→ Integration Testing
                ↓                        ↑
        Module Design ←────→ Unit Testing
                    ↓            ↑
               Implementation
```

**Key Concept**: Testing is planned in parallel with development, not as an afterthought.

### 8.1.4 Iterative and Incremental Models

**Iterative**: Repeat cycles of development, refining the product each iteration.

**Incremental**: Deliver working software in increments, adding features progressively.

**Benefits**:
- Early working software
- Customer feedback incorporated
- Risk identified early
- Easier to manage changes

### 8.1.5 Spiral Model

The Spiral model combines iterative development with risk management.

**Four Quadrants per Spiral**:
1. **Determine objectives**: Identify alternatives, constraints
2. **Risk analysis**: Evaluate alternatives, identify risks
3. **Development and testing**: Build and verify
4. **Planning**: Review and plan next iteration

**Best For**: Large, high-risk projects requiring careful risk management.

### 8.1.6 Rapid Application Development (RAD)

RAD emphasizes rapid prototyping and user feedback over planning.

**Phases**:
1. Requirements planning
2. User design (prototyping)
3. Construction (iterative)
4. Cutover (deployment)

**Characteristics**:
- Heavy user involvement
- Rapid prototyping
- Time-boxed development
- CASE tools and code generators

### Practical Example 8.1: Model Selection

**Scenario**: A government agency needs to develop three different applications. Match each to appropriate SDLC model.

| Project | Characteristics | Recommended Model |
|---------|-----------------|-------------------|
| Tax filing system | Strict regulations, stable requirements | Waterfall/V-Model |
| Citizen feedback portal | Evolving requirements, user-facing | Agile (Scrum) |
| Emergency response system | High risk, critical | Spiral |

---

## Section 8.2: Agile Methodologies (B)

Agile is an iterative approach that emphasizes flexibility, collaboration, and delivering value quickly.

### 8.2.1 Agile Manifesto

**Four Values**:
1. **Individuals and interactions** over processes and tools
2. **Working software** over comprehensive documentation
3. **Customer collaboration** over contract negotiation
4. **Responding to change** over following a plan

**Twelve Principles**:
1. Customer satisfaction through early and continuous delivery
2. Welcome changing requirements
3. Deliver working software frequently
4. Business and developers work together daily
5. Build projects around motivated individuals
6. Face-to-face conversation is most effective
7. Working software is the primary measure of progress
8. Sustainable development pace
9. Continuous attention to technical excellence
10. Simplicity—maximizing work not done
11. Self-organizing teams
12. Regular reflection and adjustment

### 8.2.2 Scrum Framework

Scrum is the most widely used Agile framework, organizing work into time-boxed iterations called Sprints.

**Scrum Roles**:

| Role | Responsibilities |
|------|-----------------|
| Product Owner | Defines product vision, manages backlog, prioritizes features |
| Scrum Master | Facilitates Scrum process, removes impediments, coaches team |
| Development Team | Self-organizing, cross-functional, delivers increment |

**Scrum Artifacts**:

| Artifact | Description |
|----------|-------------|
| Product Backlog | Prioritized list of all desired features |
| Sprint Backlog | Items selected for current sprint |
| Increment | Potentially shippable product at sprint end |

**Scrum Events (Ceremonies)**:

| Event | Duration | Purpose |
|-------|----------|---------|
| Sprint | 1-4 weeks | Time-boxed iteration |
| Sprint Planning | 4-8 hours | Select and plan sprint work |
| Daily Standup | 15 minutes | Synchronization, identify blockers |
| Sprint Review | 2-4 hours | Demonstrate increment to stakeholders |
| Sprint Retrospective | 1.5-3 hours | Reflect and improve process |

### Practical Example 8.2: Scrum in Practice

**Scenario**: A team developing a document management system.

**Sprint 1 (2 weeks)**:

**Sprint Planning**:
- Product Owner presents prioritized backlog
- Team selects stories: User login, Document upload, Basic search
- Team estimates: 20 story points capacity

**Daily Standups**:
- "Yesterday I completed the login API"
- "Today I'll work on UI integration"
- "Blocked: Need API documentation from external system"

**Sprint Review**:
- Demonstrate working login and upload features
- Stakeholder feedback: "Need preview for PDFs"
- New item added to Product Backlog

**Sprint Retrospective**:
- What went well: Good collaboration
- What to improve: Better estimation
- Action: Break large stories into smaller pieces

### 8.2.3 Kanban

Kanban visualizes workflow and limits work-in-progress (WIP) for continuous delivery.

**Core Principles**:
1. Visualize the workflow
2. Limit work in progress (WIP)
3. Manage flow
4. Make policies explicit
5. Implement feedback loops
6. Improve collaboratively

**Kanban Board**:
```
| Backlog | To Do | In Progress (WIP: 3) | Review | Done |
|---------|-------|----------------------|--------|------|
| Story E | Story D | Story A            | Story B |      |
| Story F |         | Story C            |         |      |
|         |         |                    |         |      |
```

**Key Metrics**:
- **Lead Time**: Total time from request to delivery
- **Cycle Time**: Time from work started to completion
- **Throughput**: Items completed per time period

### 8.2.4 Scrum vs Kanban

| Aspect | Scrum | Kanban |
|--------|-------|--------|
| Iterations | Fixed sprints | Continuous flow |
| Roles | Defined (PO, SM, Team) | No prescribed roles |
| Planning | Sprint planning | Continuous |
| Change | At sprint boundaries | Anytime |
| WIP Limits | Sprint backlog | Column-based |
| Metrics | Velocity | Lead/cycle time |
| Best For | Product development | Support, operations |

### 8.2.5 Extreme Programming (XP)

XP emphasizes technical practices for high-quality software.

**Key Practices**:
- **Pair Programming**: Two developers at one workstation
- **Test-Driven Development (TDD)**: Write tests before code
- **Continuous Integration**: Integrate and test frequently
- **Refactoring**: Improve code without changing behavior
- **Simple Design**: Build only what's needed
- **Collective Code Ownership**: Any team member can modify any code

### 8.2.6 Lean Software Development

Adapted from lean manufacturing principles:

1. **Eliminate waste**: Remove non-value-adding activities
2. **Amplify learning**: Fast feedback cycles
3. **Decide late**: Keep options open
4. **Deliver fast**: Short iterations
5. **Empower the team**: Trust developers
6. **Build integrity in**: Quality from the start
7. **See the whole**: Optimize the entire system

---

## Section 8.3: Testing Methodologies (I)

Testing ensures software meets requirements and functions correctly.

### 8.3.1 Testing Levels

| Level | Scope | Performed By | Purpose |
|-------|-------|--------------|---------|
| Unit Testing | Individual components | Developers | Verify code units work |
| Integration Testing | Component interactions | Developers/Testers | Verify interfaces work |
| System Testing | Entire application | QA Team | Verify system requirements |
| Acceptance Testing | Business requirements | Users/QA | Verify business needs met |

### 8.3.2 Testing Types

**Functional Testing**:
- Verify software does what it should
- Based on requirements/specifications
- Black-box approach

**Non-Functional Testing**:
- **Performance Testing**: Speed, scalability, stability
- **Load Testing**: Behavior under expected load
- **Stress Testing**: Behavior under extreme conditions
- **Security Testing**: Vulnerability assessment
- **Usability Testing**: User experience

**Other Testing Types**:
- **Regression Testing**: Verify changes don't break existing features
- **Smoke Testing**: Quick sanity check of major functions
- **Exploratory Testing**: Unscripted testing to find issues

### 8.3.3 Test-Driven Development (TDD)

TDD reverses the traditional development flow: write tests first, then code.

**TDD Cycle (Red-Green-Refactor)**:

```
1. RED: Write a failing test
       ↓
2. GREEN: Write minimum code to pass test
       ↓
3. REFACTOR: Improve code while tests pass
       ↓
   (Repeat)
```

**Example**:
```
# Step 1: RED - Write failing test
def test_add_positive_numbers():
    assert add(2, 3) == 5  # Fails - add() doesn't exist

# Step 2: GREEN - Minimal implementation
def add(a, b):
    return a + b  # Test passes

# Step 3: REFACTOR - Improve if needed
# (In this case, implementation is already simple)
```

**Benefits**:
- High test coverage
- Cleaner design (testable = well-designed)
- Documentation through tests
- Confidence to refactor
- Fewer bugs

### 8.3.4 Behavior-Driven Development (BDD)

BDD extends TDD by writing tests in natural language that stakeholders understand.

**Gherkin Syntax**:
```gherkin
Feature: User Login
  As a registered user
  I want to log in to the system
  So that I can access my account

  Scenario: Successful login
    Given I am on the login page
    And I have a registered account
    When I enter valid credentials
    And I click the login button
    Then I should be redirected to the dashboard
    And I should see a welcome message

  Scenario: Failed login with wrong password
    Given I am on the login page
    When I enter incorrect password
    Then I should see an error message
    And I should remain on the login page
```

**BDD Tools**: Cucumber, SpecFlow, Behave

### Practical Example 8.3: Testing Strategy

**Scenario**: Define testing strategy for a government portal.

**Testing Pyramid**:
```
         /\
        /  \     E2E Tests (10%)
       /----\    - User workflows
      /      \
     /--------\  Integration Tests (30%)
    /          \ - API testing
   /------------\- Service integration
  /              \
 /----------------\ Unit Tests (60%)
                    - Component logic
                    - Business rules
```

**Test Distribution**:
| Test Type | Count | Automation | Frequency |
|-----------|-------|------------|-----------|
| Unit | 500+ | 100% | Every commit |
| Integration | 150+ | 100% | Every build |
| E2E | 30+ | 80% | Daily |
| Performance | 10+ | 100% | Weekly |
| Security | 20+ | 80% | Weekly |
| UAT | 50+ | 0% | Release |

---

## Section 8.4: DevOps Practices (A)

DevOps bridges development and operations for faster, more reliable software delivery.

### 8.4.1 DevOps Principles

**CALMS Framework**:
- **C**ulture: Collaboration between Dev and Ops
- **A**utomation: Automate repetitive tasks
- **L**ean: Eliminate waste, continuous improvement
- **M**easurement: Metrics-driven decisions
- **S**haring: Knowledge and responsibility sharing

**Key Practices**:
1. Continuous Integration
2. Continuous Delivery/Deployment
3. Infrastructure as Code
4. Monitoring and Logging
5. Communication and Collaboration

### 8.4.2 CI/CD Pipeline

**Continuous Integration (CI)**:
- Developers integrate code frequently
- Automated build and test on each commit
- Fast feedback on integration issues

**Continuous Delivery (CD)**:
- Code is always in deployable state
- Automated testing ensures quality
- Manual approval for production deployment

**Continuous Deployment**:
- Extends CD with automatic production deployment
- Every passing change goes to production
- Requires high confidence in automated testing

**Pipeline Stages**:
```
┌──────────┐   ┌───────┐   ┌──────────┐   ┌─────────┐   ┌────────┐
│  Source  │→  │ Build │→  │   Test   │→  │ Release │→  │ Deploy │
│   Code   │   │       │   │          │   │         │   │        │
└──────────┘   └───────┘   └──────────┘   └─────────┘   └────────┘
     │              │            │              │             │
  Commit       Compile     Unit/Int       Package      Staging/
  to repo     & Package     Tests       & Version      Production
```

### 8.4.3 CI/CD Tools

| Category | Tools |
|----------|-------|
| CI/CD Platforms | Jenkins, GitLab CI, GitHub Actions, Azure DevOps |
| Build Tools | Maven, Gradle, npm, Make |
| Testing | JUnit, pytest, Selenium, Cypress |
| Artifact Repository | Nexus, JFrog Artifactory, Docker Hub |
| Deployment | Kubernetes, Docker, Ansible |
| Monitoring | Prometheus, Grafana, ELK Stack |

### Practical Example 8.4: CI/CD Pipeline Configuration

**Scenario**: Configure GitHub Actions pipeline for a web application.

```yaml
# .github/workflows/ci-cd.yml
name: CI/CD Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm ci

      - name: Run linting
        run: npm run lint

      - name: Run unit tests
        run: npm test -- --coverage

      - name: Build application
        run: npm run build

  integration-tests:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run integration tests
        run: npm run test:integration

  deploy-staging:
    needs: integration-tests
    if: github.ref == 'refs/heads/develop'
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to staging
        run: ./deploy.sh staging

  deploy-production:
    needs: integration-tests
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    environment: production  # Requires approval
    steps:
      - name: Deploy to production
        run: ./deploy.sh production
```

### 8.4.4 Infrastructure as Code (IaC)

IaC manages infrastructure through code rather than manual processes.

**Benefits**:
- Version controlled infrastructure
- Reproducible environments
- Automated provisioning
- Documentation as code
- Reduced configuration drift

**IaC Tools**:
| Tool | Provider | Language |
|------|----------|----------|
| Terraform | Multi-cloud | HCL |
| CloudFormation | AWS | JSON/YAML |
| ARM Templates | Azure | JSON |
| Ansible | Agentless | YAML |
| Puppet | Agent-based | Puppet DSL |
| Chef | Agent-based | Ruby |

**Terraform Example**:
```hcl
# Create web server in AWS
resource "aws_instance" "web_server" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"

  tags = {
    Name = "WebServer"
    Environment = "Production"
  }
}

resource "aws_security_group" "web_sg" {
  name = "web_security_group"

  ingress {
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

### 8.4.5 Configuration Management

**Ansible Example**:
```yaml
# playbook.yml - Configure web servers
---
- hosts: webservers
  become: yes

  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: latest

    - name: Start nginx service
      service:
        name: nginx
        state: started
        enabled: yes

    - name: Deploy application
      copy:
        src: ./app/
        dest: /var/www/html/
```

### 8.4.6 Containerization

**Docker**:
- Packages applications with dependencies
- Consistent across environments
- Lightweight compared to VMs

**Dockerfile Example**:
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --production
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]
```

**Docker Compose** (multi-container):
```yaml
version: '3.8'
services:
  web:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - db

  db:
    image: postgres:15
    environment:
      POSTGRES_DB: myapp
      POSTGRES_PASSWORD: secret
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:
```

### 8.4.7 Monitoring and Logging

**Observability Pillars**:
1. **Logs**: Event records
2. **Metrics**: Numerical measurements
3. **Traces**: Request paths through system

**ELK Stack**:
- **Elasticsearch**: Search and analytics
- **Logstash**: Log processing
- **Kibana**: Visualization

**Prometheus + Grafana**:
- Prometheus: Metrics collection
- Grafana: Dashboards and visualization

---

## Section 8.5: Version Control (A)

Version control tracks changes to code and enables collaboration.

### 8.5.1 Git Fundamentals

**Basic Commands**:
```bash
# Initialize repository
git init

# Clone repository
git clone https://github.com/org/repo.git

# Stage changes
git add .
git add specific-file.txt

# Commit changes
git commit -m "Add new feature"

# Push to remote
git push origin main

# Pull changes
git pull origin main

# Check status
git status

# View history
git log --oneline
```

**Branching**:
```bash
# Create and switch to branch
git checkout -b feature/new-feature

# Switch branches
git checkout main

# Merge branch
git merge feature/new-feature

# Delete branch
git branch -d feature/new-feature
```

### 8.5.2 Branching Strategies

**Git Flow**:
```
main (production)
  │
  ├── hotfix/* (urgent fixes)
  │
develop (integration)
  │
  ├── feature/* (new features)
  │
  └── release/* (preparation for release)
```

**GitHub Flow**:
```
main (always deployable)
  │
  └── feature/* (all changes)
        │
        └── Pull Request → Review → Merge → Deploy
```

**Trunk-Based Development**:
```
main/trunk (continuous integration)
  │
  └── short-lived branches (< 1 day)
```

### Practical Example 8.5: Branching Strategy Selection

**Scenario**: Choose branching strategy for different projects.

| Project Type | Strategy | Reason |
|--------------|----------|--------|
| Enterprise product | Git Flow | Multiple versions, scheduled releases |
| Web application | GitHub Flow | Continuous deployment |
| Startup/Rapid development | Trunk-Based | Fast iteration |

### 8.5.3 Pull Requests and Code Review

**Pull Request Process**:
1. Create feature branch
2. Make changes and commit
3. Push branch to remote
4. Open Pull Request
5. Code review by peers
6. Address feedback
7. Approval and merge
8. Delete feature branch

**Code Review Checklist**:
- [ ] Code follows style guidelines
- [ ] Logic is correct and efficient
- [ ] Tests are included
- [ ] Documentation updated
- [ ] No security vulnerabilities
- [ ] Error handling is appropriate
- [ ] No hardcoded secrets

---

## Section 8.6: Requirements Engineering (E)

### 8.6.1 Requirement Types

**Functional Requirements**: What the system should do
- User authentication
- Report generation
- Data validation

**Non-Functional Requirements**: Quality attributes
- Performance (response time < 2 seconds)
- Scalability (support 10,000 concurrent users)
- Security (OWASP compliance)
- Availability (99.9% uptime)

### 8.6.2 Requirements Elicitation

**Techniques**:
| Technique | Description | Best For |
|-----------|-------------|----------|
| Interviews | One-on-one discussions | Deep understanding |
| Workshops | Group sessions | Consensus building |
| Surveys | Written questionnaires | Large stakeholder groups |
| Observation | Watch users work | Understanding workflow |
| Prototyping | Build mockups | Validating UI requirements |
| Document Analysis | Review existing docs | Understanding current state |

### 8.6.3 User Stories

**Format**:
```
As a [role]
I want [feature]
So that [benefit]
```

**INVEST Criteria**:
- **I**ndependent: Can be developed separately
- **N**egotiable: Details can be discussed
- **V**aluable: Delivers user value
- **E**stimable: Can be estimated
- **S**mall: Fits in one sprint
- **T**estable: Has clear acceptance criteria

**Example**:
```
User Story: Password Reset

As a registered user
I want to reset my forgotten password
So that I can regain access to my account

Acceptance Criteria:
- Given I am on the login page
- When I click "Forgot Password"
- Then I should see a form to enter my email
- When I submit a valid email
- Then I should receive a reset link within 5 minutes
- The link should expire after 24 hours
```

---

## Section 8.7: Documentation (I)

### 8.7.1 Technical Documentation Types

| Type | Audience | Content |
|------|----------|---------|
| Requirements Spec | Stakeholders | What system should do |
| Design Document | Developers | How system is built |
| API Documentation | Developers | Endpoint specifications |
| User Manual | End Users | How to use system |
| Operations Runbook | Operations | How to maintain system |
| Code Comments | Developers | Inline explanations |

### 8.7.2 API Documentation

**OpenAPI/Swagger Example**:
```yaml
openapi: 3.0.0
info:
  title: Employee API
  version: 1.0.0

paths:
  /employees:
    get:
      summary: List all employees
      parameters:
        - name: department
          in: query
          schema:
            type: string
      responses:
        '200':
          description: List of employees
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Employee'

components:
  schemas:
    Employee:
      type: object
      properties:
        id:
          type: integer
        name:
          type: string
        department:
          type: string
```

---

## Hands-on Labs

### Lab 8.1: Scrum Sprint Simulation

See [labs/lab-08-01-scrum.md](labs/lab-08-01-scrum.md) for complete lab instructions.

**Objective**: Simulate a complete Scrum sprint with ceremonies and artifacts.

### Lab 8.2: TDD Practice

See [labs/lab-08-02-tdd.md](labs/lab-08-02-tdd.md) for complete lab instructions.

**Objective**: Develop a feature using Test-Driven Development.

### Lab 8.3: CI/CD Pipeline Setup

See [labs/lab-08-03-cicd.md](labs/lab-08-03-cicd.md) for complete lab instructions.

**Objective**: Configure a CI/CD pipeline using GitHub Actions.

### Lab 8.4: Git Workflow

See [labs/lab-08-04-git.md](labs/lab-08-04-git.md) for complete lab instructions.

**Objective**: Practice Git branching, merging, and pull requests.

### Lab 8.5: Docker Containerization

See [labs/lab-08-05-docker.md](labs/lab-08-05-docker.md) for complete lab instructions.

**Objective**: Containerize an application and deploy with Docker Compose.

---

## Chapter Summary

Key points covered in this chapter:

- SDLC defines phases from planning to maintenance; models include Waterfall, V-Model, Iterative, Spiral, and RAD.
- Agile methodologies prioritize individuals, working software, customer collaboration, and responding to change.
- Scrum organizes work into sprints with defined roles (PO, SM, Team), ceremonies, and artifacts.
- Kanban visualizes workflow and limits work-in-progress for continuous flow.
- Testing levels progress from unit to integration to system to acceptance; TDD writes tests before code.
- DevOps bridges development and operations through automation, CI/CD, and infrastructure as code.
- CI/CD pipelines automate build, test, and deployment processes for faster, reliable delivery.
- Infrastructure as Code (Terraform, Ansible) enables version-controlled, reproducible infrastructure.
- Version control with Git supports collaboration through branching strategies and pull requests.
- Requirements engineering captures functional and non-functional requirements through various elicitation techniques.

---

## Key Takeaways

1. **Match methodology to project**: Waterfall for stable requirements, Agile for evolving needs, Spiral for high-risk projects.

2. **Agile is about mindset, not just process**: The values and principles matter more than specific practices.

3. **Testing is not optional**: Automated testing at multiple levels is essential for quality software delivery.

4. **DevOps is culture plus tools**: Successful DevOps requires collaboration between teams, not just automation.

5. **Version control is critical infrastructure**: Proper branching strategies and code review processes prevent integration problems.

---

## Self-Assessment Questions

Answer these questions in your own words (2-3 paragraphs each):

1. **Compare Waterfall and Agile methodologies**. When would you recommend each for a government IT project? What are the risks of choosing the wrong approach? (B/I)

2. **Describe the Scrum framework** including roles, ceremonies, and artifacts. How would you implement Scrum for a team that has never used Agile before? (I)

3. **Design a CI/CD pipeline** for a web application that includes building, testing, and deploying to staging and production environments. Include specific tools and quality gates. (A)

4. **Evaluate different branching strategies** (Git Flow, GitHub Flow, Trunk-Based Development) for a government agency with multiple development teams working on the same product. What strategy would you recommend and why? (A/E)

5. **A large government project is experiencing delays and quality issues** using traditional Waterfall methodology. Propose a transition plan to Agile practices, including how to handle the existing requirements documentation and contractual obligations. (E)

---

## Chapter MCQs

See [mcqs.md](mcqs.md) for complete MCQ set with:
- 45 Beginner (B) questions (25%)
- 63 Intermediate (I) questions (35%)
- 54 Advanced (A) questions (30%)
- 18 Expert (E) questions (10%)

Total: 180 MCQs

---

## References

- Beck, Kent, et al. "Manifesto for Agile Software Development." 2001. https://agilemanifesto.org/
- Schwaber, Ken, and Jeff Sutherland. "The Scrum Guide." 2020. https://scrumguides.org/
- Kim, Gene, et al. "The DevOps Handbook." IT Revolution Press, 2016.
- Humble, Jez, and David Farley. "Continuous Delivery." Addison-Wesley, 2010.
- Beck, Kent. "Extreme Programming Explained." 2nd Edition. Addison-Wesley, 2004.
- Chacon, Scott, and Ben Straub. "Pro Git." 2nd Edition. Apress, 2014. https://git-scm.com/book
- Anderson, David J. "Kanban: Successful Evolutionary Change for Your Technology Business." Blue Hole Press, 2010.
- PMBOK Guide. 7th Edition. Project Management Institute, 2021.

---

**Chapter Status**: Draft
**Last Updated**: 2026-02-01
**Author**: Content Development Team
**Reviewer**: Pending Technical Review
