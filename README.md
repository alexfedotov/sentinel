# 🛰️ Sentinel – Event Ingestor and Rule Engine

**Sentinel** is a lightweight, event-driven alerting service built with **FastAPI**, **asyncio**, and **SQLAlchemy**.  
It ingests JSON events via HTTP or streaming backends (Redis/Kafka) and evaluates user-defined rules written in a tiny DSL (Domain-Specific Language).  
When a rule matches an event, Sentinel triggers asynchronous notifications such as Slack or webhooks.

---

## ✨ Features

- 🚀 **Event ingestion** via HTTP (`POST /events`) or async queue  
- 🧩 **Rule engine** with DSL syntax:
  ```text
  when event.type == "order" and amount > 500 then notify("slack:#big-orders")
⚙️ Rule management API — CRUD endpoints for user-defined rules

🧠 Async workers for background event evaluation

🔔 Slack/Webhook notifier with retry & exponential backoff

📊 Prometheus metrics at /metrics

🗃️ PostgreSQL + Redis orchestration via Docker Compose

🧱 Pydantic models, SQLAlchemy ORM, and mypy type safety

🧰 Alembic migrations and modular, production-ready architecture

🧠 Tech Stack
Layer	Technology
API & Background Tasks	FastAPI, asyncio
Database & ORM	PostgreSQL, SQLAlchemy, Alembic
Queue / Stream	Redis (or Kafka optional)
DSL Parsing	Lark or Parsimonious
Notifications	Slack API, async HTTP
Metrics	Prometheus
Deployment	Docker Compose

🚀 Quick Start
bash
Copy code
# Clone the repo
git clone https://github.com/<your-username>/sentinel.git
cd sentinel

# Start the stack
docker-compose up --build
Test the API
bash
Copy code
curl -X POST http://localhost:8000/events \
  -H "Content-Type: application/json" \
  -d '{"type": "order", "amount": 750}'
📜 Example Rule
json
Copy code
{
  "name": "High value orders",
  "dsl": "when event.type == 'order' and amount > 500 then notify('slack:#big-orders')"
}
📊 Metrics
Sentinel exposes Prometheus metrics at:

bash
Copy code
GET /metrics
Example metrics:

events_ingested_total

rules_triggered_total

notifications_sent_total

🧰 Development
bash
Copy code
# Run lint and type checks
mypy .

# Run tests
pytest -v
🧱 Project Structure (suggested)
graphql
Copy code
sentinel/
│
├── api/                # FastAPI routers and endpoints
├── core/               # Config, logging, settings
├── db/                 # SQLAlchemy models + Alembic migrations
├── rules_engine/       # DSL parser, rule compiler, evaluator
├── workers/            # Async background tasks
├── notifiers/          # Slack, webhook, etc.
├── tests/              # Pytest-based tests
├── docker-compose.yml
├── requirements.txt
└── README.md