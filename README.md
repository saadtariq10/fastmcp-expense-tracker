# HITS – FastMCP Expense Tracker

A lightweight **Expense Tracker** built using **FastMCP** and **SQLite**.  
It exposes MCP tools to add, list, and summarize expenses, along with a resource endpoint for expense categories.

---

## Features

- Add expense entries with category and subcategory
- List expenses within a date range
- Summarize expenses by category
- Categories served from `categories.json`
- SQLite database auto-initialization
- Async database operations using `aiosqlite`
- Runs as an HTTP MCP server

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
```

---

## Requirements

- Python **3.13**
- Dependencies:
  - fastmcp
  - aiosqlite

---

## Installation

### 1. Create a virtual environment (recommended)

```bash
python -m venv .venv
source .venv/bin/activate   # macOS / Linux
# .venv\Scripts\activate    # Windows
```

### 2. Install dependencies

```bash
pip install fastmcp aiosqlite
```

Or using `pyproject.toml`:

```bash
pip install -e .
```

---

## Running the Server

```bash
python main.py
```

Server runs on:

- Host: `0.0.0.0`
- Port: `8000`

SQLite database (`expenses.db`) is created automatically.

---

## Database Schema

Table: `expenses`

- `id` – INTEGER (Primary Key)
- `date` – TEXT (`YYYY-MM-DD`)
- `amount` – REAL
- `category` – TEXT
- `subcategory` – TEXT
- `note` – TEXT

---

## MCP Tools

### add_expense
Adds a new expense entry.

### list_expenses
Lists expenses within a date range.

### summarize
Summarizes expenses by category.

---

## MCP Resource

### expense:///categories

Returns available categories from `categories.json`.

---

## Notes

- Dates must be in `YYYY-MM-DD` format
- Ensure write permissions for database file

---

## License

MIT
