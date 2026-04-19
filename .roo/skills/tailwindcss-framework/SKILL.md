---
name: tailwindcss-framework
description: Master rules for Next.js UI layout, Tailwind CSS v4 usage, Headless UI, and Magic UI integration.
triggers:
  mode: ["code", "god", "architect"]
  keyword: ["tailwind", "css", "layout", "flex", "grid", "page", "nextjs", "magic ui"]
---

# Next.js "Perfect UI" & Tailwind v4 Mandate

## 1. Layout Integrity (No More Broken Heights)
When building layouts (Sidebars, Dashboards, Full-page apps), you must PREVENT containers from cutting off or refusing to stretch.
*   **The Golden Wrapper**: The root wrapper MUST be `min-h-screen flex` (or `flex-col` depending on axis).
*   **The Stretching Content**: The main content area MUST have `flex-1` so it stretches to fill the gap left by headers/sidebars.
*   **No Fixed Arbitrary Heights**: DO NOT use `h-[800px]` or random fixed heights. Let flexbox define the height. Use `min-h-0` on scrollable flex children to prevent flex blowout.

## 2. Tailwind CSS v4 Architecture
Tailwind v4 is an engine shift. It uses CSS-first configuration.
*   **No `tailwind.config.js`**: Custom colors, fonts, and breakpoints are defined as native CSS variables inside the `@theme` block in `globals.css` or `app.css`.
*   **Example Setup**:
    ```css
    @import "tailwindcss";
    @theme {
      --color-primary: oklch(0.6 0.25 285);
      --font-display: "Clash Display", sans-serif;
    }
    ```
*   You use classes identically (`bg-primary`, `font-display`).

## 3. Component & UI Integration
*   **Headless UI / Shadcn**: Use these for complex accessible components (Dropdowns, Dialogs, Tabs) rather than building from scratch. Style them purely through Tailwind.
*   **Magic UI**: For premium "Wow" factor components (Marquees, Animated Counters, Blur Fades). Assume the user has `magic-ui-mcp` available. Check Magic UI docs using the MCP for the exact component implementation.
*   **Framer Motion**: Add `<motion.div>` to critical entry points. Example: `initial={{ opacity: 0, y: 10 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: 0.3 }}`.

## 4. Execution Requirement
Before writing any complex layout, you MUST verify in your thoughts: 
*"I have verified that the sidebar and main content are wrapped in a min-h-screen flex container, and the main content uses flex-1 to prevent height bugs."*
