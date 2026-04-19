# FastAPI: Async Database Integration

FastAPI shines brightest when the database calls are fully asynchronous. 

## 1. Async SQLAlchemy (SQLModel)
Always use `AsyncSession` from `sqlalchemy.ext.asyncio` rather than blocking synced sessions.

```python
# app/db/session.py
from sqlalchemy.ext.asyncio import create_async_engine, AsyncSession
from sqlalchemy.orm import sessionmaker

engine = create_async_engine("postgresql+asyncpg://user:pass@localhost/db", echo=True)
AsyncSessionLocal = sessionmaker(engine, class_=AsyncSession, expire_on_commit=False)

async def get_db():
    async with AsyncSessionLocal() as session:
        yield session
```

## 2. Advanced Route Examples
Use async/await uniformly across route definitions when working with async databases or external APIs.

```python
@router.post("/", response_model=UserResponse, status_code=201)
async def create_user(
    *,
    db: AsyncSession = Depends(get_db),
    user_in: UserCreate,
) -> Any:
    """Create a new user securely."""
    # Logic goes heavily to CRUD
    user = await crud_user.get_by_email(db, email=user_in.email)
    if user:
        raise HTTPException(
            status_code=400,
            detail="The user with this username already exists in the system.",
        )
    user = await crud_user.create(db, obj_in=user_in)
    return user
```

## 3. Dependency Scope
Remember that `Depends(get_db)` opens and closes the connection *per request*. Never leak sessions across requests or store them in global scope.
