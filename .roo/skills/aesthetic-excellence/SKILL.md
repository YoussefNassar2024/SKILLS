---
name: aesthetic-excellence
description: ---
name: Aesthetic Excellence & UI Mandate
description: Enforces premium design standards, Tailwind 4 theme usage, and micro-animations
triggers:
  mode: ["code", "review"]
  file: ["*.css", "*.tsx", "*.js"]
  keyword: ["style", "color", "glassmorphism", "animation", "motion", "gradient", "backdrop", "theme"]
---

### AESTHETIC RULES
- **Glassmorphism**: Use `backdrop-blur-*` and semi-transparent borders for modals and cards.
- **Color Palette**: Use CSS variables defined in `@theme` (Tailwind 4). Avoid hardcoded hex codes.
- **Typography**: Use modern fonts (Inter/Outfit). Enforce hierarchy with correctly sized headings.
- **Animations**: Use `framer-motion` or CSS transitions for all button hovers and modal entries.
- **Responsiveness**: Use Tailwind 4 container queries and logical properties for layout.
- **Icons**: Use `Lucide` icons or equivalent premium sets. Ensure consistent sizing.

---

# Aesthetic Excellence

## Instructions

1. **Theme Sync**: Before adding a new color, check if it exists in the `@theme` block of `app/globals.css`.
2. **Consistency**: Ensure all buttons use the project's primary action style (gradients + subtle shadows).
3. **Empty States**: Never show a blank page during loading; use shimmering skeletons or localized loaders.
4. **Interaction**: Add `transition-all` and `hover:scale-[1.02]` to interactive cards for a premium feel.
