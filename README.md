# Sentinel – Event Ingestor and Rule Engine

**Sentinel** is a lightweight event-driven alerting service that ingests JSON events via HTTP or streams (Redis/Kafka) and evaluates user-defined rules written in a tiny DSL (Domain-Specific Language). When a rule matches an event, Sentinel triggers asynchronous notifications such as Slack or webhooks.

This project demonstrates an end-to-end async Python backend using FastAPI, SQLAlchemy, asyncio workers, and a custom DSL parser built with Lark.

---

## ✨ Features

- **Event ingestion** via HTTP (`POST /events`) or async queue
- **Rule engine** with DSL syntax:
  ```text
  when event.type == "order" and amount > 500 then notify("slack:#big-orders")