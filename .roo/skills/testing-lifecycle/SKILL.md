---
name: testing-lifecycle
description: ---
name: Testing Lifecycle & Verification Mandate
description: Enforces TDD, unit test coverage, and E2E verification
triggers:
  mode: ["code", "review", "tester"]
  keyword: ["test", "spec", "vitest", "playwright", "cypress", "validation", "verify", "assert"]
---

### TESTING RULES
- **Unit Testing**: Use `Vitest` for logic, helpers, and Server Component logic. Coverage > 80% for new features.
- **Component Testing**: Use `React Testing Library` for Client Components and user interactions.
- **E2E Testing**: Use `Playwright` for critical business flows (e.g., submitting a Risk report).
- **Automation**: Run `npm test` before marking any step as completed in `PIPELINE_STATE.md`.
- **Fail First**: When fixing a bug, first write a failing test that reproduces the issue.

---

# Testing Lifecycle

## Instructions

1. **Test Location**: Put unit tests in `__tests__/` mirroring the `app/` structure.
2. **Mocking**: Use `vi.mock` for external services and database calls.
3. **Snapshots**: Use snapshots sparingly; prefer explicit property assertions for stability.
4. **CI Readiness**: Ensure all tests run in headless mode and don't rely on local environment variables without defaults.
