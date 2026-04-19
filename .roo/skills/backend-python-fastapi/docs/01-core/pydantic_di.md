# FastAPI: Pydantic v2 & Dependency Injection

Our FastAPI APIs strictly adhere to robust software engineering principles to guarantee type safety and maintainability.

## 1. Pydantic v2 Best Practices (`app/schemas/`)
With Pydantic v2, significant performance and syntax improvements were introduced. All data validation schemas must follow these rules:

- **Type Annotations**: Use native Python 3.10+ types (`str | None` instead of `Optional[str]`).
- **Configuration**: Use Model configuration classes (`model_config`).
- **Dumping**: Use `.model_dump()` replacing `.dict()`.

```python
from pydantic import BaseModel, ConfigDict, Field, EmailStr

class UserBase(BaseModel):
    model_config = ConfigDict(from_attributes=True) # Replaces orm_mode=True
    
    email: EmailStr
    is_active: bool = True
    full_name: str | None = Field(default=None, max_length=50)

class UserCreate(UserBase):
    password: str = Field(min_length=8)

class UserResponse(UserBase):
    id: int
```

## 2. Dependency Injection (`app/api/dependencies/`)
FastAPI’s DI system resolves dependencies before a route executes. We use this strictly for:
- Database Sessions
- Authentication / Current User
- Pagination contexts

**Rule**: Never initialize the database session inside the route handler.

```python
from fastapi import Depends, HTTPException, status
from sqlalchemy.orm import Session
from app.db.session import get_db

def get_current_user(token: str = Depends(oauth2_scheme), db: Session = Depends(get_db)):
    user = authenticate_token(token, db)
    if not user:
        raise HTTPException(status_code=status.HTTP_401_UNAUTHORIZED, detail="Invalid token")
    return user
```

## 3. Router Isolation (`app/api/routes/`)
Routes must be clean. Business logic goes into `crud/` or `services/`.

```python
from fastapi import APIRouter, Depends
from app.schemas.user import UserResponse
from app.api.dependencies import get_db, get_current_user
from sqlalchemy.orm import Session
from app.crud import user as crud_user

router = APIRouter()

@router.get("/me", response_model=UserResponse)
def read_current_user(current_user: User = Depends(get_current_user)):
    return current_user
```
