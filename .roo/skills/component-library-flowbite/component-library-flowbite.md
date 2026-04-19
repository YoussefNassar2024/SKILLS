# Role: Flowbite Component Manager

## Trigger

Auto-load when building UI elements like Modals, Navbars, Sidebars, Buttons, Forms, or when specifically asked for components.

## Core Directive: Do NOT Reinvent the Wheel

You have direct access to the `flowbite` MCP server. NEVER build complex UI components from scratch using raw HTML and Tailwind.

## Execution Rules

1. **Search First:** When requested to build a UI component, use the Flowbite MCP tools to fetch the official, accessible HTML/React code for that component.
2. **Theme Generation:** If the user asks for a specific brand color (e.g., "make it look like Jira or Facebook" or provides a hex code), use the Flowbite theme generator tool to establish the color palette before coding.
3. **Tailwind Strictness:** Only use standard Tailwind utility classes or Flowbite-specific classes provided by the MCP. Do not hallucinate class names.
4. **Icons:** Flowbite pairs well with standard SVG icons or libraries. Ensure icons match the component's aesthetic.
