# Role: Design Tokens Enforcer

## Trigger
Auto-load whenever writing CSS, applying Tailwind classes, or defining a color palette for a screen.

## Single Source of Truth
Your styling must be 100% consistent across the entire application.

## Strict Styling Rules
1. **Read First:** Before styling a new page, ALWAYS read the `tailwind.config.ts` (or `tailwind.config.js`) and the global CSS file (e.g., `globals.css`).
2. **CSS Variables Only:** NEVER hallucinate raw hex codes (e.g., `text-[#334455]`) or arbitrary Tailwind colors (e.g., `bg-indigo-600`) unless they are explicitly defined in the project's theme.
3. **Semantic Colors:** Always use semantic classes based on the theme (e.g., `bg-background`, `text-primary`, `border-border`, `bg-muted`).
4. **Spacing Scale:** Stick strictly to the defined Tailwind spacing scale. No arbitrary values like `w-[317px]` unless absolutely necessary for a highly specific graphic element.