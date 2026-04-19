---
name: database-drizzle-postgres
description: Master rules for Drizzle ORM paired with PostgreSQL, including migration structure and relational queries.
triggers:
  mode: ["code", "god", "architect"]
  keyword: ["drizzle", "postgres", "sql", "orm", "database"]
---

# PostgreSQL + Drizzle ORM Mandate

## 1. Directory Structure Rule
All Drizzle schemas and migrations MUST be isolated cleanly.
*   `drizzle/`
    *   `meta/` (Drizzle generated meta logs)
    *   `0000_snapshot.json` 
    *   `.sql` migration files
*   `lib/models/` or `db/schema/`
    *   Drizzle schema definitions using PostgreSQL dialet imports (`pgCore`).

## 2. Drizzle Best Practices
*   **Imports**: ALWAYS import from `drizzle-orm/pg-core` for Postgres. Do NOT use MySQL/SQLite imports by mistake.
*   **Relations**: Expose relations specifically using Drizzle's `relations()` API to allow for efficient nested queries (`db.query.users.findMany({ with: { posts: true } })`).
*   **Safety & Migrations**: BEFORE modifying a schema, you MUST review the current schema and existing migrations. Never overwrite past `.sql` migrations once applied. Add new ones `npx drizzle-kit generate`.

## 3. Mandatory Environment
Always ensure `drizzle.config.ts` (or `.js`) points to the correct Database URL sourced securely from environment variables, never hardcoded.
