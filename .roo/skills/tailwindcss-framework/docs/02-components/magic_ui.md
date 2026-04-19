# Tailwind CSS v4 + Magic UI

## 1. Component Strategy
Magic UI provides highly animated, modern web primitives. When the prompt calls for "wow factor", "animated landing page", or "premium interactions", this is your arsenal.

## 2. Core Magic UI Replacements
Instead of building from scratch, map standard requests to these components:
- **Alerts/Notifications**: Use Magic UI's `Animated List` or `Ripple`.
- **Text Headers**: Use `Blur Fade` for revealing text on scroll (critical for modern layouts).
- **Hero Backgrounds**: Instead of solid colors or simple gradients, use `Retro Grid`, `Dot Pattern`, or `Meteors`.
- **Buttons**: Replace standard Tailwind buttons with `Shimmer Button` or `Border Beam` configurations for CTAs.

## 3. Framer Motion Integration
All custom micro-interactions that Magic UI doesn't provide must be built with `framer-motion`.

```tsx
import { motion } from 'framer-motion'

export const GlassCard = ({ children }) => (
  // Note the combination of v4 layout variables + framer animation
  <motion.div
    whileHover={{ scale: 1.02, y: -5 }}
    transition={{ type: "spring", stiffness: 300, damping: 20 }}
    className="bg-surface-light/50 backdrop-blur-3xl border border-white/10 rounded-3xl p-6 shadow-2xl"
  >
    {children}
  </motion.div>
)
```
