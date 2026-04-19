# Role: Architecture & State Management Lead

## Trigger

Auto-load when setting up a project, managing data flow, fixing performance issues, or when keywords like "state", "store", "zustand", "riverpod", "bloc", "provider", or "architecture" are used.

## Core Architectural Directives

- **Separation of Concerns:** NEVER mix heavy business logic or API calls directly inside UI components. UI components should be "dumb" and only react to state changes.
- **Immutability:** Always treat state as immutable. Never mutate arrays or objects directly; always return new instances.
- **Single Source of Truth:** State should live in exactly one place to avoid synchronization bugs.

## Next.js & React State Rules

- **Global State:** Default to **Zustand** for global client state. It is lightweight and minimizes boilerplate. Do NOT use Redux unless explicitly requested.
- **Server vs Client:** Maximize the use of React Server Components (RSC) for data fetching. Keep Client Components (`"use client"`) at the leaves of the tree to reduce bundle size.
- **Data Fetching:** For client-side data fetching, caching, and optimistic updates, strongly prefer **TanStack Query (React Query)** or **SWR**.
- **Local State:** Use Context API ONLY for theming or dependency injection in compound components, not for rapidly changing state to avoid unnecessary re-renders.

## Flutter Architecture Rules

- **State Management:** Default to **Riverpod** (using Code Generation if possible) for state management and dependency injection. If the user prefers BLoC, follow strict BLoC event/state patterns.
- **Immutable States:** Always define state classes using the `freezed` package or `equatable`. This ensures value equality and prevents unnecessary UI rebuilds.
- **Handling Async Data:** Always handle the three distinct states of async operations explicitly: `Loading`, `Data` (Success), and `Error`. Use Riverpod's `AsyncValue.when()` to render UI accordingly.
- **Widget Purity:** Widgets should strictly be for UI. They should only listen to state (`ref.watch`) and dispatch actions/events (`ref.read(notifier.notifier).action()`).
