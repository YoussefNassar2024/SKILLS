---
name: backend-python-fastapi
description: Master rules for writing modern FastAPI backends using Pydantic V2 and Dependency Injection.
triggers:
  mode: ["code", "god", "architect"]
  keyword: ["fastapi", "python", "backend", "pydantic", "api"]
---

# FastAPI "Golden Rules" Mandate

## 1. Pydantic v2 & Type Safety
*   **Modern Python Types**: Always use standard Python type hints (e.g., `list[str]`, `dict[str, int]`, `str | None`) instead of the deprecated `typing` module imports (`List`, `Optional`, `Dict`).
*   **Pydantic V2**: Use `model_validator(mode='before')` and `Field(...)` explicitly. NEVER use deprecated v1 methods like `@root_validator` or `.dict()`. Use `.model_dump()` instead.

## 2. Directory Structure Requirement
Unless strictly building a single-file microservice, follow this domain-driven structure:
*   `app/core/` (settings, logging, auth logic)
*   `app/api/routes/` (APIRouter endpoints)
*   `app/models/` (Database ORM models)
*   `app/schemas/` (Pydantic validation models)
*   `app/crud/` (Database operations, never in the route)

## 3. Dependency Injection (DI)
*   Never instantiate database sessions inside routes. Always inject them: `db: Session = Depends(get_db)`.
*   Inject authentication contexts: `current_user: User = Depends(get_current_active_user)`.

## 4. Mandatory Dockerization
You MUST supply an optimized `Dockerfile` using a python slim image, utilizing Multi-stage builds if dependencies are heavy, and running the app with `uvicorn` or `gunicorn` with worker management.
