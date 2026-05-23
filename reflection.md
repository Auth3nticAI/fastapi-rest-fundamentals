# Week 3 Reflection

## 1. What was the most confusing thing about Python compared to JavaScript?

Indentation as syntax. In JS, whitespace is decorative — braces define blocks. In
Python, the indentation *is* the block, so a stray space or a tab/space mix is a
parse error, not a style issue. The other adjustment was decorators (`@app.get(...)`)
and the fact that there's no `function` keyword or `;` line terminators. The flow
feels lighter once it clicks but the silence around block boundaries is
disorienting at first.

## 2. What does an HTTP status code tell you? Give one example.

It's a one-line summary of what happened to the request, agreed on by every web
client and server. 2xx = it worked, 4xx = the caller did something wrong, 5xx =
the server broke. Example: `GET /books/999` on a missing book returns `404 Not
Found` — the route exists but the resource doesn't, so the client knows the
problem is the id, not the URL or the server.

## 3. What was the difference between a path parameter and a query parameter?

Path parameters are part of the URL itself and identify *which* resource —
`/books/2` means "the book with id 2." They're typically required and the route
won't match without them. Query parameters come after `?` and *modify* a request
on a route that already makes sense without them — `/books?status=reading` says
"list books, but filter to reading." In FastAPI, function arguments that appear
inside `{}` in the path string become path params; everything else becomes a
query param.

## 4. What happens to the data if the server restarts?

It all disappears. `books_db = []` and `next_id = 1` live in process memory, so
killing uvicorn wipes every book. That's a problem for anything beyond a demo —
real apps need state to survive restarts, deploys, and crashes. The fix is a
database. Next week (Week 4) we'll swap the in-memory list for PostgreSQL via
SQLAlchemy, so writes persist to disk and survive restarts.
