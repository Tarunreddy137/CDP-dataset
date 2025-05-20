# 🧱 JSON to Structured CSV Pipeline

This repository demonstrates a complete data pipeline that transforms **unstructured JSON data** into **structured CSV output**, following a modular and production-ready architecture.

---

## 🧭 Architecture Overview


### 1. **Raw Files**
- Location: `data/raw/samplefile.json`
- The JSON contains multiple nested events from a customer activity dataset.
- Fields include: `eventType`, `personKey`, `timestamp`, `web`, `listOperations`, etc.

---

### 2. **Ingestion**
- Reads the JSON file into memory.
- Uses Python's `json` module to parse the file.
- Target Path: `scripts/extract/extract_json.py`

```python
import json

def ingest_json(filepath):
    with open(filepath, 'r') as f:
        return json.load(f)

### 3. **Processing**
- Flattens nested fields from each record:
  - `eventType`
  - `timestamp`
  - `sourceID`
  - `listKey`
  - `webPageDetails`
  - `geo location`, etc.
- Converts nested records into a flat tabular format (rows and columns).

### 4. **Validation**
- Ensures required fields are present (e.g., `eventType`, `timestamp`).
- Optional checks:
  - Null/missing value detection.
  - Timestamp formatting.
  - ID consistency.

### 5. **Storage**
- Saves the final structured DataFrame into CSV format.
- CSV stored in the `data/processed/` directory.
- Optional: load into SQLite or other RDBMS.

### 6. **Output**
- Final output: Cleaned and structured CSV file.
- Ready for use in analytics, dashboards, or downstream ETL tools.

---

## ▶️ How to Run

1. Place your unstructured JSON file inside `data/raw/`.
2. Run the pipeline:

```bash
python pipeline_runner.py

### Directory Structure ###
project-root/
├── data/
│   ├── raw/
│   │   └── samplefile.json
│   └── processed/
│       └── cleaned_data.csv
├── scripts/
│   ├── extract/
│   │   └── extract_json.py
│   ├── transform/
│   │   └── clean_transform.py
│   ├── validate/
│   │   └── validate.py
│   └── load/
│       └── load_to_csv.py
├── pipeline_runner.py
└── README.md

