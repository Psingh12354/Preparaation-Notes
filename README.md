
# 📘 Azure Databricks - Notes

Azure Databricks is an Apache Spark-based analytics platform optimized for Microsoft Azure. It is designed to provide fast, easy, and collaborative analytics and AI solutions.

---

## 🧰 Services Provided by Azure Databricks

| **Service**              | **Description**                                                                 |
|--------------------------|---------------------------------------------------------------------------------|
| **Apache Spark**         | Fully managed Spark clusters for large-scale data processing.                   |
| **Delta Lake**           | Storage layer with ACID transactions and scalable metadata handling.           |
| **MLflow**               | Open-source platform for managing the ML lifecycle (experiments, deployment).  |
| **Databricks SQL**       | Query data using familiar SQL syntax and create dashboards.                    |
| **Notebooks**            | Interactive workspace for collaborative data science and engineering tasks.    |
| **Databricks Runtime**   | Optimized Apache Spark environment with performance and reliability improvements. |

---

## 🖥️ Azure Databricks UI Overview

Azure Databricks provides a web-based UI that supports data engineers, data scientists, and analysts. The main components include:

### 1. **Workspace**
- Organizes notebooks, libraries, dashboards, and experiments.
- Supports folders and permissions.

### 2. **Notebooks**
- Language support: Python, SQL, Scala, R.
- Interactive and supports visualizations and markdown.

### 3. **Clusters**
- Launch and manage Apache Spark clusters.
- Choose Databricks Runtime version and scaling configuration.

### 4. **Jobs**
- Schedule and automate notebooks, JARs, or Python scripts.

### 5. **Libraries**
- Manage and attach Python, Maven, or CRAN libraries to clusters.

### 6. **SQL Editor & Dashboards**
- Query data using SQL.
- Build and share visual dashboards.

---

## 🏗️ Azure Databricks Architecture

```plaintext
+---------------------+       +----------------------+
| Azure Data Sources  | <---> |    Azure Databricks  |
| (Blob, ADLS, SQL DB)|       | (Workspace, Clusters)|
+---------------------+       +----------------------+
                                        |
                                        v
                          +---------------------------+
                          |     Apache Spark Engine   |
                          |  (Optimized via Runtime)  |
                          +---------------------------+
                                        |
                                        v
                          +---------------------------+
                          |     Delta Lake Storage    |
                          +---------------------------+
                                        |
                                        v
                          +---------------------------+
                          | MLflow / Notebooks / SQL  |
                          +---------------------------+

```

## 🔧 Key Components
Azure Databricks integrates several core components for scalable, secure, and collaborative data and AI workflows:

| **Component**              | **Description**                                                                                                                |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **Azure Integration**      | Connects easily to Azure services like Azure Data Lake Storage (ADLS), Azure SQL Database, Synapse Analytics, Event Hubs, etc. |
| **Compute (Clusters)**     | Managed, auto-scaling Apache Spark clusters that can be shared or ephemeral.                                                   |
| **Delta Lake**             | Storage layer that enables ACID transactions, schema enforcement, and time travel.                                             |
| **Databricks Runtime**     | Optimized Spark runtime that includes performance improvements and preinstalled libraries.                                     |
| **Security & Identity**    | Uses Azure Active Directory (AAD) for authentication and role-based access control (RBAC).                                     |
| **Machine Learning Tools** | Includes MLflow for experiment tracking, model versioning, and deployment.                                                     |

---------------

## ⚙️ Azure Databricks Clusters

A **cluster** in Azure Databricks is a set of computation resources and configurations on which you run **notebooks**, **jobs**, **libraries**, and **Spark applications**. Databricks clusters are fully managed, elastic, and support autoscaling.

---

### 🧱 Types of Clusters

| **Cluster Type**     | **Description**                                                                 |
|----------------------|----------------------------------------------------------------------------------|
| **Interactive Cluster** | Used for ad-hoc analysis, data exploration, and development in notebooks. Shared by users. |
| **Job Cluster**         | Automatically created to run a scheduled job or workflow, and terminated after the job completes. |
| **SQL Warehouse**       | Specialized for running SQL queries and dashboards. Optimized for BI tools like Power BI. |
| **Single Node Cluster** | Runs Spark locally with no worker nodes. Best for development, testing, and small workloads. |
| **Standard Cluster**    | Distributed Spark clusters with driver and worker nodes. Supports large-scale data processing. |

---

### 🔧 Cluster Configuration Options

When creating a cluster, you configure the following:

| **Setting**                      | **Description**                                                                 |
|----------------------------------|---------------------------------------------------------------------------------|
| **Cluster Name**                 | A name to identify the cluster.                                                |
| **Cluster Mode**                 | Choose between **Single Node** or **Standard** (multi-node Spark cluster).     |
| **Databricks Runtime Version**   | Preconfigured environment including Apache Spark, Delta Lake, ML libraries.    |
| **Node Type**                    | Virtual machine size (e.g., `Standard_DS3_v2`, `i3.xlarge`).                    |
| **Autoscaling**                  | Automatically adds/removes worker nodes based on workload.                     |
| **Min & Max Workers**            | Specify range if autoscaling is enabled.                                       |
| **Auto Termination**             | Automatically terminates the cluster after a set idle time.                    |
| **Spark Configs**                | Advanced Spark settings in key-value format (optional).                        |
| **Init Scripts**                 | Scripts to run on cluster startup (e.g., install packages).                    |
| **Libraries**                    | Attach Python packages, JARs, or Maven libraries.                              |
| **Tags**                         | Add metadata to manage and track usage/costs.                                  |

---

### 📌 Example: Basic Cluster Configuration (JSON)

```json
{
  "cluster_name": "data-engineering-cluster",
  "spark_version": "13.3.x-scala2.12",
  "node_type_id": "Standard_DS3_v2",
  "autoscale": {
    "min_workers": 2,
    "max_workers": 8
  },
  "autotermination_minutes": 30,
  "spark_conf": {
    "spark.databricks.delta.preview.enabled": "true"
  },
  "custom_tags": {
    "Project": "ETL Pipeline"
  }
}

