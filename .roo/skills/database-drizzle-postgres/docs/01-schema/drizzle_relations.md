# Drizzle ORM + PostgreSQL Mandate

## 1. Setup & Connection

When setting up Drizzle with PostgreSQL, we distinguish between connection pooling (e.g., `pg` or `postgres.js`) and schema definitions.

```typescript
// db/index.ts
import { drizzle } from 'drizzle-orm/postgres-js';
import postgres from 'postgres';
import * as schema from './schema';

const queryClient = postgres(process.env.DATABASE_URL!);
export const db = drizzle(queryClient, { schema });
```

## 2. Schema Definition (`db/schema/`)

Always use the specialized `pg-core` imports.

```typescript
import { pgTable, text, serial, timestamp, boolean, uuid } from 'drizzle-orm/pg-core';
import { relations } from 'drizzle-orm';

export const users = pgTable('users', {
  id: uuid('id').defaultRandom().primaryKey(),
  email: text('email').notNull().unique(),
  name: text('name').notNull(),
  isActive: boolean('is_active').default(true),
  createdAt: timestamp('created_at').defaultNow(),
});

export const posts = pgTable('posts', {
  id: serial('id').primaryKey(),
  title: text('title').notNull(),
  content: text('content'),
  authorId: uuid('author_id').references(() => users.id),
});

// Relational queries support
export const usersRelations = relations(users, ({ many }) => ({
  posts: many(posts),
}));

export const postsRelations = relations(posts, ({ one }) => ({
  author: one(users, {
    fields: [posts.authorId],
    references: [users.id],
  }),
}));
```

## 3. Relational Queries 

Prefer Drizzle's Relation Queries API (`db.query`) over raw joins where deeply nested data is required, as it perfectly types the result mapping.

```typescript
// Fetch users with their latest active posts
const data = await db.query.users.findMany({
  with: {
    posts: {
      where: (posts, { eq }) => eq(posts.isActive, true),
      limit: 5
    }
  }
});
```

## 4. Migrations (`drizzle/`)

- Before interacting with the DB or writing arbitrary queries, MUST ensure schema is synchronized.
- Generate migrations: `npx drizzle-kit generate`
- DO NOT manually edit the `drizzle/000X_snapshot.json` files or `.sql` files once executed in production.
- If schema mismatches occur, use `npx drizzle-kit pull` to inspect current DB state.
