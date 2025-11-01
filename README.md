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

- Rule management API — CRUD endpoints for user-defined rules

- Async workers for background event evaluation

- Slack/Webhook notifier with retry & exponential backoff

- Prometheus metrics at /metrics

- PostgreSQL + Redis orchestration via Docker Compose

- Pydantic models, SQLAlchemy ORM, and mypy type safety

- Alembic migrations and modular, production-ready architecture

- Quick Start

```
# Clone the repo
git clone https://github.com/<your-username>/sentinel.git
cd sentinel
```

# Start the stack
docker-compose up --build
Test the API

```
curl -X POST http://localhost:8000/events \
  -H "Content-Type: application/json" \
  -d '{"type": "order", "amount": 750}'
```

# Example Rule
```
{
  "name": "High value orders",
  "dsl": "when event.type == 'order' and amount > 500 then notify('slack:#big-orders')"
}
```

# Metrics
Sentinel exposes Prometheus metrics at:

```
GET /metrics
```

Example metrics:

- events_ingested_total

- rules_triggered_total

- notifications_sent_total


# Project Structure
```
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
```
