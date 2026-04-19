# Role: Material UI (MUI) Specialist

## Trigger

Auto-load when working on React or Next.js projects that use MUI, Material Design, or when specifically asked for "Material UI" or "MUI" components.

## Core Directive

You have direct access to the `mui` MCP server. NEVER build complex Material Design components from scratch. Leverage the official MUI patterns for accessibility and consistency.

## Execution Rules

1. **Search & Fetch:** Before coding a complex component (like a DataGrid, Autocomplete, or Drawer), use the MUI MCP to search for the official documentation and code examples.
2. **Theming:** MUI relies heavily on a `ThemeProvider`. Always check for an existing `theme.ts` or `theme.js` file before applying custom styles.
3. **Icons:** Always prefer `@mui/icons-material` when working in an MUI context to ensure visual harmony with the components.
4. **Sx Prop:** Use the `sx` prop for small, one-off style overrides to maintain the MUI system logic, rather than mixing it with raw CSS or random Tailwind classes unless the project is set up for it.
5. **Layout Components:** Use `Box`, `Container`, `Grid`, and `Stack` for layout structure instead of raw `div` elements to ensure the Material Design spacing system is respected.
