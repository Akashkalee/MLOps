# 30-Day MLOps/DevOps Roadmap: Daily Quick-Start Guide

---

## ⚡ Quick Summary

**Goal:** Build production-grade MLOps/DevOps portfolio in 30 days
**Time Commitment:** 4-5 hours/day
**Target Outcome:** Land MLOps/DevOps role
**Tech Stack Level:** Advanced 2026 enterprise standards

---

## 📋 Pre-Requisites (Install Before Starting)

### Essential Software
```bash
# Python setup
python3 --version  # 3.11+
pip install --upgrade pip

# Git
git --version

# Docker
docker --version
docker-compose --version

# Kubernetes
kubectl version --client

# Cloud CLI (choose one)
aws --version  # For AWS
gcloud --version  # For GCP
az --version  # For Azure

# Editor/IDE
# VS Code + Python extension recommended
# Or: PyCharm, IntelliJ IDEA
```

### Quick Setup Script
```bash
#!/bin/bash
# setup_environment.sh

# Create workspace
mkdir -p ~/mlops-projects && cd ~/mlops-projects

# Python virtual environment
python3 -m venv venv
source venv/bin/activate

# Essential tools
pip install poetry black isort flake8 pytest pytest-cov
pip install fastapi uvicorn pydantic
pip install pandas numpy scikit-learn
pip install mlflow dvc
pip install docker

# Git setup
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Pre-commit hooks
pip install pre-commit
pre-commit install

echo "✓ Environment setup complete"
```

---

## 🗓️ WEEK 1: Foundations (Days 1-7)

### Daily Schedule Template
```
9:00 AM - 10:00 AM:   Learn theory (videos/docs)
10:00 AM - 1:00 PM:   Hands-on implementation
1:00 PM - 2:00 PM:    Lunch break
2:00 PM - 4:00 PM:    Continue implementation
4:00 PM - 5:00 PM:    Test, document, commit
```

---

### DAY 1: Python MLOps CLI Tool

**Morning (Theory)**
- [ ] Read: Click documentation (30 min)
- [ ] Watch: Real Python CLI tutorial (30 min)

**Afternoon (Implementation)**
```bash
cd ~/mlops-projects
mkdir day1-cli-tool && cd day1-cli-tool
git init

# Project structure
mkdir -p src tests
touch src/__init__.py tests/test_cli.py
touch main.py config.yaml requirements.txt README.md

# Install dependencies
pip install click pydantic pyyaml
```

**Code Tasks:**
- [ ] Create CLI with 5+ commands
- [ ] Implement config parsing
- [ ] Add help documentation
- [ ] Write 3+ unit tests

**Evening (Finalize)**
```bash
pytest tests/ -v
git add .
git commit -m "feat: day 1 - MLOps CLI tool"
git tag day1-complete
```

**Deliverable:** GitHub repo with working CLI, 100% test coverage

---

### DAY 2: Docker Containerization

**Morning (Theory)**
- [ ] Docker docs: Images & Containers (30 min)
- [ ] Multi-stage builds tutorial (30 min)

**Afternoon (Implementation)**
```bash
cd ~/mlops-projects/day1-cli-tool

# Create Dockerfile
cat > Dockerfile << 'EOF'
FROM python:3.11-slim as builder
WORKDIR /app
COPY requirements.txt .
RUN pip install --user --no-cache-dir -r requirements.txt

FROM python:3.11-slim
WORKDIR /app
COPY --from=builder /root/.local /root/.local
COPY . .
ENV PATH=/root/.local/bin:$PATH
EXPOSE 8000
CMD ["python", "main.py"]
EOF

# Docker compose
cat > docker-compose.yml << 'EOF'
version: '3.8'
services:
  app:
    build: .
    ports:
      - "8000:8000"
    environment:
      - LOG_LEVEL=INFO
EOF
```

**Code Tasks:**
- [ ] Multi-stage Dockerfile
- [ ] docker-compose.yml with services
- [ ] Health check configuration
- [ ] Environment variable support

**Evening (Finalize)**
```bash
docker build -t mlops-cli:1.0 .
docker run mlops-cli:1.0
docker-compose up
git add Dockerfile docker-compose.yml
git commit -m "feat: day 2 - Docker containerization"
```

**Deliverable:** Dockerized application, working docker-compose

---

### DAY 3: Git Workflow & Version Control

**Morning (Theory)**
- [ ] Pro Git Book Chapters 1-3 (1 hour)
- [ ] GitHub Skills: "Introduction to GitHub" (30 min)

**Afternoon (Implementation)**
```bash
cd ~/mlops-projects

# Setup pre-commit
cat > .pre-commit-config.yaml << 'EOF'
repos:
  - repo: https://github.com/psf/black
    rev: 23.12.0
    hooks:
      - id: black
  - repo: https://github.com/PyCQA/isort
    rev: 5.13.2
    hooks:
      - id: isort
  - repo: https://github.com/PyCQA/flake8
    rev: 6.1.0
    hooks:
      - id: flake8
EOF

# Install pre-commit
pre-commit install
pre-commit run --all-files

# Create feature branch
git checkout -b feature/git-workflow
git add .pre-commit-config.yaml
git commit -m "chore: add pre-commit hooks"
```

**Git Workflow Tasks:**
- [ ] Setup .gitignore properly
- [ ] Configure pre-commit hooks
- [ ] Use feature branches
- [ ] Write descriptive commits
- [ ] Create pull request (if on GitHub)

**Evening (Finalize)**
```bash
git log --oneline | head -10
git branch -a
git commit -m "chore: git workflow configuration"
```

**Deliverable:** Professional Git workflow, clean commit history

---

### DAY 4: Linux & Shell Scripting

**Morning (Theory)**
- [ ] Linux Command Line basics (1 hour)
- [ ] Bash scripting fundamentals (30 min)

**Afternoon (Implementation)**
```bash
mkdir ~/mlops-projects/scripts

# Create setup script
cat > ~/mlops-projects/scripts/setup.sh << 'EOF'
#!/bin/bash
set -e

# Colors
RED='\033[0;31m'
GREEN='\033[0;32m'
NC='\033[0m'

echo "Setting up MLOps environment..."

# Check Python
if ! command -v python3 &> /dev/null; then
    echo -e "${RED}Python3 not found${NC}"
    exit 1
fi

# Create venv
python3 -m venv venv
source venv/bin/activate

# Install deps
pip install -r requirements.txt

# Create dirs
mkdir -p data models logs
chmod 755 data models logs

echo -e "${GREEN}Setup complete!${NC}"
EOF

chmod +x ~/mlops-projects/scripts/setup.sh

# Create monitor script
cat > ~/mlops-projects/scripts/monitor.sh << 'EOF'
#!/bin/bash
watch -n 1 'ps aux | grep python'
EOF

chmod +x ~/mlops-projects/scripts/monitor.sh
```

**Shell Script Tasks:**
- [ ] Create setup automation script
- [ ] Error handling with set -e
- [ ] Logging to files
- [ ] Cron job scheduling
- [ ] Permission management

**Evening (Finalize)**
```bash
bash ~/mlops-projects/scripts/setup.sh
git add scripts/
git commit -m "feat: day 4 - shell scripting automation"
```

**Deliverable:** Production-ready shell scripts with error handling

---

### DAY 5: Virtual Environments & Dependency Management

**Morning (Theory)**
- [ ] Poetry documentation (45 min)
- [ ] Conda vs venv comparison (30 min)

**Afternoon (Implementation)**
```bash
cd ~/mlops-projects

# Initialize Poetry
poetry init --no-interaction --name mlops-project --author "Your Name"

# Add dependencies
poetry add fastapi uvicorn pydantic scikit-learn pandas numpy
poetry add --group dev pytest black isort flake8 pre-commit

# Create pyproject.toml
cat >> pyproject.toml << 'EOF'
[tool.black]
line-length = 100

[tool.isort]
profile = "black"

[tool.pytest.ini_options]
testpaths = ["tests"]
EOF

poetry lock
```

**Dependency Management Tasks:**
- [ ] Poetry project setup
- [ ] Separate dev/prod dependencies
- [ ] Lock file generation
- [ ] Version pinning strategy
- [ ] Reproducible environments

**Evening (Finalize)**
```bash
poetry install
poetry show  # List all deps
git add pyproject.toml poetry.lock
git commit -m "feat: day 5 - Poetry dependency management"
```

**Deliverable:** Poetry project with proper dependency management

---

### DAY 6: Unit Testing & Code Quality

**Morning (Theory)**
- [ ] pytest documentation (45 min)
- [ ] Testing best practices (30 min)

**Afternoon (Implementation)**
```bash
cd ~/mlops-projects

# Create test structure
mkdir -p tests
touch tests/__init__.py tests/test_preprocessing.py

# Write comprehensive tests
cat > tests/test_preprocessing.py << 'EOF'
import pytest
import numpy as np
import pandas as pd

@pytest.fixture
def sample_data():
    return pd.DataFrame({
        'feature1': [1, 2, 3, np.nan, 5],
        'feature2': [10, 20, 30, 40, 50],
    })

def test_data_shape(sample_data):
    assert sample_data.shape[0] == 5
    assert sample_data.shape[1] == 2

def test_null_values(sample_data):
    assert sample_data.isnull().sum().sum() == 1

@pytest.mark.parametrize("value", [0, 1, 2.5, -1])
def test_multiple_values(value):
    assert isinstance(value, (int, float))
EOF

# Run tests with coverage
poetry run pytest tests/ -v --cov=src --cov-report=html
```

**Testing Tasks:**
- [ ] Unit tests (>80% coverage)
- [ ] Fixtures and parametrization
- [ ] Edge case testing
- [ ] Integration tests
- [ ] Coverage reports

**Evening (Finalize)**
```bash
poetry run pytest
poetry run flake8 src tests
git add tests/
git commit -m "feat: day 6 - comprehensive unit testing"
```

**Deliverable:** Test suite with >80% coverage, HTML report

---

### DAY 7: Data Versioning with DVC

**Morning (Theory)**
- [ ] DVC documentation (45 min)
- [ ] DVC tutorial walkthrough (30 min)

**Afternoon (Implementation)**
```bash
cd ~/mlops-projects

# Initialize DVC
poetry add dvc dvc-s3

dvc init
dvc config core.autostage true

# Create dummy data
mkdir -p data
echo "id,feature1,feature2
1,0.5,100
2,0.3,200
3,0.8,150" > data/raw.csv

# Version data
dvc add data/raw.csv
git add data/raw.csv.dvc .gitignore

# Create pipeline
cat > dvc.yaml << 'EOF'
stages:
  preprocess:
    cmd: python scripts/preprocess.py
    deps:
      - data/raw.csv
    outs:
      - data/processed.csv
  train:
    cmd: python scripts/train.py
    deps:
      - data/processed.csv
    outs:
      - models/model.pkl
EOF

dvc repro
```

**DVC Tasks:**
- [ ] DVC initialization
- [ ] Data versioning
- [ ] DVC pipeline creation
- [ ] Remote storage setup (optional)
- [ ] Experiment tracking

**Evening (Finalize)**
```bash
dvc dag --md
git add dvc.yaml dvc.lock
git commit -m "feat: day 7 - DVC data versioning pipeline"
```

**Deliverable:** DVC pipeline with versioned data

---

## ✅ WEEK 1 CHECKLIST

**Code Quality:**
- [ ] All code formatted with Black
- [ ] No lint errors (flake8 passing)
- [ ] Tests >80% coverage
- [ ] Pre-commit hooks passing

**Git Repository:**
- [ ] 7 meaningful commits
- [ ] Clean .gitignore
- [ ] All files tracked
- [ ] Descriptive commit messages

**GitHub:**
- [ ] README.md for main repo
- [ ] Each day has its own folder
- [ ] Code examples in README
- [ ] Installation instructions

**Tech Proficiency:**
- [ ] Can write Python CLI from scratch
- [ ] Docker multi-stage builds understood
- [ ] Git workflow smooth
- [ ] Shell scripts functional
- [ ] Testing framework mastered
- [ ] DVC pipeline working

---

## 🗓️ WEEK 2: MLOps Fundamentals (Days 8-14)

### Quick Checklist Template

**DAY 8: MLflow Experiment Tracking**
```bash
# Setup
pip install mlflow scikit-learn
mlflow server --backend-store-uri sqlite:///mlflow.db &

# Code
mlflow.start_run()
mlflow.log_params(params)
mlflow.log_metrics(metrics)
mlflow.sklearn.log_model(model, "model")
mlflow.end_run()

# Test
curl http://localhost:5000/api/2.0/mlflow/runs/search
```

**Tasks:**
- [ ] MLflow server running
- [ ] 3+ experiments logged
- [ ] Metrics comparison working
- [ ] Model registry integration
- [ ] Artifacts stored

**Deliverable:** MLflow tracking with 5+ models logged

---

**DAY 9: Feature Engineering Pipeline**
```bash
# Code structure
src/
├── preprocessing.py  # Feature transforms
├── validation.py     # Feature validation
└── __init__.py

# Test
python -c "from src.preprocessing import FeatureEngineer"
pytest tests/test_preprocessing.py -v
```

**Tasks:**
- [ ] Fit/transform pattern
- [ ] Preprocessing serialization
- [ ] Feature validation
- [ ] Train/test consistency
- [ ] Pickle model artifacts

**Deliverable:** Reusable feature pipeline

---

**DAY 10: Model Training & Evaluation**
```bash
# Code
model = RandomForestClassifier()
model.fit(X_train, y_train)
y_pred = model.predict(X_test)
metrics = {
    'accuracy': accuracy_score(y_test, y_pred),
    'f1': f1_score(y_test, y_pred)
}
```

**Tasks:**
- [ ] Multi-model comparison
- [ ] Cross-validation setup
- [ ] Hyperparameter tuning
- [ ] Metrics calculation
- [ ] Model serialization

**Deliverable:** Production model with metrics

---

**DAY 11: FastAPI Model Serving**
```bash
# Quick test
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class PredictionInput(BaseModel):
    features: list

@app.post("/predict")
def predict(input: PredictionInput):
    return {"prediction": 0.5}

# Run: uvicorn main:app --reload
# Test: curl -X POST http://localhost:8000/predict ...
```

**Tasks:**
- [ ] FastAPI endpoints
- [ ] Request validation (Pydantic)
- [ ] Response models
- [ ] Error handling
- [ ] API documentation

**Deliverable:** Production FastAPI server

---

**DAY 12: Database & ORM**
```bash
# PostgreSQL setup
docker run -e POSTGRES_PASSWORD=postgres -p 5432:5432 postgres:15

# SQLAlchemy
from sqlalchemy import create_engine
engine = create_engine("postgresql://user:pass@localhost/db")
session = Session(engine)
session.add(obj)
session.commit()
```

**Tasks:**
- [ ] PostgreSQL running
- [ ] SQLAlchemy models
- [ ] CRUD operations
- [ ] Migrations (Alembic)
- [ ] Connection pooling

**Deliverable:** Production database setup

---

**DAY 13: Kubernetes Deployment**
```bash
# Create K8s manifests
kubectl apply -f deployment.yaml
kubectl get pods
kubectl logs <pod-name>
kubectl port-forward svc/ml-api 8000:80
```

**Tasks:**
- [ ] Deployment manifest
- [ ] Service configuration
- [ ] ConfigMaps/Secrets
- [ ] Resource limits
- [ ] Health checks

**Deliverable:** K8s deployment running

---

**DAY 14: Prometheus + Grafana**
```bash
# Start stack
docker-compose up -d

# Add metrics
from prometheus_client import Counter
predictions = Counter('predictions_total', 'Total predictions')

# Test
curl http://localhost:8000/metrics
# View: http://localhost:3000 (Grafana)
```

**Tasks:**
- [ ] Prometheus scraping
- [ ] Custom metrics
- [ ] Grafana dashboards
- [ ] Alert rules
- [ ] Data retention

**Deliverable:** Monitoring dashboard

---

## 📊 WEEK 2 SUMMARY

| Day | Project | Time | Status |
|-----|---------|------|--------|
| 8 | MLflow tracking | 4h | ✓ |
| 9 | Feature engineering | 4h | ✓ |
| 10 | Model training | 4h | ✓ |
| 11 | FastAPI | 4h | ✓ |
| 12 | Database | 3h | ✓ |
| 13 | Kubernetes | 4h | ✓ |
| 14 | Monitoring | 4h | ✓ |
| **Total** | | **31h** | |

**Week 2 Goals:**
- [ ] Complete ML pipeline end-to-end
- [ ] API serving predictions
- [ ] Monitoring in place
- [ ] All integrated

---

## 🗓️ WEEK 3: Advanced MLOps (Days 15-21)

### Fast-Track (1 hour per topic)

**DAY 15: GitHub Actions**
- [ ] Create `.github/workflows/test.yml`
- [ ] Setup test automation
- [ ] Docker build & push
- [ ] Deployment trigger

**DAY 16: Terraform**
- [ ] AWS VPC setup
- [ ] RDS configuration
- [ ] S3 bucket for artifacts
- [ ] IAM roles

**DAY 17: MLflow Registry**
- [ ] Register models
- [ ] Stage transitions
- [ ] Performance comparison
- [ ] Automatic promotion

**DAY 18: Data Quality**
- [ ] Great Expectations setup
- [ ] Data validation rules
- [ ] Quality reports
- [ ] Anomaly detection

**DAY 19: Feature Store**
- [ ] Feast installation
- [ ] Feature definitions
- [ ] Online/offline stores
- [ ] Serving API

**DAY 20: Airflow**
- [ ] DAG creation
- [ ] Task dependencies
- [ ] Error handling
- [ ] Monitoring

**DAY 21: KServe**
- [ ] InferenceService manifest
- [ ] Model serving
- [ ] Canary deployments
- [ ] Request routing

---

## 🗓️ WEEK 4: Production MLOps (Days 22-30)

### Integration Focus

**DAY 22-23: Drift Detection & CT**
- [ ] Monitoring setup
- [ ] Drift metrics
- [ ] Automatic retraining
- [ ] Performance tracking

**DAY 24: K8s Scaling**
- [ ] Multi-environment setup
- [ ] Auto-scaling policies
- [ ] Resource optimization
- [ ] Cost monitoring

**DAY 25-26: Logging & Security**
- [ ] ELK Stack
- [ ] Distributed tracing
- [ ] Security hardening
- [ ] RBAC setup

**DAY 27-28: Advanced Topics**
- [ ] LLM/RAG pipelines
- [ ] Cost optimization
- [ ] Compliance setup

**DAY 29-30: Portfolio**
- [ ] Documentation
- [ ] Live demo
- [ ] Performance metrics
- [ ] Interview prep

---

## 🎯 Daily Standup Template

Use this format each evening:

```
## Day X Summary

### Completed
- [ ] Task 1
- [ ] Task 2
- [ ] Task 3

### Metrics
- Tests passing: 100%
- Code coverage: 85%
- Lines of code: 500+
- Commits: 3

### Blockers
- Issue: ...
- Solution: ...

### Tomorrow Plan
- Task 1
- Task 2
- Task 3

### Learnings
- Key takeaway 1
- Key takeaway 2

### GitHub
git push origin day-X-complete
git tag day-X-complete
```

---

## 📱 Mobile Study Tips

### Before bed (30 min)
- Read documentation
- Watch tutorial videos
- Review concepts

### Early morning (1 hour)
- Code review from yesterday
- Plan day's implementation
- Setup environment

### Lunch break (30 min)
- Community slack channels
- Read MLOps blogs
- Industry news

---

## 🚨 Common Issues & Solutions

### Docker Won't Start
```bash
# Check running containers
docker ps
# Clear dangling images
docker system prune
# Rebuild
docker-compose down && docker-compose up --build
```

### Port Already in Use
```bash
# Find process on port
lsof -i :8000
# Kill process
kill -9 <PID>
```

### Python Dependency Conflicts
```bash
# Fresh venv
rm -rf venv
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Git Merge Conflicts
```bash
git checkout --theirs <file>  # Accept incoming
git checkout --ours <file>    # Keep current
git add <file>
git commit -m "Resolve conflict"
```

### Kubernetes Pod Issues
```bash
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl exec -it <pod-name> /bin/bash
```

---

## 🏆 Success Metrics Tracking

### Create tracking spreadsheet:

| Day | Project | Tests | Coverage | LOC | Commits | Status |
|-----|---------|-------|----------|-----|---------|--------|
| 1 | CLI | ✓ | 85% | 250 | 2 | ✓ |
| 2 | Docker | ✓ | 80% | 50 | 1 | ✓ |
| 3 | Git | ✓ | - | 0 | 5 | ✓ |
| ... | ... | ... | ... | ... | ... | ... |

**Target:**
- Total code: 5,000+ lines
- Tests: >85% coverage
- Commits: 50+
- Projects: 30
- Stars (GitHub): 50+

---

## 💪 Motivation Boosters

### Weekly Wins
1. **Day 7**: Basic portfolio ready
2. **Day 14**: End-to-end ML pipeline
3. **Day 21**: Advanced MLOps features
4. **Day 30**: Production system + job offers

### Share Progress
- Tweet daily learning
- LinkedIn posts
- GitHub contributions
- Community forums

### Connect with Others
- Join MLOps.community
- Contribute to open-source
- Participate in discussions
- Help others learning

---

## 📞 Support Resources

### When Stuck
1. GitHub Issues section
2. Stack Overflow
3. Official documentation
4. Community forums (MLOps.community)
5. YouTube tutorials

### Time Management
- **Use Pomodoro:** 25min work, 5min break
- **Track time:** See daily summary
- **Adjust pace:** If falling behind, skip optional tasks
- **Sleep well:** 7-8 hours improves learning

---

## 🎓 After 30 Days

### Immediate Next Steps
1. Polish portfolio
2. Update LinkedIn
3. Start applying
4. Interview preparation
5. Contribute to open-source

### Timeline to Job
- Weeks 1-4: Build portfolio
- Weeks 5-6: Apply to jobs
- Weeks 7-8: Interviews
- Week 9+: Offer/Negotiation

### Expected Salary Range (2026)
- **India:** ₹18-35 LPA
- **USA:** $120-160K
- **UK:** £60-90K
- **Remote:** Varies by location

---

## 🔗 Quick Links

### Tools
- GitHub: https://github.com
- Docker Hub: https://hub.docker.com
- Kubernetes: https://kubernetes.io
- AWS: https://aws.amazon.com

### Learning
- Roadmap.sh: https://roadmap.sh/mlops
- MLOps.community: https://mlops.community
- Made With ML: https://madewithml.com
- Fast.ai: https://course.fast.ai

### Communities
- MLOps Slack
- Kubernetes Slack
- DevOps Discord
- Reddit: r/devops

---

**Remember:** The best time to start was yesterday. The second best time is now. 🚀

You've got this! 💪

---

**Last Updated:** April 2026

**Created for:** Serious learners committed to landing MLOps/DevOps roles
