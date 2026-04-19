# Mongoose Schema & Best Practices

## 1. Schema Design Conventions
All Mongoose models must reside in `lib/models/` and follow the `*_model.js` naming convention.

```javascript
const mongoose = require('mongoose');

const UserSchema = new mongoose.Schema({
  email: {
    type: String,
    required: [true, 'Email is required'],
    unique: true,
    lowercase: true,
    trim: true,
    index: true // Ensure frequent lookups are indexed
  },
  role: {
    type: String,
    enum: ['user', 'admin'],
    default: 'user'
  }
}, {
  timestamps: true, // ALWAYS enable this to automatically get createdAt, updatedAt
  toJSON: { virtuals: true }, 
  toObject: { virtuals: true }
});

// Example of a reverse relationship virtual
UserSchema.virtual('posts', {
  ref: 'Post',
  localField: '_id',
  foreignField: 'author'
});

const User = mongoose.model('User', UserSchema);
module.exports = User;
```

## 2. Advanced Indexing
- **Single Field Indices**: Add `index: true` directly in the schema definition for fields commonly used in `find()` or `sort()` operations (e.g., `status`, `createdAt`, `email`).
- **Compound Indices**: For queries that span multiple fields, define them at the schema level:
  `UserSchema.index({ role: 1, createdAt: -1 });`

## 3. Query Optimization
- Use `.lean()` when fetching data purely for reading (API responses) where Mongoose documents (which are heavy) are not needed.
- Use `.select()` carefully to exclude heavy or sensitive fields: `.select('-password -__v')`.

## 4. Middleware (Hooks)
Use Mongoose pre/post hooks to encapsulate logic:
- Hashing passwords before save: `UserSchema.pre('save', async function(next) { ... })`
- Populating default fields across queries: `UserSchema.pre(/^find/, function(next) { this.populate('profile'); next(); })`
