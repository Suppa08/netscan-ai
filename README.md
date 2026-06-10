# 🔍 NetScan AI — Network Security Scanner

AI-powered network port scanner with risk analysis, interactive dashboard, and PDF reporting.

## Tech Stack

| Layer       | Technology                        |
|-------------|-----------------------------------|
| Frontend    | React 18 + Recharts + Lucide      |
| Backend API | FastAPI (Python 3.11)             |
| Scanner     | asyncio sockets + python-nmap     |
| AI/ML       | Scikit-learn + TensorFlow (opt.)  |
| Database    | PostgreSQL 16 (async SQLAlchemy)  |
| Auth        | JWT (python-jose + bcrypt)        |
| Reports     | ReportLab PDF                     |
| Deploy      | Docker Compose                    |

---

## 🚀 Quick Start (Docker)

```bash
# 1. Clone / extract project
cd netscan

# 2. Copy env files
cp backend/.env.example backend/.env
cp frontend/.env.example frontend/.env

# 3. Build and start everything
docker-compose up --build

# 4. Seed the database (first time only)
docker-compose exec backend python seed.py
```

Open **http://localhost** in your browser.
Default login: `admin` / `admin123`

---

## 🛠️ Local Development

### Backend

```bash
cd backend

# Create virtualenv
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Start PostgreSQL (Docker)
docker run -d \
  -e POSTGRES_USER=netscan \
  -e POSTGRES_PASSWORD=netscan_pass \
  -e POSTGRES_DB=netscan_db \
  -p 5432:5432 postgres:16-alpine

# Copy env
cp .env.example .env

# Run API
uvicorn app.main:app --reload --port 8000

# Seed demo data
python seed.py
```

API docs: http://localhost:8000/docs

### Frontend

```bash
cd frontend
npm install
cp .env.example .env
npm run dev
```

Open http://localhost:3000

---

## 🤖 AI / ML

### Rule-Based (default, no training needed)
Instant risk scoring via weighted port rules + expert security knowledge.

### Train Scikit-learn Model (recommended)
```bash
cd backend
python ml_trainer.py                  # train on synthetic data
python ml_trainer.py --use-db         # train on your real scan history
```

### Train TensorFlow Neural Network
```bash
pip install tensorflow
python ml_trainer.py                  # trains both sklearn + TF automatically
```

Models are saved to `backend/ml_models/` and auto-loaded by the API.

---

## 🧪 Testing

```bash
cd backend
pip install pytest pytest-asyncio
pytest tests/ -v
```

---

## 📊 Dashboard Features

- **Total Scans** — count of all historical scans
- **Hosts Scanned** — total unique IPs assessed  
- **Open Ports** — cumulative across all scans
- **High Risk Hosts** — hosts with critical/high risk score
- **Port Distribution** — bar chart of most-seen open ports
- **Risk Distribution** — pie chart by risk level
- **Scan Activity** — 30-day timeline
- **AI Recommendations** — prioritized security actions

---

## 🔒 Scan Types

| Type         | Description                           | Requires         |
|--------------|---------------------------------------|------------------|
| TCP Connect  | Full 3-way handshake (default)        | Normal user      |
| SYN Scan     | Half-open, stealthier                 | Root / NET_RAW   |
| UDP Scan     | UDP port detection (slower)           | Root             |

---

## 📄 PDF Reports

Click **Export PDF** on any completed scan. Reports include:
- Executive summary with risk metrics
- Top open ports table
- AI security recommendations with CVE references
- Scan metadata

---

## ⚠️ Legal Notice

Only scan networks and systems you own or have **explicit written permission** to test.
Unauthorized port scanning may violate computer crime laws in your jurisdiction.

---

## 📁 Project Structure

```
netscan/
├── backend/
│   ├── app/
│   │   ├── api/          # FastAPI routers (auth, scans, reports, dashboard)
│   │   ├── core/         # Config, database, security (JWT)
│   │   ├── ml/           # ML inference loader
│   │   ├── models/       # SQLAlchemy ORM models
│   │   └── services/     # Scanner engine, AI analyzer, PDF generator
│   ├── alembic/          # DB migrations
│   ├── tests/            # pytest unit tests
│   ├── ml_trainer.py     # Standalone ML training script
│   ├── seed.py           # Demo data seeder
│   └── requirements.txt
├── frontend/
│   └── src/
│       ├── pages/        # Dashboard, Scans, ScanDetail, NewScan, Login
│       └── utils/        # API client
├── docker-compose.yml
└── README.md
```
