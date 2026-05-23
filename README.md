# Book Tracker API — Week 3

A small FastAPI REST API for tracking books — read, reading, or want to read.
In-memory storage (resets on restart); persistence comes in Week 4.

## Run it

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload
```

- Welcome: <http://localhost:8000/>
- Interactive docs: <http://localhost:8000/docs>

## Endpoints

| Method | Path                       | Description                                |
|--------|----------------------------|--------------------------------------------|
| GET    | `/`                        | Welcome message                            |
| GET    | `/health`                  | Liveness probe                             |
| GET    | `/books`                   | List all books; `?status=` filter optional |
| POST   | `/books`                   | Create a book (201)                        |
| GET    | `/books/stats`             | Counts by status + average rating          |
| GET    | `/books/{book_id}`         | Fetch one book (404 if missing)            |
| PUT    | `/books/{book_id}`         | Partial update of status and/or rating     |
| DELETE | `/books/{book_id}`         | Remove a book                              |

`/books/stats` is intentionally declared before `/books/{book_id}` so the
literal route wins the match.
