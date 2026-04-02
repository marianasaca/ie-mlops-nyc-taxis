# NYC Airbnb Price Prediction — End-to-End MLOps Pipeline

An end-to-end MLOps project that predicts nightly Airbnb listing prices in New York City, covering every stage from exploratory analysis through deployment, monitoring, and CI/CD.

**Author:** Mariana Saca
**Context:** Master in Business Analytics & Data Science, IE University

---

## Project Overview

Setting the right nightly price is one of the hardest decisions for Airbnb hosts. This project builds a machine learning pipeline that predicts listing prices using features like neighborhood, room type, availability, and review activity. Beyond the model itself, the focus is on **operationalizing** the workflow: experiment tracking with MLflow, serving predictions via a REST API, simulating live traffic for monitoring, containerizing with Docker, and automating quality checks with GitHub Actions.

### Dataset

[AB_NYC_2019.csv](http://insideairbnb.com/) — ~49,000 Airbnb listings in New York City with features including neighborhood group, room type, price, minimum nights, number of reviews, and availability.

---

## Pipeline Stages

The project is organized into sequential stages, each in its own directory:

| Stage | Directory | What It Does |
|---|---|---|
| **EDA** | `01-notebook/` | Exploratory data analysis — distributions, correlations, outlier detection |
| **Feature Engineering** | `02-features/` | Data cleaning, encoding, and feature creation |
| **Experiment Tracking** | `03-experiment-tracking/` | Model training with MLflow logging (parameters, metrics, artifacts) |
| **Deployment** | `04-deployment/` | FastAPI REST API that loads the trained model from MLflow |
| **Monitoring** | `05-monitoring/` | Simulates live predictions and generates an HTML monitoring report |
| **CI/CD** | `06-cicd/` | Dockerfile + GitHub Actions workflow (linting and syntax checks) |

---

## Quick Start

### Prerequisites

- Python 3.9+
- pip

### Setup

```bash
git clone https://github.com/marianasaca/mlops-nyc-airbnb.git
cd mlops-nyc-airbnb
pip install -r requirements.txt
```

### Train the Model

```bash
cd 04-deployment
python train.py
```

This trains the model, logs the experiment to MLflow, and writes a `run_id.txt` file that the API uses to load the correct model artifact.

### Start the API

```bash
cd 04-deployment
uvicorn app:app --reload
```

The API will be available at `http://localhost:8000`. Interactive docs are at `/docs`.

### Make a Prediction

Send a POST request to the `/predict` endpoint:

```bash
curl -X POST http://localhost:8000/predict \
  -H "Content-Type: application/json" \
  -d '{
    "neighbourhood_group": "Manhattan",
    "neighbourhood": "Harlem",
    "room_type": "Private room",
    "minimum_nights": 3,
    "number_of_reviews": 25,
    "availability_365": 200
  }'
```

> **Note:** Verify the exact field names and required inputs against `app.py` — adjust the example above if your schema differs.

### Run Monitoring

```bash
cd 05-monitoring
python simulate.py   # sends ~100 requests to the API, logs results to predictions.csv
python monitor.py    # generates an HTML monitoring report from logged predictions
```

### Run with Docker

```bash
cd 06-cicd
docker build -t airbnb-api .
docker run -p 8000:8000 airbnb-api
```

---

## Project Structure

```
mlops-nyc-airbnb/
├── 01-notebook/                 # Exploratory data analysis
├── 02-features/                 # Feature engineering scripts
├── 03-experiment-tracking/      # MLflow experiment tracking
├── 04-deployment/
│   ├── train.py                 # Train model, log to MLflow, write run_id.txt
│   ├── app.py                   # FastAPI app — loads model and serves /predict
│   └── test_api.py              # Optional API integration tests
├── 05-monitoring/
│   ├── simulate.py              # Simulate ~100 live prediction requests
│   ├── monitor.py               # Generate HTML monitoring report
│   └── data/
│       └── predictions.csv      # Logged prediction results
├── 06-cicd/
│   └── Dockerfile               # Docker image for the FastAPI service
├── .github/
│   └── workflows/
│       └── ci.yml               # GitHub Actions CI (lint + syntax checks)
├── data/
│   └── AB_NYC_2019.csv          # Airbnb NYC 2019 dataset
├── requirements.txt
└── README.md
```

---

## Tech Stack

- **ML & Data:** Python, Pandas, NumPy, Scikit-Learn
- **Experiment Tracking:** MLflow
- **API:** FastAPI, Uvicorn
- **Monitoring:** Custom HTML report (no external monitoring framework)
- **Containerization:** Docker
- **CI/CD:** GitHub Actions

---

## Things to Verify Before Pushing

A few details I couldn't confirm from the repo listing alone — double-check these match your actual code:

- [ ] **Model type** — is it Random Forest, Gradient Boosting, or something else? If you want to mention the algorithm and any key metrics (MAE, RMSE, R²), add a "Model Performance" section.
- [ ] **API request schema** — the curl example above is a guess based on common columns in AB_NYC_2019.csv. Verify the exact field names in `app.py`.
- [ ] **Python version** — I wrote 3.9+ but confirm against what you actually used.
- [ ] **Dataset path** — I assumed `data/AB_NYC_2019.csv` based on the original README. Confirm it lives there.
