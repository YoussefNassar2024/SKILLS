---
name: backend-nodejs-mongoose
description: Strict architectural mandates for Node.js + Mongoose backends, enforcing the required directory structure.
triggers:
  mode: ["code", "god", "architect"]
  keyword: ["node", "express", "mongoose", "backend", "api"]
---

# Node.js + Mongoose Architectural Mandate

You MUST adhere strictly to the following directory structure and naming conventions for all Node.js/Mongoose projects. NO EXCEPTIONS.

## 1. Directory Structure Rule
All application logic MUST reside in the `lib/` folder.
*   `lib/config/`
    *   `db.js` (Mongoose connection logic)
*   `lib/controllers/`
    *   Files MUST be named `[entity]_controller.js` (e.g., `user_controller.js`).
*   `lib/middleware/`
    *   Files MUST be named `[type]_middleware.js` (e.g., `error_middleware.js`, `auth_middleware.js`).
*   `lib/models/`
    *   Files MUST be named `[entity]_model.js` (e.g., `user_model.js`).
*   `lib/routes/`
    *   Files MUST be named `[entity]_routes.js` (e.g., `user_routes.js`).
*   `lib/utils/`
    *   Reusable logic (e.g., `enums.js`, `jwt_utils.js`).

## 2. Mongoose Schema Best Practices
*   **Timestamps**: Always enable `{ timestamps: true }` on every schema to automatically track `createdAt` and `updatedAt`.
*   **Virtuals**: Use virtuals for reverse relationships instead of embedding massive arrays of `ObjectId`s.
*   **Indexing**: Add `.index()` on frequently queried fields (like email, foreign keys) at the schema level.

## 3. Mandatory Dockerization
If creating a new backend, you MUST provide a robust `Dockerfile` exposing the correct port and using a slim Node.js alpine image.
