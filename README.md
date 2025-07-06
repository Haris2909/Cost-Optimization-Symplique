# Cost-Optimization-Symplique
Azure-Cost-Optimization-Symplique
# Azure Cost Optimization - Serverless Architecture

This project is a solution to the **Cost Optimization Challenge** for managing billing records in Azure Cosmos DB using serverless architecture.

---

## 🧠 Problem Statement

We have a workload architecture in Azure, where one of our services stores billing records in **Azure Cosmos DB**. The system is moderately busy, but records older than three months are rarely accessed.

Due to data growth and infrequent access to old data, cost is increasing. We need a solution to **optimize costs without compromising on performance**.

---

## 🚧 Current System Constraints

1. Each record can be as large as **10KB**
2. The database holds **over 2 million records**
3. **Low-latency reads** are required for recent records

---

## ✅ Solution Approach

### 🔹 1. Simplicity
Used **Azure Functions** and **Cosmos DB (Serverless)** with **Blob Storage** for archiving.

### 🔹 2. No Storage Bloat
- Recent records (90 days) remain in Cosmos DB
- Older records archived to Blob Storage via Azure Data Factory or Timer Trigger

### 🔹 3. No Changes to API Contract
- APIs continue to fetch from Cosmos DB for recent records
- For archived data, fallback query from Blob Storage is introduced

---

## 🔄 Data Flow

```mermaid
graph TD;
  A[Client API] --> B[Azure Function];
  B --> C[Cosmos DB (Hot Data)];
  B -->|If not found| D[Blob Storage (Archived)];
