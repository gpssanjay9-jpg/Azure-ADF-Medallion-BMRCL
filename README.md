# Multi-Stage Azure Transit Data Pipeline (Medallion Architecture)

##  Project Overview
This project demonstrates a production-grade implementation of a **Medallion Architecture** using **Azure Data Factory (ADF)**. The system is engineered to ingest, process, and curate high-velocity transit telemetry from the **OpenCity API**, transforming raw JSON data into actionable insights for urban transit cost-feasibility modeling.

By utilizing a three-tier data lake strategy (Bronze → Silver → Gold), this project ensures high data quality, lineage transparency, and optimized performance for downstream analytics in **Azure Synapse Analytics**.

---

##  Data Architecture (Medallion Framework)

### 1. Bronze Layer (Ingestion)
* **Logic:** Mechanized raw data extraction from REST API endpoints.
* **Implementation:** Utilizes ADF **Copy Activity** with a `RestSource` to capture real-time telemetry.
* **Storage:** Data is persisted in **Azure Data Lake Storage (ADLS) Gen2** as raw JSON objects, preserving the original hierarchy for auditability.

### 2. Silver Layer (Transformation & Validation)
* **Logic:** Systematized data cleaning, schema enforcement, and deduplication.
* **Implementation:** Employs **ADF Mapping Data Flows** (Spark-based) with 8-core General Compute to standardize data types and filter noise.
* **Achievement:** Reduced raw data volatility, ensuring a 100% schema-compliant dataset for secondary analysis.

### 3. Gold Layer (Curation & Analytics)
* **Logic:** Aggregation and business-logic application.
* **Implementation:** Complex transformations curate the data into specialized transit-metric tables optimized for **Azure Synapse Analytics**.

---

##  Technical Stack & Skills
* **Orchestration:** Azure Data Factory (Master Pipeline with ExecutePipeline dependencies).
* **Storage/Compute:** Azure Data Lake Gen2, Azure Synapse Analytics, Microsoft Fabric (OneLake).
* **Version Control:** Native **Git Integration** within ADF for mechanized code deployments.
* **DevOps:** CI/CD ready structure with JSON definitions for all resource artifacts.
* **Transformation:** Advanced SQL (Stored Procedures) and Spark-based Mapping Data Flows.

---

##  Reliability & Performance Tuning
To meet enterprise-grade **SLA requirements**, the following features were implemented:
* **Fault Tolerance:** Mechanized retry policies (30-second intervals) for API ingestion.
* **SLA Optimization:** Optimized SQL extraction logic, contributing to a **35% reduction** in processing latency.
* **Data Governance:** Enforced security and compliance standards by managing access via Linked Services.
* **Observability:** Centralized monitoring of pipeline health to troubleshoot and resolve failures in real-time.

---

##  Repository Structure
```text
├── pipeline/      # JSON definitions for Bronze, Silver, Gold & Master Orchestrator
├── dataflow/      # Transformation logic (Mapping Data Flows)
├── dataset/       # Source (REST) and Sink (JSON/Synapse) metadata
├── linkedService/ # Connection configurations (ADLS, API, Synapse)
└── README.md      # Project documentation and architectural overview
