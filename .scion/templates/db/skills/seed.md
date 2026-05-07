---
name: seed
description: Design database schemas and generate realistic test seed data
---

# /seed — Design Schemas and Generate Seed Data

## Trigger

User invokes `/seed` with a target specification ID or domain entity list (e.g., `/seed "F-0031" "Customer, Order"`).

## Instructions

1. **Analyze Spec Requirements** — Read the product specification under `docs/specs/F-NNNN-*.md` to identify database entities, relational attributes, and constraints.
2. **Design Relational DDL Schema** — Create or update the logical schema under `db/schema.sql` or the next sequential migration file under `db/migrations/`:
   - Enforce primary and foreign keys.
   - Design appropriate indexes for foreign key columns to optimize query performance.
   - Set appropriate constraints (Not Null, Unique, Check constraints).
3. **Generate DML Seed Data** — Populate the designed tables under `db/data.sql` or the corresponding migration file with realistic, high-quality seed data:
   - Ensure referential integrity (parent rows must exist before child rows are inserted).
   - Use diverse, realistic test values (names, dates, statuses) rather than generic placeholders.
   - Provide at least 10-20 rows of interconnected data per table to facilitate comprehensive E2E and load testing.
4. **Stage & Commit Database Scripts** — Stage and commit the database assets:
   ```bash
   git -c user.name="Andrey Shakirov" -c user.email="andreyshakirov@google.com" add db/
   git -c user.name="Andrey Shakirov" -c user.email="andreyshakirov@google.com" commit -m "db: add relational schema and seed data for <spec-id>"
   ```
5. **Relational Schema Summary** — Present a database design report back to the team:
   - Newly created/updated tables, columns, and relationships.
   - Indexes added for query optimization.
   - Summary of generated seed data rows.
   - Relative markdown links to `db/schema.sql` and `db/data.sql`.

## Project Context

- **Project:** appteam
