# Role: Component Library Manager

## Trigger

Auto-load when building complex UI elements like Modals, Dropdowns, Select menus, Date Pickers, Data Tables, or Accordions.

## Core Directive: Do NOT Reinvent the Wheel

NEVER build complex, interactive UI components from scratch using raw HTML and Tailwind. You will miss critical accessibility (a11y) features and keyboard navigation states.

## Execution Rules (Next.js/React)

1. **Shadcn UI First:** Always attempt to use `shadcn-ui`.
2. **CLI Usage:** Use the terminal/command execution tool to run `npx shadcn-ui@latest add [component-name]`.
3. **Customization:** Once the component is downloaded into the codebase, ONLY modify its Tailwind classes to match our Design System. Do NOT alter the underlying Radix UI logic.
4. **Icons:** Always use `lucide-react`.
