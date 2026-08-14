# CineLog

A community film tracking app. Users log films they've watched, rate them, and build collections.

A Flask/SQLAlchemy API for tracking watched films and building collections. I implemented the watchlist feature end-to-end (deduplication logic + tests) on this branch, then worked through a full code review cycle — addressing six maintainer review comments and, along the way, recovering from a silent rebase that had dropped commits, by managing an interactive rebase back to a clean, conventional-commit linear history.

---

## Setup

```bash
pip install -r requirements.txt
python app.py
```

The app starts on `http://localhost:5000` and uses a local SQLite database (`cinelog.db`).

---

## Project Structure

```
ai201-project6-cinelog-starter/
├── app.py                     # Flask app factory
├── models.py                  # SQLAlchemy models
├── services/
│   └── collection_service.py  # Business logic for collections
├── routes/
│   ├── films.py               # Film browsing endpoints
│   └── collection.py          # Collection endpoints
├── tests/
│   └── test_collection.py     # Tests for collection service
├── CONTRIBUTING.md            # Commit conventions and PR guidelines
└── requirements.txt
```

---

## API Overview

### Films

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/films/` | List all films (supports `?genre=` and `?year=` filters) |
| GET | `/films/<film_id>` | Get a single film by UUID |

### Collection

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/collection/<user_id>` | Get a user's collection (newest first) |
| POST | `/collection/<user_id>/add` | Add a film to the collection |
| DELETE | `/collection/<user_id>/remove` | Remove a film from the collection |

---

## Data Models

**Film** — A film in the catalog. IDs are UUIDs.

**User** — A registered user. IDs are UUIDs.

**CollectionEntry** — Links a user to a film they've watched. Stores rating and date added. A user can only have one entry per film.

---

## Naming Conventions

Service functions follow a `verb_to_noun` pattern. See `CONTRIBUTING.md` for full details.

---

## Running Tests

```bash
pytest tests/
```
