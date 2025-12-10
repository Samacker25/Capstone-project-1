#  Sentiment Analysis – End-to-End MLOps Pipeline

A fully production-style Machine Learning + MLOps workflow built using AWS, Kubernetes, MLflow, DVC, GitHub Actions, Docker, and real monitoring tools like Prometheus & Grafana.

This project demonstrates how a text-classification ML model can be developed, tracked, deployed, and monitored using modern MLOps practices.

# 1. Project Overview

This project implements an end-to-end MLOps pipeline for Sentiment Analysis that automates:

Data ingestion from AWS S3

Preprocessing & Feature Engineering (NLP + TF-IDF)

Model training, evaluation & versioning

Reproducible ML pipelines using DVC

CI pipeline execution using GitHub Actions

Containerization with Docker

Deployment on AWS EKS (Kubernetes)

Monitoring & alerting using Prometheus + Grafana

It mimics the workflow followed by ML Engineers and MLOps teams in real-world production systems.

# 2. Architecture Diagram
AWS S3 → DVC Pipeline → Preprocessing → Feature Engineering → Model Training
      → MLflow Tracking → Model Registry → CI/CD → Docker → AWS ECR → AWS EKS
      → Prometheus Monitoring → Grafana Dashboards

# 3. End-to-End Workflow
# Data Ingestion

Raw dataset stored in AWS S3

Pulled into pipeline using DVC (dvc repro)

# Data Preprocessing & Feature Engineering

Text cleaning

Tokenization

TF-IDF Vectorization

Dataset splitting

# Model Training & Evaluation

Logistic Regression / SVM / Naive Bayes

Cross-validation

MLflow used for:

Experiment tracking

Metrics logging

Parameter tracking

Model versioning

# Model Registry & Promotion

Best model automatically promoted to production through CI pipeline

Stored in MLflow’s Model Registry

# 4. CI/CD Pipeline (GitHub Actions)

Every push triggers:

🔹 CI Stage

Run DVC pipeline

Run ML tests (tests/test_model.py)

Run API tests (tests/test_flask_app.py)

Register & promote model if tests pass

🔹 CD Stage

Build Docker image

Push to AWS ECR

Update deployment on AWS EKS

Kubernetes rollout update

This ensures fully automated, reproducible deployment with every commit.

# 5. AWS Deployment (EKS + EC2)

Kubernetes cluster created using AWS EKS

Nodes running on EC2

App deployed as a Kubernetes Deployment + Service

Secrets managed via Kubernetes Secret

Auto-updates triggered by CI/CD

# 6. Monitoring & Alerting

Metrics collected via:

Prometheus → scrapes application & system metrics

Grafana → dashboards for:

Model latency

Prediction throughput

API status

Pod health

Resource consumption

Alerts can be configured for:
⚠️ High error rate
⚠️ High latency
⚠️ Pod crash loops

# 7. Tech Stack
Languages & ML

Python

Scikit-learn

NLP (TF-IDF)

MLOps Tools

MLflow

DVC

GitHub Actions

Docker

Cloud & Deployment

AWS S3

AWS ECR

AWS EC2

AWS EKS

Kubernetes

Monitoring

Prometheus

Grafana

API

Flask REST API

📂 8. Project Structure
├── data/                     # DVC managed dataset
├── src/
│   ├── data_ingestion.py
│   ├── data_preprocessing.py
│   ├── feature_engineering.py
│   ├── model_trainer.py
│   ├── model_evaluation.py
│   └── utils.py
├── models/                   # Saved models (MLflow-managed)
├── deployment/
│   ├── Dockerfile
│   ├── deployment.yaml
│   └── service.yaml
├── scripts/
│   ├── promote_model.py
├── tests/
│   ├── test_model.py
│   └── test_flask_app.py
├── app.py                    # Flask API
├── requirements.txt
├── dvc.yaml                  # DVC pipeline
├── README.md
└── .github/workflows/ci.yaml # GitHub Actions pipeline

▶️ 9. Run Project Locally
1️⃣ Create a virtual environment
python -m venv venv
source venv/bin/activate

2️⃣ Install dependencies
pip install -r requirements.txt

3️⃣ Reproduce pipeline
dvc repro

4️⃣ Run Flask API
python app.py

# 10. Docker Build
docker build -t sentiment-app .
docker run -p 5000:5000 sentiment-app

# 11. Deploy to Kubernetes (EKS)
Update kubeconfig:
aws eks update-kubeconfig --region us-east-1 --name flask-app-cluster

Apply deployment:
kubectl apply -f deployment.yaml

# 12. Monitoring

Prometheus:

kubectl port-forward svc/prometheus-service 9090:9090


Grafana:

kubectl port-forward svc/grafana-service 3000:3000

# 13. Features

✔ End-to-end automated ML pipeline
✔ Model registry + version control
✔ Fully containerized
✔ CI/CD with GitHub Actions
✔ Production-grade Kubernetes deployment
✔ Monitoring + alerting
✔ Cloud-native architecture

# 14. Future Improvements

Add drift detection

Add model re-training triggers

Implement feature store

Deploy to multi-node cluster

Integrate FastAPI instead of Flask

# Acknowledgement

Special thanks to Vikash Das for his step-by-step tutorial that guided the entire project structure and workflow.
