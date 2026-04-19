---
name: drizzle-orm
description: ---
name: Drizzle ORM Conventions
description: Replaces Prisma with Drizzle schema, migration, and query rules
triggers:
  mode: ["code", "review", "debug"]
  file: ["*.ts", "*.sql", "drizzle.config.*"]
  keyword: ["schema", "drizzle", "pgTable", "mysqlTable", "db.", "migration"]
---

### DRIZZLE ORM CONVENTIONS (PRISMA REPLACEMENT)
- Schema: Define in `src/db/schema.ts` using `pgTable`/`mysqlTable`, `serial`, `varchar`, `relations()`.
- Migrations: `npx drizzle-kit generate` → `npx drizzle-kit push` (dev) or `migrate` (prod).
- Queries: `drizzle-orm` builder (`db.select()`, `db.insert()`, `.where()`, `.innerJoin()`).
- NO `.prisma` files. NO `prisma generate`. NO Prisma Client.
- Validate: `npx tsc --noEmit` + `npx drizzle-kit check`.
- Always type DB responses explicitly; Drizzle is TypeScript-native, not codegen-heavy.
- Use `db.transaction()` for multi-table writes. Enforce indexes & foreign keys explicitly.
---

# Drizzle Orm

## Instructions

Add your skill instructions here.
