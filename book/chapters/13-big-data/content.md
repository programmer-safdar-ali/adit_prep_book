# Chapter 13: Big Data & Modern Technologies

## Overview

Big Data has transformed how organizations collect, process, and derive value from vast amounts of information. For Assistant Directors IT in public service, understanding Big Data technologies is essential as government agencies increasingly leverage data analytics for policy-making, service delivery optimization, and evidence-based decision-making. This chapter covers the 5 V's of Big Data, the Hadoop ecosystem, data processing frameworks, NoSQL databases, data warehousing concepts, machine learning fundamentals, and emerging technologies like IoT and blockchain.

## Learning Objectives

After completing this chapter, you will be able to:

- Explain the 5 V's of Big Data and their implications for data management
- Describe components of the Hadoop ecosystem and their functions
- Differentiate between batch and stream processing paradigms
- Select appropriate NoSQL database types based on use case requirements
- Design data warehousing solutions using star and snowflake schemas
- Understand fundamental machine learning concepts and algorithms
- Apply IoT and blockchain concepts to government use cases

---

## 13.1 Big Data Characteristics

### The 5 V's of Big Data

Big Data is characterized by five key dimensions:

```
              ┌─────────────────────────────────────┐
              │           THE 5 V's                 │
              │                                     │
              │    VOLUME ─── VELOCITY ─── VARIETY  │
              │         \          |          /     │
              │          \         |         /      │
              │           \        |        /       │
              │            VERACITY ─ VALUE         │
              └─────────────────────────────────────┘
```

#### Volume

**Definition**: The massive scale of data generated.

**Characteristics**:
- Terabytes to petabytes of data
- Growing exponentially
- Beyond traditional database capacity

**Government Examples**:
| Source | Daily Volume |
|--------|--------------|
| Tax records | Millions of transactions |
| Census data | Hundreds of millions of records |
| CCTV footage | Petabytes of video |
| Social services | Millions of applications |

#### Velocity

**Definition**: Speed at which data is generated, processed, and analyzed.

**Types**:
- **Batch Processing**: Data collected and processed periodically
- **Real-time Processing**: Data processed as it arrives
- **Near Real-time**: Processing with minimal delay

**Government Examples**:
- Emergency response systems (real-time)
- Traffic monitoring (near real-time)
- Tax processing (batch)

#### Variety

**Definition**: Different types and formats of data.

**Data Types**:
| Type | Format | Examples |
|------|--------|----------|
| Structured | Tables, databases | SQL databases, spreadsheets |
| Semi-structured | Tagged data | XML, JSON, log files |
| Unstructured | No predefined format | Images, videos, documents |

**Government Data Variety**:
- Forms and applications (structured)
- Emails and documents (semi-structured)
- Social media, images (unstructured)

#### Veracity

**Definition**: Accuracy, reliability, and trustworthiness of data.

**Challenges**:
- Data quality issues
- Inconsistent formats
- Missing values
- Outdated information

**Quality Dimensions**:
- Accuracy: Correctness of data
- Completeness: No missing values
- Consistency: Same across systems
- Timeliness: Current and relevant

#### Value

**Definition**: Business worth derived from data.

**Value Creation**:
- Informed decision-making
- Operational efficiency
- Predictive insights
- Service improvement

---

## 13.2 Hadoop Ecosystem

### Introduction to Hadoop

**Apache Hadoop** is an open-source framework for distributed storage and processing of large datasets.

**Core Components**:
```
┌─────────────────────────────────────────────────┐
│                HADOOP ECOSYSTEM                  │
├─────────────────────────────────────────────────┤
│  Data Access: Hive | Pig | HBase | Sqoop | Flume │
├─────────────────────────────────────────────────┤
│         Processing: MapReduce | Spark            │
├─────────────────────────────────────────────────┤
│      Resource Management: YARN                   │
├─────────────────────────────────────────────────┤
│         Storage: HDFS                            │
└─────────────────────────────────────────────────┘
```

### HDFS (Hadoop Distributed File System)

**Purpose**: Distributed storage for large files across multiple nodes.

**Architecture**:
```
                     ┌───────────────┐
                     │   NameNode    │
                     │   (Master)    │
                     │ - Metadata    │
                     │ - Directory   │
                     └───────┬───────┘
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
┌───────▼───────┐   ┌───────▼───────┐   ┌───────▼───────┐
│   DataNode 1  │   │   DataNode 2  │   │   DataNode 3  │
│ Block 1, 3, 5 │   │ Block 2, 4, 1 │   │ Block 3, 5, 2 │
└───────────────┘   └───────────────┘   └───────────────┘
```

**Key Features**:
| Feature | Description |
|---------|-------------|
| Block Size | Default 128MB (larger than traditional FS) |
| Replication | Default 3 copies across nodes |
| Fault Tolerance | Automatic recovery from failures |
| Scalability | Linear scalability by adding nodes |

**HDFS Commands**:
```bash
# List files
hdfs dfs -ls /user/data

# Copy from local to HDFS
hdfs dfs -put localfile.txt /user/data/

# Copy from HDFS to local
hdfs dfs -get /user/data/file.txt ./

# Create directory
hdfs dfs -mkdir /user/newdir

# Check file system health
hdfs fsck /user/data -files -blocks
```

### MapReduce

**Purpose**: Programming model for distributed data processing.

**Phases**:
```
Input → [Split] → [Map] → [Shuffle & Sort] → [Reduce] → Output
```

**Example: Word Count**:
```
Input: "hello world hello"

MAP PHASE:
  "hello" → (hello, 1)
  "world" → (world, 1)
  "hello" → (hello, 1)

SHUFFLE & SORT:
  (hello, [1, 1])
  (world, [1])

REDUCE PHASE:
  hello → 2
  world → 1

Output: hello:2, world:1
```

**Limitations**:
- High latency for iterative algorithms
- Disk I/O between stages
- Complex programming model

### YARN (Yet Another Resource Negotiator)

**Purpose**: Resource management and job scheduling.

**Components**:
| Component | Function |
|-----------|----------|
| ResourceManager | Global resource allocation |
| NodeManager | Per-node resource management |
| ApplicationMaster | Per-application coordination |
| Container | Resource allocation unit |

### Hadoop Ecosystem Components

#### Hive

**Purpose**: SQL-like queries on Hadoop data.

**Features**:
- HiveQL (SQL-like language)
- Schema-on-read
- JDBC/ODBC connectivity
- Supports partitioning and bucketing

**Example Query**:
```sql
SELECT department, COUNT(*) as emp_count
FROM employees
WHERE salary > 50000
GROUP BY department
ORDER BY emp_count DESC;
```

#### Pig

**Purpose**: Data flow language for ETL operations.

**Characteristics**:
- Pig Latin language
- High-level scripting
- Translates to MapReduce jobs

**Example Script**:
```pig
-- Load data
employees = LOAD '/user/data/employees.csv'
            USING PigStorage(',')
            AS (id:int, name:chararray, dept:chararray, salary:float);

-- Filter
high_salary = FILTER employees BY salary > 50000;

-- Group and count
dept_count = GROUP high_salary BY dept;
result = FOREACH dept_count GENERATE group, COUNT(high_salary);

-- Store result
STORE result INTO '/user/output/dept_count';
```

#### HBase

**Purpose**: NoSQL column-family database on HDFS.

**Characteristics**:
- Real-time read/write access
- Column-oriented storage
- Automatic sharding
- Strong consistency

**Use Cases**:
- Time-series data
- Messaging systems
- Recommendation engines

#### Sqoop

**Purpose**: Transfer data between Hadoop and relational databases.

**Operations**:
```bash
# Import from RDBMS to HDFS
sqoop import --connect jdbc:mysql://server/db \
             --table employees \
             --target-dir /user/hdfs/employees

# Export from HDFS to RDBMS
sqoop export --connect jdbc:mysql://server/db \
             --table employees \
             --export-dir /user/hdfs/employees
```

#### Flume

**Purpose**: Collect and transfer log data to HDFS.

**Architecture**:
```
[Source] → [Channel] → [Sink]
              │
          (Buffer)
```

**Use Cases**:
- Log aggregation
- Event streaming
- Real-time ingestion

#### Oozie

**Purpose**: Workflow scheduler for Hadoop jobs.

**Features**:
- Directed Acyclic Graph (DAG) of jobs
- Time-based and data-based triggers
- Supports MapReduce, Pig, Hive jobs

---

## 13.3 Data Processing

### Batch vs. Stream Processing

| Aspect | Batch Processing | Stream Processing |
|--------|-----------------|-------------------|
| Data Scope | Complete dataset | Continuous flow |
| Latency | Minutes to hours | Milliseconds to seconds |
| Use Case | Historical analysis | Real-time alerts |
| Examples | Daily reports, ETL | Fraud detection, monitoring |
| Tools | MapReduce, Hive | Spark Streaming, Flink |

### Apache Spark

**Purpose**: Fast, general-purpose distributed computing engine.

**Advantages over MapReduce**:
- In-memory processing (100x faster)
- Interactive queries
- Rich APIs (Scala, Python, Java, R)
- Unified engine for batch and streaming

**Spark Components**:
```
┌─────────────────────────────────────────────────┐
│               SPARK APPLICATIONS                │
├──────────┬──────────┬──────────┬───────────────┤
│  Spark   │  Spark   │  MLlib   │   GraphX      │
│   SQL    │Streaming │   (ML)   │   (Graph)     │
├──────────┴──────────┴──────────┴───────────────┤
│               SPARK CORE ENGINE                 │
│            (RDD, DataFrames, Datasets)         │
├─────────────────────────────────────────────────┤
│     Cluster Managers: Standalone | YARN | K8s   │
└─────────────────────────────────────────────────┘
```

**Spark Example (PySpark)**:
```python
from pyspark.sql import SparkSession

# Initialize Spark
spark = SparkSession.builder.appName("Example").getOrCreate()

# Load data
df = spark.read.csv("/data/employees.csv", header=True)

# Transform
result = df.filter(df.salary > 50000) \
           .groupBy("department") \
           .count()

# Show results
result.show()
```

### Apache Flink

**Purpose**: True stream processing engine with batch capabilities.

**Key Features**:
- Event-time processing
- Exactly-once semantics
- Low latency
- Stateful computations

### Apache Storm

**Purpose**: Real-time computation system.

**Characteristics**:
- Topology-based processing
- Spouts (data sources) and Bolts (processors)
- At-least-once processing
- Low latency

---

## 13.4 NoSQL Databases

### Introduction to NoSQL

**NoSQL (Not Only SQL)**: Databases designed for specific data models with flexible schemas.

### CAP Theorem

**Principle**: A distributed system can only guarantee two of three properties:

```
               Consistency
                   /\
                  /  \
                 /    \
                /  CA  \
               /________\
              /    |     \
             / CP  |  AP  \
            /      |       \
           /       |        \
   Partition      |     Availability
   Tolerance      |
```

**Properties**:
| Property | Description | Example |
|----------|-------------|---------|
| Consistency | All nodes see same data | Single-node databases |
| Availability | System always responds | Replicated systems |
| Partition Tolerance | Works despite network failures | Distributed systems |

### BASE vs. ACID

| ACID (Traditional) | BASE (NoSQL) |
|-------------------|--------------|
| Atomicity | Basically Available |
| Consistency | Soft state |
| Isolation | Eventually consistent |
| Durability | |

### NoSQL Database Types

#### Document Stores

**Examples**: MongoDB, CouchDB

**Structure**:
```json
{
  "_id": "emp001",
  "name": "John Smith",
  "department": "IT",
  "skills": ["Python", "SQL", "AWS"],
  "address": {
    "city": "Islamabad",
    "country": "Pakistan"
  }
}
```

**Use Cases**:
- Content management
- User profiles
- Catalogs

**Characteristics**:
- JSON/BSON documents
- Flexible schema
- Rich query language
- Nested data support

#### Key-Value Stores

**Examples**: Redis, DynamoDB, Amazon ElastiCache

**Structure**:
```
Key: "session:user123"
Value: "{"user": "john", "expires": "2024-01-15"}"

Key: "counter:pageviews"
Value: 42857
```

**Use Cases**:
- Session management
- Caching
- Real-time counters

**Characteristics**:
- Simplest NoSQL model
- Extremely fast lookups
- Limited query capabilities

#### Column-Family Stores

**Examples**: Apache Cassandra, HBase

**Structure**:
```
Row Key: user123
  Column Family: personal
    name: "John"
    email: "john@example.com"
  Column Family: activity
    last_login: "2024-01-10"
    page_views: 150
```

**Use Cases**:
- Time-series data
- Event logging
- Messaging platforms

**Characteristics**:
- Wide columns (billions)
- Distributed across clusters
- Tunable consistency

#### Graph Databases

**Examples**: Neo4j, Amazon Neptune, OrientDB

**Structure**:
```
(Person:John)-[:WORKS_IN]->(Department:IT)
(Person:John)-[:REPORTS_TO]->(Person:Sarah)
(Person:Sarah)-[:MANAGES]->(Project:DataMigration)
```

**Use Cases**:
- Social networks
- Fraud detection
- Recommendation engines

**Characteristics**:
- Nodes and relationships
- Pattern matching queries
- Traversal algorithms

### NoSQL Selection Guide

| Use Case | Best NoSQL Type | Reason |
|----------|-----------------|--------|
| Session storage | Key-Value | Fast access by key |
| User profiles | Document | Flexible schema, nested data |
| Time-series | Column-Family | Wide rows, time-ordered |
| Social networks | Graph | Relationships are primary |
| Product catalog | Document | Varied product attributes |
| Real-time analytics | Column-Family | Fast writes, aggregations |

---

## 13.5 Data Warehousing

### Data Warehouse Concepts

**Definition**: Central repository for integrated data from multiple sources, optimized for analysis.

**Characteristics**:
- Subject-oriented
- Integrated
- Time-variant
- Non-volatile

### OLTP vs. OLAP

| Aspect | OLTP | OLAP |
|--------|------|------|
| Purpose | Transactions | Analysis |
| Data | Current | Historical |
| Queries | Simple, frequent | Complex, ad-hoc |
| Users | Many (clerks) | Few (analysts) |
| Updates | Real-time | Batch |
| Design | Normalized | Denormalized |

### Star Schema

**Structure**:
```
                           ┌──────────────┐
                           │   DIM_TIME   │
                           │ time_id (PK) │
                           │ date         │
                           │ month        │
                           │ quarter      │
                           │ year         │
                           └──────┬───────┘
                                  │
┌──────────────┐           ┌──────▼───────┐           ┌──────────────┐
│ DIM_PRODUCT  │           │  FACT_SALES  │           │ DIM_LOCATION │
│ prod_id (PK) │◄──────────│ time_id (FK) │──────────►│ loc_id (PK)  │
│ name         │           │ prod_id (FK) │           │ city         │
│ category     │           │ loc_id (FK)  │           │ region       │
│ brand        │           │ cust_id (FK) │           │ country      │
└──────────────┘           │ quantity     │           └──────────────┘
                           │ amount       │
                           │ discount     │
┌──────────────┐           └──────┬───────┘
│ DIM_CUSTOMER │                  │
│ cust_id (PK) │◄─────────────────┘
│ name         │
│ segment      │
└──────────────┘
```

**Characteristics**:
- Central fact table
- Surrounding dimension tables
- Simple joins
- Optimized for queries

### Snowflake Schema

**Definition**: Normalized version of star schema with dimension tables split into multiple related tables.

**Example**:
```
DIM_PRODUCT
    └── DIM_CATEGORY
            └── DIM_BRAND
```

**Advantages**:
- Reduced data redundancy
- Easier maintenance of dimension data

**Disadvantages**:
- More complex queries
- Additional joins

### ETL Process

**ETL (Extract, Transform, Load)**:

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   EXTRACT   │ ──► │  TRANSFORM  │ ──► │    LOAD     │
│ Source data │     │ Clean, map, │     │ Target DW   │
│             │     │ aggregate   │     │             │
└─────────────┘     └─────────────┘     └─────────────┘
```

**Stages**:
1. **Extract**: Pull data from sources (databases, files, APIs)
2. **Transform**: Clean, validate, convert, aggregate
3. **Load**: Insert into data warehouse

### Data Lakes vs. Data Warehouses

| Aspect | Data Lake | Data Warehouse |
|--------|-----------|----------------|
| Data Type | Raw, all formats | Processed, structured |
| Schema | Schema-on-read | Schema-on-write |
| Users | Data scientists | Business analysts |
| Processing | Varies | Optimized for queries |
| Cost | Lower storage cost | Higher for structured |
| Agility | High | Lower |

---

## 13.6 Analytics & Visualization

### Types of Analytics

| Type | Question | Example |
|------|----------|---------|
| Descriptive | What happened? | Monthly sales report |
| Diagnostic | Why did it happen? | Root cause analysis |
| Predictive | What will happen? | Sales forecast |
| Prescriptive | What should we do? | Inventory optimization |

### Visualization Tools

**Business Intelligence Platforms**:
| Tool | Strengths |
|------|-----------|
| Tableau | Visual analytics, dashboards |
| Power BI | Microsoft integration, cost-effective |
| QlikView | Associative data model |
| Looker | Data modeling, embedded analytics |

### Real-Time Analytics

**Use Cases**:
- Fraud detection
- Network monitoring
- Customer behavior tracking
- IoT sensor analysis

**Technologies**:
- Apache Kafka
- Apache Druid
- ClickHouse
- TimescaleDB

---

## 13.7 Machine Learning Basics

### Machine Learning Overview

**Definition**: Systems that learn from data to make predictions or decisions.

### Learning Types

#### Supervised Learning

**Definition**: Learning from labeled training data.

**Types**:
| Type | Output | Examples |
|------|--------|----------|
| Classification | Categories | Spam detection, image recognition |
| Regression | Continuous values | Price prediction, demand forecasting |

**Common Algorithms**:
- Linear Regression
- Logistic Regression
- Decision Trees
- Random Forests
- Support Vector Machines (SVM)
- Neural Networks

#### Unsupervised Learning

**Definition**: Finding patterns in unlabeled data.

**Types**:
| Type | Purpose | Examples |
|------|---------|----------|
| Clustering | Group similar items | Customer segmentation |
| Dimensionality Reduction | Reduce features | PCA, t-SNE |
| Association | Find relationships | Market basket analysis |

**Common Algorithms**:
- K-Means Clustering
- Hierarchical Clustering
- Principal Component Analysis (PCA)
- Apriori Algorithm

#### Reinforcement Learning

**Definition**: Learning through trial and error with rewards.

**Components**:
- Agent: Learner making decisions
- Environment: System agent interacts with
- Actions: What agent can do
- Rewards: Feedback on actions

**Use Cases**:
- Game playing (AlphaGo)
- Robotics
- Autonomous vehicles

### Key ML Concepts

#### Training and Testing

```
Original Data
     │
     ├── Training Set (70-80%)
     │       │
     │       └── Train Model
     │
     └── Test Set (20-30%)
             │
             └── Evaluate Model
```

#### Overfitting vs. Underfitting

| Issue | Description | Solution |
|-------|-------------|----------|
| Overfitting | Model memorizes training data | More data, regularization |
| Underfitting | Model too simple | More features, complex model |

### Deep Learning

**Definition**: Neural networks with many layers.

**Architectures**:
| Type | Use Case |
|------|----------|
| CNN (Convolutional Neural Networks) | Image recognition |
| RNN (Recurrent Neural Networks) | Sequential data, text |
| LSTM | Long sequences, time series |
| Transformers | NLP, language models |
| GAN (Generative Adversarial Networks) | Image generation |

### Natural Language Processing (NLP)

**Tasks**:
- Text classification
- Named Entity Recognition (NER)
- Sentiment analysis
- Machine translation
- Question answering
- Chatbots

**Techniques**:
- Tokenization
- Stemming and Lemmatization
- Word embeddings (Word2Vec, GloVe)
- Large Language Models (LLMs)

---

## 13.8 Internet of Things (IoT)

### IoT Architecture

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   DEVICES   │ ──► │  GATEWAYS   │ ──► │    CLOUD    │ ──► │ APPLICATIONS│
│  Sensors,   │     │ Aggregate,  │     │ Process,    │     │ Dashboards, │
│  Actuators  │     │ Filter      │     │ Store       │     │ Analytics   │
└─────────────┘     └─────────────┘     └─────────────┘     └─────────────┘
```

### IoT Protocols

| Protocol | Use Case | Characteristics |
|----------|----------|-----------------|
| MQTT | Messaging | Lightweight, pub/sub |
| CoAP | Constrained devices | REST-like, UDP |
| AMQP | Enterprise messaging | Reliable, queued |
| HTTP/REST | Web integration | Standard, overhead |
| LoRaWAN | Long range IoT | Low power, wide area |

### IoT Government Applications

| Domain | Application |
|--------|-------------|
| Smart Cities | Traffic management, street lighting |
| Agriculture | Soil monitoring, irrigation |
| Healthcare | Patient monitoring, asset tracking |
| Environment | Air quality, water management |
| Infrastructure | Bridge monitoring, utility meters |

### Edge Computing

**Definition**: Processing data near the source rather than in centralized cloud.

**Benefits**:
- Reduced latency
- Bandwidth savings
- Privacy preservation
- Offline capability

**Edge vs. Cloud**:
| Processing | Location | Latency | Best For |
|------------|----------|---------|----------|
| Edge | Near device | Low | Real-time decisions |
| Fog | Intermediate | Medium | Aggregation |
| Cloud | Centralized | Higher | Complex analytics |

---

## 13.9 Blockchain

### Blockchain Fundamentals

**Definition**: Distributed ledger technology with immutable, cryptographically linked blocks.

**Structure**:
```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Block 1   │ ──► │   Block 2   │ ──► │   Block 3   │
│ Hash: 0A2F  │     │ Hash: 7B3E  │     │ Hash: 9C4D  │
│ Prev: 0000  │     │ Prev: 0A2F  │     │ Prev: 7B3E  │
│ Nonce: 2847 │     │ Nonce: 9134 │     │ Nonce: 4521 │
│ Data: ...   │     │ Data: ...   │     │ Data: ...   │
└─────────────┘     └─────────────┘     └─────────────┘
```

### Consensus Mechanisms

| Mechanism | Description | Examples |
|-----------|-------------|----------|
| Proof of Work (PoW) | Computational puzzle solving | Bitcoin |
| Proof of Stake (PoS) | Stake-based validation | Ethereum 2.0 |
| Delegated PoS | Elected validators | EOS |
| Practical BFT | Byzantine fault tolerance | Hyperledger Fabric |

### Smart Contracts

**Definition**: Self-executing contracts with terms directly written in code.

**Characteristics**:
- Automated execution
- Immutable once deployed
- Transparent and auditable
- Reduce intermediaries

### Blockchain Types

| Type | Access | Governance | Use Case |
|------|--------|------------|----------|
| Public | Open | Decentralized | Cryptocurrency |
| Private | Restricted | Centralized | Enterprise |
| Consortium | Limited parties | Shared | Industry networks |

### Government Blockchain Use Cases

| Application | Benefit |
|-------------|---------|
| Land registry | Tamper-proof records |
| Voting systems | Transparent, verifiable |
| Supply chain | Traceability |
| Identity management | Secure credentials |
| Public procurement | Transparent bidding |

---

## 13.10 Data Mining

### Data Mining Process

**CRISP-DM (Cross-Industry Standard Process)**:
```
┌─────────────────────────────────────────────────┐
│  Business Understanding ◄─► Data Understanding  │
│         ↓                         ↓             │
│  Data Preparation         Modeling              │
│         ↓                         ↓             │
│         └──────► Evaluation ◄─────┘             │
│                      ↓                          │
│                 Deployment                      │
└─────────────────────────────────────────────────┘
```

### Data Mining Techniques

#### Association Rule Mining

**Purpose**: Find relationships between items.

**Example (Market Basket Analysis)**:
```
Rule: {bread, butter} → {milk}
Support: 5% (5% of transactions contain all items)
Confidence: 80% (80% who bought bread+butter also bought milk)
Lift: 2.5 (2.5x more likely than random)
```

#### Classification

**Purpose**: Categorize data into predefined classes.

**Algorithms**:
- Decision Trees
- Naive Bayes
- K-Nearest Neighbors
- Neural Networks

#### Clustering

**Purpose**: Group similar data points.

**Algorithms**:
- K-Means
- DBSCAN
- Hierarchical Clustering

---

## Hands-On Labs

### Lab 13.1: NoSQL Database Selection

**Scenario**: Select appropriate database for each government use case.

| Use Case | Recommendation | Justification |
|----------|----------------|---------------|
| Citizen identity records | Document Store (MongoDB) | Varied attributes, nested data |
| Session management for portal | Key-Value (Redis) | Fast lookups by session key |
| Social welfare connections | Graph Database (Neo4j) | Family relationships important |
| Sensor data from smart meters | Column-Family (Cassandra) | Time-series, high write volume |

### Lab 13.2: Star Schema Design

**Scenario**: Design a star schema for government procurement analysis.

**Solution**:
```
FACT_PROCUREMENT
- procurement_id (PK)
- date_id (FK)
- vendor_id (FK)
- department_id (FK)
- category_id (FK)
- amount
- quantity
- status

DIM_DATE
- date_id (PK)
- date
- month
- quarter
- fiscal_year

DIM_VENDOR
- vendor_id (PK)
- vendor_name
- vendor_type
- registration_no

DIM_DEPARTMENT
- department_id (PK)
- department_name
- ministry
- province

DIM_CATEGORY
- category_id (PK)
- category_name
- category_type
```

### Lab 13.3: IoT Architecture Design

**Scenario**: Design IoT architecture for smart city traffic management.

**Solution**:
```
Edge Layer:
  - Traffic sensors (cameras, inductive loops)
  - Smart traffic lights
  - Edge gateways for local processing

Communication:
  - LoRaWAN for sensors
  - 4G/5G for high-bandwidth (cameras)
  - MQTT protocol

Processing:
  - Edge: Real-time light control
  - Cloud: Pattern analysis, optimization

Applications:
  - Traffic control center dashboard
  - Citizen mobile app (congestion info)
  - Emergency vehicle priority system
```

---

## Chapter Summary

- **Big Data** is characterized by 5 V's: Volume, Velocity, Variety, Veracity, and Value
- **Hadoop Ecosystem** provides distributed storage (HDFS) and processing (MapReduce, Spark)
- **Batch Processing** handles historical data; **Stream Processing** handles real-time data
- **NoSQL Databases** include Document, Key-Value, Column-Family, and Graph types
- **CAP Theorem**: Distributed systems can only guarantee 2 of 3 properties (Consistency, Availability, Partition Tolerance)
- **Data Warehousing** uses star and snowflake schemas for analytical queries (OLAP)
- **Machine Learning** includes supervised, unsupervised, and reinforcement learning
- **IoT** connects devices through sensors, gateways, and cloud processing
- **Blockchain** provides immutable, distributed ledgers with consensus mechanisms

---

## Multiple Choice Questions

### Beginner Level

1. Which of the following is NOT one of the 5 V's of Big Data?
   - A) Volume
   - B) Velocity
   - C) Visibility
   - D) Veracity

   **Answer: C**
   *Explanation: The 5 V's are Volume, Velocity, Variety, Veracity, and Value. Visibility is not one of them.*

2. HDFS stores data in:
   - A) Single centralized server
   - B) Distributed blocks across multiple nodes
   - C) Memory only
   - D) External cloud storage

   **Answer: B**
   *Explanation: HDFS distributes data in blocks (default 128MB) across multiple DataNodes with replication.*

3. Which NoSQL database type is BEST for storing user sessions?
   - A) Document Store
   - B) Key-Value Store
   - C) Column-Family Store
   - D) Graph Database

   **Answer: B**
   *Explanation: Key-Value stores provide fast lookup by key, ideal for session storage.*

4. In a star schema, the central table is called:
   - A) Dimension table
   - B) Fact table
   - C) Lookup table
   - D) Junction table

   **Answer: B**
   *Explanation: The star schema has a central fact table surrounded by dimension tables.*

5. Which processing type is BEST for real-time fraud detection?
   - A) Batch processing
   - B) Stream processing
   - C) Manual processing
   - D) Scheduled processing

   **Answer: B**
   *Explanation: Stream processing provides low-latency, real-time analysis needed for fraud detection.*

### Intermediate Level

6. According to CAP theorem, which two properties does Cassandra prioritize?
   - A) Consistency and Availability
   - B) Availability and Partition Tolerance
   - C) Consistency and Partition Tolerance
   - D) All three equally

   **Answer: B**
   *Explanation: Cassandra prioritizes Availability and Partition Tolerance, with tunable consistency (AP system).*

7. Which component of Hadoop is responsible for resource management?
   - A) HDFS
   - B) MapReduce
   - C) YARN
   - D) Hive

   **Answer: C**
   *Explanation: YARN (Yet Another Resource Negotiator) manages resources and job scheduling in Hadoop.*

8. What type of machine learning uses labeled training data?
   - A) Supervised learning
   - B) Unsupervised learning
   - C) Reinforcement learning
   - D) Semi-supervised learning

   **Answer: A**
   *Explanation: Supervised learning trains models using labeled data (input-output pairs).*

9. In blockchain, a consensus mechanism ensures:
   - A) Data encryption
   - B) Agreement on valid transactions
   - C) Network speed
   - D) User authentication

   **Answer: B**
   *Explanation: Consensus mechanisms ensure all nodes agree on valid transactions and block creation.*

10. Which IoT protocol is specifically designed for low-power, constrained devices?
    - A) HTTP
    - B) CoAP
    - C) FTP
    - D) SMTP

    **Answer: B**
    *Explanation: CoAP (Constrained Application Protocol) is designed for constrained IoT devices with limited resources.*

### Advanced Level

11. In MapReduce, which phase combines intermediate results with the same key?
    - A) Map
    - B) Shuffle and Sort
    - C) Reduce
    - D) Partition

    **Answer: B**
    *Explanation: Shuffle and Sort groups intermediate key-value pairs by key before the reduce phase.*

12. A retail company wants to analyze product purchase patterns. Which data mining technique is MOST appropriate?
    - A) Classification
    - B) Clustering
    - C) Association rule mining
    - D) Regression

    **Answer: C**
    *Explanation: Association rule mining discovers relationships between items (market basket analysis).*

13. What differentiates a snowflake schema from a star schema?
    - A) Snowflake has no fact table
    - B) Snowflake normalizes dimension tables
    - C) Star schema has more tables
    - D) Snowflake cannot handle large data

    **Answer: B**
    *Explanation: Snowflake schema normalizes dimension tables, splitting them into multiple related tables.*

14. Which deep learning architecture is BEST suited for image classification?
    - A) RNN
    - B) CNN
    - C) LSTM
    - D) Autoencoder

    **Answer: B**
    *Explanation: CNNs (Convolutional Neural Networks) are specifically designed for image processing and recognition.*

15. What is the PRIMARY advantage of edge computing in IoT?
    - A) Lower device cost
    - B) Reduced latency
    - C) Simpler programming
    - D) More storage capacity

    **Answer: B**
    *Explanation: Edge computing processes data near the source, significantly reducing latency for real-time decisions.*

16. In Spark, which abstraction provides distributed collection with optimizations?
    - A) RDD
    - B) DataFrame
    - C) Array
    - D) List

    **Answer: B**
    *Explanation: DataFrames in Spark provide distributed collections with schema and optimizations through Catalyst optimizer.*

17. Which statement about public vs. private blockchain is TRUE?
    - A) Public blockchains are faster
    - B) Private blockchains are fully decentralized
    - C) Private blockchains have controlled access
    - D) Public blockchains are more suitable for enterprise

    **Answer: C**
    *Explanation: Private blockchains restrict participation to authorized members with controlled access.*

18. A model performs well on training data but poorly on test data. This indicates:
    - A) Underfitting
    - B) Overfitting
    - C) Proper fit
    - D) Insufficient features

    **Answer: B**
    *Explanation: Overfitting occurs when the model memorizes training data but fails to generalize to new data.*

19. Which Hadoop component would you use to transfer data from Oracle to HDFS?
    - A) Flume
    - B) Sqoop
    - C) Oozie
    - D) Pig

    **Answer: B**
    *Explanation: Sqoop is designed for transferring data between Hadoop and relational databases like Oracle.*

20. In ETL, the "Transform" phase typically includes:
    - A) Only data loading
    - B) Only data extraction
    - C) Cleaning, validation, and aggregation
    - D) Database connection only

    **Answer: C**
    *Explanation: Transform phase includes data cleaning, validation, conversion, and aggregation operations.*

---

## References and Further Reading

1. "Hadoop: The Definitive Guide" by Tom White
2. "Learning Spark" by Holden Karau et al.
3. "NoSQL Distilled" by Martin Fowler
4. "The Data Warehouse Toolkit" by Ralph Kimball
5. Apache Hadoop Documentation - hadoop.apache.org
6. Apache Spark Documentation - spark.apache.org
7. "Designing Data-Intensive Applications" by Martin Kleppmann
8. NIST Big Data Interoperability Framework

---

*Chapter 13 completed. Big Data technologies enable organizations to extract value from vast amounts of information, supporting data-driven decision-making in government operations.*
