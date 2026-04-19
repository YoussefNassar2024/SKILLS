# Postgres + Drizzle: Migrations & Deep Seeding

## 1. Migration Philosophy (`drizzle/`)
Drizzle manages schema via snapshot definitions and exact `.sql` scripts.
- Only run `npx drizzle-kit generate` during active development to scaffold tables.
- NEVER delete or manually alter old `000*.sql` files after committing. If you make a mistake, roll back the DB explicitly or create a NEW migration fixing the issue.
- Applying schema in production runs `drizzle-orm/node-postgres/migrator`.

```typescript
// db/migrate.ts
import { migrate } from 'drizzle-orm/postgres-js/migrator';
import { db, connection } from './index';

async function performMigration() {
  await migrate(db, { migrationsFolder: 'drizzle' });
  await connection.end();
}
```

## 2. Advanced Relational Seeds
Seeding the DB should reflect real-world relationships. Use Drizzle's typed insertions to populate lookup tables, users, and massive data sets reliably.

```typescript
import { db } from './index';
import { users, roles } from './schema';

export async function seed() {
  const [adminRole] = await db.insert(roles)
    .values({ name: 'Admin', code: 'ADM' })
    .returning({ id: roles.id });

  await db.insert(users).values({
    email: 'admin@system.local',
    name: 'Super Admin',
    roleId: adminRole.id
  });
}
```

## 3. Query Optimization Context
When dealing with complex aggregations, favor `.execute()` with raw SQL templates (`sql\`...\``) from drizzle rather than constructing unstable chained ORM logic if it exceeds 3 levels of joins.
