# AzureProjectWithCICD
# 🏅 Azure Data Engineering Project – Paris Olympics 2024

This end-to-end Azure Data Engineering project demonstrates how to build a real-world solution for ingesting and processing data using Azure Data Factory, Azure Data Lake, and Azure Databricks — with CI/CD pipelines using **GitHub**.

## 📂 Project Structure

📁 Resources
├── Source
│ ├── athletes.csv
│ ├── coaches.csv
│ ├── events.csv
│ └── NOCs.csv
└── Config
└── github_files_config.json

markdown
Copy
Edit

---

## ✅ Project Steps

### 1️⃣ Azure Environment Setup

- Created a **Resource Group** to manage all related services.
- Created an **Azure Data Lake Storage Gen2** with containers:
  - `source`
  - `bronze`
- Created **Azure Data Factory (ADF)** as the orchestration tool.
- Connected ADF to **GitHub** for version control.

---

### 2️⃣ Bronze Layer – Data Ingestion (ADF)

#### Pipeline 1: `get-to-bronze`

This pipeline:
- Reads a **JSON config** file from Data Lake (`source` container) that contains GitHub file info.
- Uses ADF activities:
  - `Lookup`: Reads the config.
  - `ForEach`: Loops through each file entry.
  - `Copy Data`: Downloads CSVs from GitHub and saves as **Parquet** to the `bronze` container.

✅ JSON Sample:
```json
[
  {
    "url": "https://raw.githubusercontent.com/anshlambagit/AzureProjectWithCICD/main/Resources/Source/coaches.csv",
    "name": "coaches"
  },
  ...
]
Pipeline 2: data-lake-injection
This pipeline:

Validates and loads NOCs.csv from the source container to bronze with rules:

File name = NOCs.csv

Column count = 5

Uses:

Get Metadata

If Condition

Copy Data
