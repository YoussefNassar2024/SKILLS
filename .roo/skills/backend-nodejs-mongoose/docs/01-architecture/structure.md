# Node.js + Mongoose: Architectural Mandate

Our backend architecture strictly follows a decoupled, domain-driven design pattern to ensure scalability and maintainability.

## 1. Directory Structure

The `lib/` directory is the core of our application logic.

```
└── lib/
    ├── config/           # Database connections and app-wide configuration
    ├── controllers/      # Handles incoming HTTP requests and responses
    ├── middleware/       # Express middlewares (Auth, Errors, Logging)
    ├── models/           # Mongoose schemas and database models
    ├── routes/           # Express router definitions, mapping URLs to controllers
    └── utils/            # Shared utilities, calculations, enums
```

## 2. Controllers (`lib/controllers/*_controller.js`)
Controllers should be thin. They should parse the request (`req.body`, `req.params`), validate input (if not done in middleware), and call model methods or services.
- Always use `try...catch` blocks or a centralized `catchAsync` wrapper.
- Return standardized JSON responses: `{ status: 'success', data: { ... } }`.

## 3. Routes (`lib/routes/*_routes.js`)
Routes map HTTP verbs to controllers.
- Use `express.Router()`.
- Group common middlewares (e.g., `auth_middleware`) using `router.use()` or attach them to specific routes.
- Example: `router.post('/login', authController.login);`

## 4. Middleware (`lib/middleware/*`)
- **Error Handling**: Must be centralized in `error_middleware.js`. Do not leak stack traces in production.
- **Validation**: Use a validation layer (like `Joi` or `Zod`) before hitting the controller.

## 5. Configuration (`lib/config/*`)
- **Database Connection**: `db.js` must handle `mongoose.connect()` with proper retry logic, connection pooling options, and event listeners (`connected`, `disconnected`, `error`).
