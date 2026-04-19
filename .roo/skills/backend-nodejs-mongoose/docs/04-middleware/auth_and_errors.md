# Node.js: Middleware (Auth & Errors)

Middlewares form the defensive layer around our endpoints. They must be robust and failure-proof.

## 1. Error Handling Middleware
Located at `lib/middleware/error_middleware.js`, this captures warnings, validation errors, and crashes.

- Mongoose Validation Errors: Must be mapped to readable 400 responses.
- JWT Errors: Must return a standardized 401 Unauthorized.
- Duplicate Key (`code 11000`): Map to 409 Conflict.

```javascript
module.exports = (err, req, res, next) => {
  err.statusCode = err.statusCode || 500;
  err.status = err.status || 'error';

  if (process.env.NODE_ENV === 'development') {
    res.status(err.statusCode).json({
      status: err.status,
      error: err,
      message: err.message,
      stack: err.stack
    });
  } else {
    // Production: DO NOT leak error stack
    res.status(err.statusCode).json({
      status: err.status,
      message: err.isOperational ? err.message : 'Something went very wrong!'
    });
  }
};
```

## 2. Authentication Middleware
Protecting routes is done via stateless JWT.

```javascript
// lib/middleware/auth_middleware.js
exports.protect = catchAsync(async (req, res, next) => {
  // 1. Get token
  let token;
  if (req.headers.authorization?.startsWith('Bearer')) {
    token = req.headers.authorization.split(' ')[1];
  }
  
  if (!token) return next(new AppError('You are not logged in!', 401));

  // 2. Verification
  const decoded = await promisify(jwt.verify)(token, process.env.JWT_SECRET);

  // 3. Check if user still exists
  const currentUser = await User.findById(decoded.id);
  if (!currentUser) return next(new AppError('User no longer exists.', 401));

  // Grant Access
  req.user = currentUser;
  next();
});
```
