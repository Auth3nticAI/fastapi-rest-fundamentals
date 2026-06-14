# FastAPI REST Fundamentals

> A FastAPI starter API — REST endpoints, Pydantic validation, automatic OpenAPI/Swagger docs. In-memory state (no database yet) so the focus stays on the HTTP layer.

![FastAPI](https://img.shields.io/badge/FastAPI-0.136-009688?style=flat&logo=fastapi&logoColor=white)
![Pydantic](https://img.shields.io/badge/Pydantic-2.13-E92063?style=flat&logo=pydantic&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=flat&logo=python&logoColor=white)

---

## What's interesting

- **Pydantic at the boundary** — `BookCreate` validates inbound POST bodies; `BookUpdate` allows partial updates with all optional fields.
- **Route-order awareness** — literal `/books/stats` declared *before* dynamic `/books/{book_id}` so FastAPI doesn't try to parse `"stats"` as an int and 422.
- **In-memory list with a separate `next_id`** — illustrates why the next step in the course is Postgres + SQLAlchemy.

## Endpoints

| Method | Path | Purpose |
|---|---|---|
| `GET` | `/health` | Health check |
| `GET` | `/books` | List (filter by `?status=`) |
| `POST` | `/books` | Create |
| `GET` | `/books/stats` | Count by status + average rating |
| `GET` | `/books/{id}` | Read one |
| `PUT` | `/books/{id}` | Update status / rating |
| `DELETE` | `/books/{id}` | Delete |

## Run

```bash
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload
```

Open http://localhost:8000/docs for Swagger.

## Background

Built as the Week 3 lab for **CSE552 — Fullstack Software Development in the Age of AI Agents**. The Postgres-backed version is at [fastapi-postgres-crud](https://github.com/Auth3nticAI/fastapi-postgres-crud).
