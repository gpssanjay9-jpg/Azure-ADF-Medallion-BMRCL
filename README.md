# Multi-Stage Azure Transit Data Pipeline (Medallion Architecture)

## 📌 Project Overview
This project implements a production-grade **Medallion Architecture** using **Azure Data Factory (ADF)** to process high-velocity transit telemetry from the **OpenCity API**. The system transforms raw, unstructured JSON data into high-value insights for urban transit cost-feasibility modeling, optimized for **Azure Synapse Analytics**.

By utilizing a three-tier data lake strategy (Bronze → Silver → Gold), this project ensures data lineage, reliability, and high-performance querying for large-scale transportation datasets.

---

## 🖼️ Visualizing the Pipeline

### Master Orchestration Pipeline
The master pipeline mechanizes the dependency chain, ensuring the Silver layer only begins after a successful Bronze ingestion, and the Gold layer only processes validated Silver data.
![Master Pipeline](sample/EXC%20PIPELINE.png)

### Peak Hour Analytics Data Flow
Detailed view of the transformation logic. This Spark-based Data Flow utilizes multiple **Window Functions**, **Filters**, and **Aggregations** to identify peak-hour bottlenecks and transit performance metrics.
![Data Flow Logic](sample/GOLD.png)

---

## 📊 Data Evolution & Sample Outputs
The `/sample` folder contains the direct outputs from each stage of the pipeline, demonstrating the data maturation process:

* **Bronze Output (Raw):** See `sample/bronze_output.json`. This represents the raw, nested API response captured from the OpenCity endpoint, preserved for 100% auditability.
* **Silver Output (Cleaned):** See `sample/silver_output.csv`. This file shows the flattened and schema-enforced data, where timestamps are standardized and nulls are handled.
* **Gold Output (Analytics-Ready):** See `sample/gold_output.csv`. This final curated dataset contains computed Peak Hour (PEAKHR) metrics, ready for ingestion into **Azure Synapse Analytics**.

---

## 🛠️ Technical Stack & Skills
* **Orchestration:** Azure Data Factory (Master Pipeline with ExecutePipeline dependencies).
* **Storage/Compute:** Azure Data Lake Gen2, Azure Synapse Analytics, Microsoft Fabric (OneLake).
* **Version Control:** Native **Git Integration** (ADF-to-GitHub) for CI/CD readiness.
* **Transformation:** Advanced SQL (Stored Procedures) and Spark-based Mapping Data Flows.

---

## ⚙️ Reliability & Performance Tuning
To meet enterprise-grade **SLA requirements**, the following features were implemented:
* **Fault Tolerance:** Mechanized retry policies (30-second intervals) for API ingestion.
* **SLA Optimization:** Optimized SQL extraction logic, contributing to a **35% reduction** in processing latency.
* **Governance:** Enforced security via Linked Services and computerized validation gates for data compliance.

---

## 📂 Repository Structure
```text
├── pipeline/      # JSON definitions for Bronze, Silver, Gold & Master Orchestrator
├── dataflow/      # Transformation logic (Mapping Data Flows)
├── dataset/       # Source (REST) and Sink (JSON/Synapse) metadata
├── sample/        # Output files (JSON/CSV) and architecture visuals
└── README.md      # Project documentation
