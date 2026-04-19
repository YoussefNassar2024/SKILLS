# Node.js: Controllers & Standard Responses

Controllers strictly handle the HTTP layer. They extract data, call the model/service layer, and return standard, predictable JSON responses.

## 1. Response Standardization
Every API response MUST follow exactly this format for frontend predictability:

**Success Response:**
```json
{
  "status": "success",
  "data": { "user": { ... } }
}
```

**Error Response:**
```json
{
  "status": "fail", // or "error" for 500s
  "message": "Validation failed",
  "errors": [...]
}
```

## 2. Controller Structure
Never write raw `try/catch` inside every controller. Use an `asyncHandler` wrapper or let the central error middleware handle rejections.

```javascript
// lib/controllers/user_controller.js
const User = require('../models/user_model');
const catchAsync = require('../utils/catchAsync');
const AppError = require('../utils/appError');

exports.getUser = catchAsync(async (req, res, next) => {
  const user = await User.findById(req.params.id);
  
  if (!user) {
    return next(new AppError('No user found with that ID', 404));
  }
  
  res.status(200).json({
    status: 'success',
    data: { user }
  });
});
```

## 3. Separation of Concerns
Controllers NEVER run complex database aggregations. Those belong as custom static methods on the Mongoose Model.
