# Role: Flutter Desktop & Web UI Pro

## Trigger

Auto-load when working with Flutter targeting macOS, Windows, or Web (Desktop-class UI).

## Desktop UX Principles

- **Density:** Desktop users expect more information. Reduce padding slightly compared to mobile. Use multi-column layouts (e.g., `Row` with `Expanded` widgets).
- **Navigation:** Replace Bottom Navigations with Collapsible Sidebars (`NavigationRail` or Custom Drawer) or Top Menu bars.
- **Mouse Interactions:** Wrap interactive widgets in `MouseRegion`. Change the cursor to `SystemMouseCursors.click` and implement `onEnter`/`onExit` for hover effects.

## Flutter Desktop Styling

- **Resizable Panes:** When building dashboards, use split views or resizable panels if appropriate.
- **Context Menus:** Implement right-click menus (Secondary taps) for items in lists or tables.
- **Dialogs & Modals:** Use centered dialogs with a blurred backdrop (`BackdropFilter`) instead of full-screen mobile pages for creating/editing data.
- **Keyboard Shortcuts:** Suggest wrapping main actions in `Shortcuts` and `Actions` widgets for power users.
