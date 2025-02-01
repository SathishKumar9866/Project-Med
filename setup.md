### **Complete Setup Guide for `medical-project` (Windows, Linux, macOS)**  
This guide provides step-by-step installation for **Windows, Linux, and macOS** to set up your **medical project** across all components (backend, frontend, DevOps, MLOps, and analytics).

---

# **1. General Setup (All OS)**
## **1.1 Install Essential Tools**
✅ **Windows**:
1. Install **Git**: [Download Git](https://git-scm.com/downloads)
2. Install **Node.js**: [Download Node.js (LTS)](https://nodejs.org/en/)
3. Install **Python** (if not installed): [Download Python](https://www.python.org/downloads/)
4. Install **Docker Desktop**: [Download Docker](https://www.docker.com/products/docker-desktop/)
5. Install **VS Code** (Recommended): [Download VS Code](https://code.visualstudio.com/)

✅ **Linux/macOS**:
```bash
# Install system dependencies
sudo apt update && sudo apt install -y git curl build-essential unzip python3 python3-pip python3-venv nodejs npm docker docker-compose
```
For macOS, use **Homebrew**:
```bash
brew install git node python docker-compose
```

---

## **1.2 Clone Project & Setup Environment**
Run the following:
```bash
# Clone project
git clone https://github.com/your-org/medical-project.git
cd medical-project

# Create environment file
cp .env.example .env
```
Edit **.env** and update necessary configurations (e.g., database URL, API keys).

---

# **2. Backend Setup**
✅ **Windows (PowerShell)**
```powershell
cd backend/api-gateway
npm install
npm run start
```

✅ **Linux/macOS**
```bash
cd backend/api-gateway
npm install
npm run start
```

### **Backend Dependencies**
```bash
npm install express graphql @nestjs/graphql passport bcrypt class-validator
npm install --save-dev @types/express @types/node
```

---

# **3. Database Setup**
✅ **PostgreSQL**
- **Windows:** [Download PostgreSQL](https://www.postgresql.org/download/)
- **Linux/macOS:**
  ```bash
  sudo apt install postgresql postgresql-contrib
  ```

Create a PostgreSQL database:
```sql
CREATE USER admin WITH PASSWORD 'securepassword';
CREATE DATABASE medical_db;
GRANT ALL PRIVILEGES ON DATABASE medical_db TO admin;
```

✅ **Neo4j**
- **Windows:** [Download Neo4j](https://neo4j.com/download/)
- **Linux/macOS:**
  ```bash
  wget -O - https://debian.neo4j.com/neotechnology.gpg.key | sudo apt-key add -
  sudo apt update && sudo apt install neo4j
  sudo systemctl start neo4j
  ```

---

# **4. Frontend Setup**
✅ **Windows/Linux/macOS**
```bash
cd apps/web
npm install
npm start
```
Install frontend dependencies:
```bash
npm install react react-dom next axios redux react-redux react-router-dom
npm install @mui/material @mui/icons-material @emotion/react @emotion/styled
```

---

# **5. DevOps (Docker & Kubernetes)**
✅ **Windows:** Install **Docker Desktop**
✅ **Linux/macOS:** Install **Docker & Kubernetes**
```bash
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER
newgrp docker

# Start Docker
sudo systemctl start docker
```
Run:
```bash
cd devops/deployment
docker-compose up -d
```

---

# **6. CI/CD Setup**
✅ **Windows:** Install **GitHub Actions Runner**
```powershell
curl -o actions-runner-win-x64.zip -L https://github.com/actions/runner/releases/latest/download/actions-runner-win-x64.zip
Expand-Archive -Path actions-runner-win-x64.zip -DestinationPath actions-runner
cd actions-runner
config.cmd --url https://github.com/your-org/medical-project --token <TOKEN>
run.cmd
```

✅ **Linux/macOS (GitHub Actions)**
```bash
curl -o actions-runner-linux-x64.tar.gz -L https://github.com/actions/runner/releases/latest/download/actions-runner-linux-x64.tar.gz
tar xzf ./actions-runner-linux-x64.tar.gz
./config.sh --url https://github.com/your-org/medical-project --token <TOKEN>
./run.sh
```

✅ **Jenkins (Alternative)**
```bash
# Install Jenkins (Linux/macOS)
sudo apt install openjdk-11-jdk
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update && sudo apt install jenkins
```

---

# **7. Monitoring & Logging**
✅ **Install Prometheus & Grafana**
```bash
cd devops/monitoring
docker-compose up -d
```
- Access **Grafana** at `http://localhost:3000` (Default login: admin/admin)

---

# **8. MLOps Setup**
✅ **Install DVC, MLflow & Weights & Biases**
```bash
pip install dvc mlflow wandb
```
Initialize DVC:
```bash
cd mlops/dvc
dvc init
dvc remote add storage s3://your-bucket-name
```
Run MLflow Server:
```bash
mlflow server --backend-store-uri sqlite:///mlflow.db --host 0.0.0.0 --port 5000
```
Run Weights & Biases:
```bash
wandb login
```

---

# **9. Testing**
✅ **Unit & Integration Testing**
```bash
cd testing/unit-tests
npm install
npm test
```
✅ **Jest Testing Dependencies**
```bash
npm install --save-dev jest ts-jest @types/jest supertest
```

---

# **10. Documentation**
Your documentation is stored in Markdown (`.md`) files. **5 essential markdown files** to focus on for setup:
1. **`deployment_guide.md`** – Steps to deploy the system
2. **`system_architecture.md`** – High-level system design
3. **`api_design.md`** – API contracts
4. **`testing_strategy.md`** – How testing is structured
5. **`monitoring_best_practices.md`** – Best practices for uptime & alerting

✅ **For Windows/Linux/macOS, install MkDocs**
```bash
pip install mkdocs
mkdocs serve
```
Access documentation at `http://127.0.0.1:8000`.

---

# **Final Steps**
✅ **Run backend**: `cd backend/api-gateway && npm run start`  
✅ **Run frontend**: `cd apps/web && npm start`  
✅ **Run ML pipelines**: `cd mlops && dvc repro`  
✅ **Deploy via Docker**: `docker-compose up -d`  
✅ **Monitor System**: `http://localhost:3000` (Grafana)  

Your full stack **(backend, frontend, DevOps, CI/CD, MLOps, analytics, documentation, and testing)** is now operational. 🚀 