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
- **Glassmorphism & Depth**: Use `backdrop-blur-xl` or `2xl` combined with semi-transparent borders (e.g., `border-white/20`) and massive layered shadows.
- **Theme Vault First**: You MUST start by picking a Persona from the `theme-vault-catalog`. Do NOT guess colors.
- **Absolute Contrast**: NEVER use white text on light colors. Text must always pass AAA contrast. Muted text should be at least `opacity-70`.
- **Typography**: Use modern fonts (Inter, SF Pro, Clash Display). Enforce hierarchy with massive headings and dense data tables.
- **Animations**: Use `framer-motion` (Next) or Implicit Animations (Flutter) for EVERY interactive element (hover, active, transition).
- **Layout Integrity**: NEVER use arbitrary fixed heights (like `h-64` for a sidebar). Use `min-h-screen` paired with `flex-1` for perfect stretchy layouts.

---

# Aesthetic Excellence & The "Perfect Designer"

## Instructions

1. **Theme Sync**: State your chosen Theme Vault Persona before writing anything.
2. **Consistency & Magic UI**: Check if a Magic UI component can do the job better before writing from scratch. Ensure all buttons use the project's primary action style (gradients + subtle shadows).
3. **Empty States**: Never show a blank page during loading; use shimmering skeletons or localized loaders.
4. **Interaction**: Add `transition-all` and `hover:scale-[1.02]` to interactive cards for a premium feel.
