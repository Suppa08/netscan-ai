# 🔍 NetScan AI — Network Security Scanner
 
AI-powered network port scanner with risk analysis, interactive dashboard, and PDF reporting.
 
---
 
## 🚀 Quick Start — Docker (Easiest!) ⭐
 
> Docker use කරොත් Python, Node.js, PostgreSQL install කරන්න ඕනේ නැහැ!
 
### Step 1 — Docker Desktop Install කරන්න
 
👉 https://www.docker.com/products/docker-desktop
 
Download කරලා install කරන්න. Install වුණාම restart කරන්න.
 
### Step 2 — Project Clone කරන්න
 
```bash
git clone https://github.com/Suppa08/netscan-ai.git
cd netscan-ai
```
 
### Step 3 — Run කරන්න
 
```bash
docker-compose up --build
```
 
First time build වෙන්න 5-10 minutes ගන්නවා.
 
### Step 4 — Demo Data Add කරන්න (First time only)
 
නව terminal එකක් open කරලා:
 
```bash
docker-compose exec backend python seed.py
```
 
### Step 5 — Browser එකේ Open කරන්න
 
```
http://localhost
```
 
- Username: admin
- Password: admin123
### App Close කරන්න
 
```bash
docker-compose down
```
 
### ආයෙ Start කරන්න
 
```bash
docker-compose up
```
 
---
 
## 🛠️ Manual Setup (Docker නැතිව)
 
### Requirements
 
- Python 3.11+
- Node.js v20+
- PostgreSQL 16
- Git
### Step 1 — Clone කරන්න
 
```bash
git clone https://github.com/Suppa08/netscan-ai.git
cd netscan-ai
```
 
### Step 2 — Database Setup
 
```bash
psql -U postgres
```
 
```sql
CREATE USER netscan WITH PASSWORD 'netscan_pass';
CREATE DATABASE netscan_db OWNER netscan;
GRANT ALL PRIVILEGES ON DATABASE netscan_db TO netscan;
\q
```
 
### Step 3 — Backend Setup
 
```bash
cd backend
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt --timeout 300
copy .env.example .env
python seed.py
uvicorn app.main:app --reload --port 8000
```
 
### Step 4 — Frontend Setup
 
```bash
cd frontend
copy .env.example .env
npm install
npm run dev
```
 
### Step 5 — Open
 
```
http://localhost:3000
```
 
Login: admin / admin123
 
### හැම දිනකම Start කරන්න
 
Terminal 1 — Backend:
```bash
cd backend
venv\Scripts\activate
uvicorn app.main:app --reload --port 8000
```
 
Terminal 2 — Frontend:
```bash
cd frontend
npm run dev
```
 
---
 
## 📊 Tech Stack
 
| Layer | Technology |
|-------|-----------|
| Frontend | React 18 + Recharts + Lucide |
| Backend | FastAPI (Python 3.11) |
| Scanner | asyncio sockets + python-nmap |
| AI/ML | Scikit-learn + TensorFlow (opt.) |
| Database | PostgreSQL 16 (async SQLAlchemy) |
| Auth | JWT (python-jose + bcrypt) |
| Reports | ReportLab PDF |
| Deploy | Docker Compose |
 
---
 
## 📊 Dashboard Features
 
- Total Scans — count of all historical scans
- Hosts Scanned — total unique IPs assessed
- Open Ports — cumulative across all scans
- High Risk Hosts — hosts with critical/high risk score
- Port Distribution — bar chart of most-seen open ports
- Risk Distribution — pie chart by risk level
- Scan Activity — 30-day timeline
- AI Recommendations — prioritized security actions
- PDF Export — professional downloadable reports
---
 
## 🔒 Scan Types
 
| Type | Description | Requires |
|------|-------------|----------|
| TCP Connect | Full 3-way handshake (default) | Normal user |
| SYN Scan | Half-open, stealthier, faster | Admin/Root |
| UDP Scan | UDP port detection (slower) | Admin/Root |
 
---
 
## 🎯 Supported Targets
 
```
127.0.0.1              # Your own computer
192.168.1.1            # Your router
192.168.1.0/24         # Your home network
scanme.nmap.org        # Legal practice target
```
 
Only scan networks you own or have permission to test!
 
---
 
## 🤖 AI / ML
 
### Default — Rule-Based (No training needed)
Instant risk scoring using weighted port rules and expert security knowledge.
 
### Train Scikit-learn Model
 
```bash
cd backend
python ml_trainer.py
python ml_trainer.py --use-db
```
 
### Train TensorFlow Neural Network
 
```bash
pip install tensorflow
python ml_trainer.py
```
 
---
 
## 🧪 Tests
 
```bash
cd backend
pip install pytest pytest-asyncio
pytest tests/ -v
```
 
---
 
## 📄 PDF Reports
 
Click Export PDF on any completed scan:
- Executive summary with risk metrics
- Top open ports distribution table
- AI security recommendations with CVE references
- Full scan metadata
---
 
## 📁 Project Structure
 
```
netscan/
├── backend/
│   ├── app/
│   │   ├── api/          # Auth, Scans, Reports, Dashboard
│   │   ├── core/         # Config, Database, Security (JWT)
│   │   ├── ml/           # ML Inference Loader
│   │   ├── models/       # SQLAlchemy ORM Models
│   │   └── services/     # Scanner, AI Analyzer, PDF Generator
│   ├── alembic/          # Database Migrations
│   ├── tests/            # pytest Unit Tests
│   ├── ml_trainer.py     # ML Training Script
│   ├── seed.py           # Demo Data Seeder
│   └── requirements.txt
├── frontend/
│   └── src/
│       ├── pages/        # Dashboard, Scans, ScanDetail, NewScan, Login
│       └── utils/        # API Client
├── docker-compose.yml
└── README.md
```
 
---
 
## ⚠️ Legal Notice
 
Only scan networks and systems you own or have explicit written permission to test.
Unauthorized port scanning may violate computer crime laws in your jurisdiction.
 
---
 
## 👨‍💻 Author
 
Suppa08 — https://github.com/Suppa08/netscan-ai
 