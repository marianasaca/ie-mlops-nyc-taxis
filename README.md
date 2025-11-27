# 🚕 NYC Taxi Trip Duration – MLOps Pipeline

This project implements a full **end-to-end MLOps workflow** for predicting NYC taxi trip durations.  
It covers the complete machine learning lifecycle — from experimentation to deployment, monitoring, and CI/CD automation — following industry standards and best practices.

This project was completed as part of an MLOps module in the IE Master’s in Business Analytics & Big Data.

---

### 🚀 Live Demo  
You can interact with the deployed model here:  
👉 **https://ie-mlops-nyc-taxis-98u4.onrender.com/docs**  
*(Hosted via Render — may take ~20 seconds to wake up if idle.)*


## 📌 Project Overview

The goal of this project is to:

- Build and track machine learning experiments  
- Create modular, reproducible training pipelines  
- Deploy a model as a service  
- Monitor model performance over time  
- Automate workflows using CI/CD  
- Apply modern MLOps tooling and engineering practices

The project uses the **NYC Taxi Trip Duration dataset** and predicts how long a taxi trip will take based on pickup/dropoff metadata, location features, and engineerd variables.

---

## 🧱 Architecture & Workflow

This repository follows a **modular folder structure**, aligned with each MLOps stage:

ie-mlops-nyc-taxis/
│
├── 01-initial-notebook/ # Exploratory analysis, baseline model
├── 02-data-sampling-features/ # Feature engineering and dataset preparation
├── 03-experiment-tracking/ # MLflow experiment logging & model registry
├── 04-deployment/ # Model deployment (e.g. FastAPI / Docker)
├── 05-monitoring/ # Data drift + prediction monitoring (e.g. Evidently)
├── 06-cicd/ # CI/CD automation via GitHub Actions
│
├── .github/workflows/ # CI/CD workflows
├── requirements.txt # Python dependencies
├── .flake8 # Linting configuration
└── .gitignore


Each module is self-contained and reflects a real-world ML engineering workflow.

---

## 🧪 1. Experiment Tracking (MLflow)

In `03-experiment-tracking/`, the project uses **MLflow** to:

- Log parameters, metrics, and artifacts  
- Compare models (Linear Regression, Random Forest, etc.)  
- Store trained models in the MLflow Model Registry  
- Track reproducible experiment history

This enables transparent experiment management across the team.

---

## 🛠 2. Feature Engineering & Data Preparation

The `02-data-sampling-features/` section includes:

- Train/validation/test splits  
- Categorical encoding  
- Geolocation feature engineering  
- Outlier filtering  
- Pipeline building for preprocessing  

A clean dataset is exported for training and deployment.

---

## 🚀 3. Model Deployment

The `04-deployment/` module showcases:

- Packaging the trained model  
- Building an API endpoint for predictions (e.g., using FastAPI or Flask)  
- Dockerizing the service  
- Running it locally using Docker  

This simulates real-world model serving infrastructure.

---

## 📈 4. Model Monitoring (EvidentlyAI)

The `05-monitoring/` module adds:

- Data drift detection  
- Prediction drift monitoring  
- Metric tracking  
- Dashboard/report generation  

This ensures the model continues performing well in production.

---

## 🔁 5. CI/CD Pipeline (GitHub Actions)

The `06-cicd/` section configures:

- Automated linting (`flake8`)  
- Automated testing  
- Build & deployment pipelines  
- Continuous integration workflows  

This enforces engineering best practices and ensures reliability.

---

## 🧰 Tech Stack

**MLOps Tools**
- MLflow  
- Docker  
- GitHub Actions  
- EvidentlyAI

**Python Libraries**
- pandas  
- scikit-learn  
- numpy  
- joblib  

**Engineering**
- FastAPI / Flask (depending on module)  
- Linting: flake8  
- CI/CD: GitHub Actions  

---

## ⭐ Key Skills Demonstrated

- End-to-end ML pipeline development  
- Experiment tracking & model registry  
- Modular engineering design  
- Production-ready model deployment  
- Monitoring for drift/performance degradation  
- CI/CD pipelines for ML  
- Dockerization & containerized workflows  
- Collaborative ML development at scale  

---

## 👩‍💻 Author

**Mariana Saca**  
Data Analyst | Python | SQL | Machine Learning | MLOps  
- LinkedIn: https://www.linkedin.com/in/marianasaca/  
- GitHub: https://github.com/marianasaca  

📧 **msaca16@gmail.com**

---

## 📎 Notes

This project was created as part of the **IE University MBD: Big Data & AI in Operations** course on MLOps.  
It represents a real-world ML engineering workflow, implemented in a modular, scalable structure.
