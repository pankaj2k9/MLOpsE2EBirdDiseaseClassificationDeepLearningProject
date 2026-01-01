#  MLOps E2E Bird Disease Classification (Deep Learning)

> **Production-grade, end-to-end MLOps system** for bird disease classification using **CNNs**, **TensorFlow**, **Flask**, **Docker**, **AWS ECR + EC2**, and **YAML-driven pipelines**.

 **GitHub Repository**
[https://github.com/pankaj2k9/MLOpsE2EBirdDiseaseClassificationDeepLearningProject.git](https://github.com/pankaj2k9/MLOpsE2EBirdDiseaseClassificationDeepLearningProject.git)

**Live Inference Endpoint**
[http://52.87.125.220/](http://52.87.125.220/)

---

##  Executive Summary (FAANG Style)

This repository demonstrates a **real-world MLOps workflow** that mirrors industry practices used at FAANG-scale ML teams:

* Modular ML pipelines (data → model → evaluation)
* Config-driven experimentation
* Containerized inference service
* Cloud-native deployment (AWS ECR + EC2)
* CI/CD-ready structure
* Clear separation of **research**, **training**, and **production**

---

##  Business Problem

Bird diseases can cause large-scale losses in poultry farming.
Early detection using **image-based deep learning models** can significantly reduce impact.

This system:

* Classifies bird diseases from images
* Exposes predictions via a REST API
* Is fully deployable in production environments

---

## System Architecture

### High-Level Flow

```
Data → Training Pipeline → Model Artifacts → Docker Image
     → AWS ECR → EC2 → Flask API → End User
```

### Components

* **Training Pipeline**: Modular Python pipelines
* **Model**: CNN (TensorFlow/Keras)
* **Inference**: Flask REST API
* **Packaging**: Docker
* **Registry**: AWS ECR
* **Compute**: AWS EC2

---

##  Repository Structure

```
├── .github/workflows
│   └── cicd.yaml                 # CI/CD pipeline
│
├── artifacts                     # Generated pipeline outputs
├── config
│   └── config.yaml               # Centralized configuration
│
├── logs                           # Pipeline logs
├── model
│   └── model.h5                  # Trained CNN model
│
├── notebooks                      # Experimental notebooks
│   ├── 01_data_ingestion.ipynb
│   ├── 02_prepare_base_model.ipynb
│   ├── 03_model_trainer.ipynb
│   └── 04_model_evaluation.ipynb
│
├── src/cnnClassifier
│   ├── components                # Core ML logic
│   ├── pipeline                  # Pipeline orchestration
│   ├── config                    # Config manager
│   ├── constants
│   ├── entity
│   └── utils
│
├── templates
│   └── index.html                # UI template
│
├── app.py                        # Flask inference app
├── Dockerfile                    # Docker image definition
├── setup.py
├── requirements.txt
└── README.md
```

---

##  MLOps Pipeline Stages

### 1️⃣ Data Ingestion

* Downloads dataset
* Extracts and stores versioned artifacts

### 2️⃣ Prepare Base Model

* Loads pretrained CNN backbone
* Freezes layers
* Adds custom classifier head

### 3️⃣ Model Training

* Trains CNN using TensorFlow
* Saves model as `model.h5`

### 4️⃣ Model Evaluation

* Evaluates accuracy & loss
* Logs metrics for analysis

---

##  Tech Stack

| Layer            | Technology         |
| ---------------- | ------------------ |
| Language         | Python             |
| ML Framework     | TensorFlow / Keras |
| Model            | CNN                |
| Backend          | Flask              |
| Containerization | Docker             |
| Registry         | AWS ECR            |
| Compute          | AWS EC2            |
| CI/CD            | GitHub Actions     |
| Config           | YAML               |

---

##  Local Development

### Clone Repository

```bash
git clone https://github.com/pankaj2k9/MLOpsE2EBirdDiseaseClassificationDeepLearningProject.git
cd MLOpsE2EBirdDiseaseClassificationDeepLearningProject
```

### Create Virtual Environment

```bash
python -m venv venv
source venv/bin/activate
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Run Training Pipeline

```bash
python src/cnnClassifier/pipeline/stage_01_data_ingestion.py
python src/cnnClassifier/pipeline/stage_02_prepare_base_model.py
python src/cnnClassifier/pipeline/stage_03_model_trainer.py
python src/cnnClassifier/pipeline/stage_04_evaluation.py
```

### Run Flask App

```bash
python app.py
```

Access:

```
http://localhost:8080
```

---

##  Dockerization

### Build Docker Image

```bash
docker build -t bird-disease-classifier .
```

### Run Container

```bash
docker run -p 8080:8080 bird-disease-classifier
```

---

##  AWS Deployment (Production)

### Required AWS Services

* **EC2** → Virtual Machine
* **ECR** → Docker Image Registry

---

###  Required IAM Policies

Attach the following policies to your IAM user or role:

```
AmazonEC2ContainerRegistryFullAccess
AmazonEC2FullAccess
```

---

###  Environment Variables

```bash
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=

AWS_ECR_LOGIN_URI=
ECR_REPOSITORY_NAME=simple-app
```

---

## Deployment Workflow (Step-by-Step)

### 1️⃣ Build Docker Image

```bash
docker build -t simple-app .
```

### 2️⃣ Authenticate to ECR

```bash
aws ecr get-login-password --region us-east-1 \
| docker login --username AWS --password-stdin AWS_ECR_LOGIN_URI
```

### 3️⃣ Tag Image

```bash
docker tag simple-app:latest \
AWS_ECR_LOGIN_URI/simple-app:latest
```

### 4️⃣ Push Image to ECR

```bash
docker push AWS_ECR_LOGIN_URI/simple-app:latest
```

---

##  EC2 Setup

### Optional

```bash
sudo apt-get update -y
sudo apt-get upgrade -y
```

### Required (Docker Installation)

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
newgrp docker
```

---

### Pull Image from ECR (EC2)

```bash
docker pull AWS_ECR_LOGIN_URI/simple-app:latest
```

### Run Container on EC2

```bash
docker run -d -p 8080:8080 \
AWS_ECR_LOGIN_URI/simple-app:latest
```

---

## Live Production Endpoint

```
http://52.87.125.220/
```

---

## 🧪 Research vs Production

| Layer        | Purpose                       |
| ------------ | ----------------------------- |
| `research/`  | Experimentation & prototyping |
| `src/`       | Production-ready pipelines    |
| `artifacts/` | Versioned ML outputs          |
| `app.py`     | Inference service             |

---

## Future Enhancements

* MLflow model registry
* Data & concept drift monitoring
* Canary deployments
* Auto-retraining
* GPU-enabled EC2
* Auth & rate-limiting
* Kubernetes (EKS)

---

## 👤 Author

**Pankaj Kumar Pramanik**
AI & Data Engineer | MLOps | Deep Learning

🌐 Portfolio: [https://pankajpramanik.com](https://pankajpramanik.com)

