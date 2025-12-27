```md
# HITS – FastMCP Expense Tracker

A lightweight **Expense Tracker** built using **FastMCP** + **SQLite**.  
It exposes MCP tools to **add expenses**, **list expenses**, and **summarize spending**, plus a resource endpoint for **categories**.

---

## Features

- ✅ Add an expense (date, amount, category, subcategory, note)
- ✅ List expenses within a date range
- ✅ Summarize totals by category (optionally filter by category)
- ✅ Categories resource served from `categories.json` (with a fallback default)
- ✅ SQLite database auto-initialization (`expenses.db`)
- ✅ Async DB operations using `aiosqlite`
- ✅ Runs as an HTTP MCP server

---

## Project Structure

```

saadtariq10-fastmcp-expense-tracker/
├── README.md
├── categories.json
├── main.py
├── pyproject.toml
├── requirements.txt
└── .python-version

````

---

## Requirements

- Python **3.13** (as per `.python-version`)
- Dependencies:
  - `fastmcp`
  - `aiosqlite`

---

## Setup

### 1) Create & activate a virtual environment (recommended)

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
# .venv\Scripts\activate    # Windows
````

### 2) Install dependencies

If you use `pyproject.toml`:

```bash
pip install -e .
```

Or install directly:

```bash
pip install fastmcp aiosqlite
```

(If your `requirements.txt` is usable, you can also do: `pip install -r requirements.txt`.)

---

## Run the Server

Start the MCP server:

```bash
python main.py
```

By default it runs on:

* **Host:** `0.0.0.0`
* **Port:** `8000`

You should see a log line showing the database path, e.g.:

```
Database path: .../expenses.db
```

> Note: The database file `expenses.db` will be created automatically in the same directory as `main.py`.

---

## Database

The server uses a local SQLite DB: `expenses.db`.

Table schema:

* `id` (auto-increment)
* `date` (TEXT, required, format: `YYYY-MM-DD`)
* `amount` (REAL, required)
* `category` (TEXT, required)
* `subcategory` (TEXT, optional)
* `note` (TEXT, optional)

---

## MCP Tools

### 1) `add_expense`

Adds a new expense record.

**Arguments**

* `date` (string) → `YYYY-MM-DD`
* `amount` (number)
* `category` (string)
* `subcategory` (string, optional)
* `note` (string, optional)

**Returns**

```json
{
  "status": "success",
  "id": 1,
  "message": "Expense added successfully"
}
```

---

### 2) `list_expenses`

Lists expenses within an inclusive date range.

**Arguments**

* `start_date` (string) → `YYYY-MM-DD`
* `end_date` (string) → `YYYY-MM-DD`

**Returns**
An array of expense objects ordered by newest first.

---

### 3) `summarize`

Summarizes total spend grouped by category within a date range.

**Arguments**

* `start_date` (string) → `YYYY-MM-DD`
* `end_date` (string) → `YYYY-MM-DD`
* `category` (string, optional) → filter to one category

**Returns**
Example:

```json
[
  { "category": "food", "total_amount": 1250.0, "count": 12 },
  { "category": "transport", "total_amount": 620.0, "count": 6 }
]
```

---

## MCP Resource

### `expense:///categories`

Returns categories as JSON.

* If `categories.json` exists → serves its contents
* If not → returns a default category list

---

## Categories

Edit `categories.json` to customize categories/subcategories.
Example top-level categories included:

* food
* transport
* housing
* utilities
* health
* education
* travel
* business
* misc
  … and more.

---

## Notes / Troubleshooting

### Database is read-only

If you get a “read-only mode” error:

* Ensure the folder containing `expenses.db` is writable
* Ensure `expenses.db` file permissions allow writing

### Date format

Use ISO date strings: `YYYY-MM-DD`
Example: `2025-12-27`

---

## License

MIT (or update this section with your preferred license)

```

