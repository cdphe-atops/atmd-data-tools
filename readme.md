# atmd-data-tools

## CDPHE Air Toxics Public Data Lake

This repository provides tools and examples for accessing Colorado's Air Toxics Monitoring Data via a serverless public data lake. This project serves to demonstrate how researchers, citizens, and partner agencies can query high-resolution air quality data without managing complex infrastructure.

---

## 📂 Repository Structure

- `catalog.csv`: An archived human-readable index of all available datasets, sites, and deployment dates.
- `notebooks/`:
  - `01_getting_started.ipynb`: A step-by-step guide to querying the S3 bucket using DuckDB.
- `requirements.txt`: Python dependencies required to run the tools.

---

## 🚀 Getting Started

### 1. Installation

This project requires Python 3.9+. We recommend using a virtual environment (venv) or Conda.

**Using Pip:**

```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

**Using Conda:**

```bash
conda create --name atmd-data-tools
conda activate atmd-data-tools
pip install -r requirements.txt
```

### 2. Accessing the Data

The data is hosted in a public S3 bucket: `s3://cdphe-atmd-datalake-public/`
**No AWS credentials are required for access.**

To see the data in action, launch the Jupyter notebook:

```bash
jupyter notebook notebooks/01_getting_started.ipynb
```

## Data Architecture

The data lake is organized using the Hive Partitioning strategy to optimize query performance and minimize data transfer costs.

Path Structure:
`s3://cdphe-atmd-datalake-public/data/asset={ID}/deployment={DATE}/part-0.parquet`

- Asset: The monitoring equipment or program (e.g., `CAT`, `MARMOT-Millie`)
- Deployment: The specific date the data was collected (e.g., `2024-12-18`)
- Format: Apache Parquet (Columnar storage with predicate pushdown support)
