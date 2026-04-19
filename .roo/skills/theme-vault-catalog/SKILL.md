---
name: theme-vault-catalog
description: A mandatory pre-flight check and repository of hundreds of aesthetic design presets that the AI MUST choose from before writing any UI code.
triggers:
  mode: ["code", "god", "architect"]
  keyword: ["theme", "design", "layout", "colors", "persona", "ui", "ux", "create a page"]
---

# The Theme Vault Mandate

## Core Directive: ZERO RANDOM DESIGN
You are formally FORBIDDEN from making up random color palettes, margins, or UI styles when starting a project or a new page. You MUST use a predefined "Design Persona" from the Theme Vault.

## The Pre-flight Protocol
Before outputting any UI code (Next.js, Tailwind, or Flutter), you MUST execute the following pre-flight check in your response:

```markdown
### 🎨 Pre-flight Design Check
- **Selected Persona**: [e.g., Cyberpunk 2077]
- **Primary Color**: [e.g., oklch(0.6 0.25 285)]
- **Layout Integrity**: Verified `min-h-screen`, `flex-1` constraint for core container.
- **Framework Strategy**: [e.g., Next.js with Magic UI & Tailwind v4]
```

## Referencing the Catalog
The full catalog of aesthetic themes (100+ Personas) is located at `docs/catalog.md` within this skill.
If you do not have it memorized, read `docs/catalog.md`.

## Enforcement Rules
1. **Never use pure white backgrounds** (`#FFFFFF` or `bg-white`) on light mode if the Persona dictates off-white surfaces (`bg-slate-50` or `oklch(0.98 0 0)`). 
2. **Never mix rounding**: If the Persona says "Radius: 0px (Brutalist)", you must NOT use `rounded-xl` anywhere.
3. **Contrast Mandate**: Text must always meet WCAG AAA contrast ratio against its background surface.
