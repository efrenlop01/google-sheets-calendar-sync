# Google Sheets → Google Calendar Sync (Apps Script)

## Overview
This project automates the creation, updating, and cancellation of Google Calendar events directly from a structured Google Sheet using Google Apps Script.

It was designed for scheduling Special Education IEP meetings but is flexible enough to support any workflow where a spreadsheet acts as the source of truth for calendar events.

The system is **rate-limit safe**, **idempotent**, and includes built-in validation, error reporting, and duplicate prevention.

---

## Key Features

- ⏱️ Time-driven automation (runs every 15 minutes)
- 📅 Creates and updates Google Calendar events
- ❌ Automatically deletes events when `Status = CANCELLED`
- 🔁 Prevents duplicate events using stored Event IDs
- 🧠 Change detection using a generated Sync Key
- 🕒 Tracks last successful sync with timestamp
- ⚠️ Row-level validation with error messages written back to the sheet
- 🧾 Supports extra “reference-only” columns that are ignored by Calendar
- 🔐 No external APIs or paid services required

---

## Architecture

**Source of Truth**
- Google Sheet tab (e.g. `chen train`)

**Identity & Updates**
- Each calendar event’s ID is stored in the sheet
- Events are updated in place (not recreated)

**Change Detection**
- A Sync Key is generated per row
- Calendar updates only occur when row data changes

**Observability**
- Errors are written to an `Error` column
- Each row logs a `Last Synced` timestamp

---

## Sheet Structure

Required columns (example order):

| Column | Name |
|------|------|
| A | Title |
| B | Students Name |
| C | Case Manager |
| D | Type of Meeting |
| E | Language - Interpreter |
| F | Start Date |
| G | Start Time |
| H | End Time |
| I | Location |
| J | Counselor |
| K | General ED |
| L | Admin |
| M | Language - Interpreter Name |
| N | Psychologist |
| O | Front Office |
| P | Event ID *(auto-generated)* |
| Q | Status |
| R | Error *(auto-generated)* |
| S | IEP Due Date *(ignored by script)* |
| T | Attempted Contact *(ignored by script)* |
| U | Sync Key *(auto-generated)* |
| V | Last Synced *(auto-generated)* |

---

## Workflow Example

1. Add a new row → Calendar event is created
2. Edit date/time/location → Event is updated
3. Set `Status = CANCELLED` → Event is deleted
4. Fix any validation issues shown in `Error` column
5. Sync runs automatically every 15 minutes

---

## Installation

See [`docs/setup.md`](docs/setup.md) for full installation steps.

---

## Privacy & Security

- No student or personal data is included in this repository
- Sample files use fake names and placeholder values
- Calendar ID is intentionally excluded from version control

---

## Why This Project Matters

This automation reduces:
- Manual scheduling errors
- Duplicate calendar invites
- Administrative overhead

It demonstrates real-world skills in:
- Workflow automation
- Data validation
- Event-driven design
- Google Workspace scripting
- Operational reliability

---

## License
MIT License
