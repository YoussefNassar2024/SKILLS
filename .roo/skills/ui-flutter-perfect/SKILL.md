---
name: ui-flutter-perfect
description: Master rules for Flutter mobile and desktop UI perfection, pixel-perfect rendering, and implicit animations.
triggers:
  mode: ["code", "god", "architect"]
  file: ["*.dart"]
  keyword: ["flutter", "ui", "design", "animation", "layout", "mobile", "desktop", "adaptive"]
---

# Flutter "Perfect UI" Mandate

## 1. Pixel-Perfect Rendering & Typography
*   **Never rely on default Material spacing**. Flutter's default Material spacing is often too sparse for premium apps.
*   **Shadows**: Use layered `BoxShadow` for depth, NEVER a single heavy black shadow.
    ```dart
    BoxShadow(color: Colors.black.withOpacity(0.05), blurRadius: 10, offset: const Offset(0, 4)),
    BoxShadow(color: Colors.black.withOpacity(0.01), blurRadius: 2, offset: const Offset(0, 1)),
    ```
*   **Glassmorphism**: Use `BackdropFilter` combined with `Container(color: Colors.white.withOpacity(0.1))` and a subtle `Border.all(color: Colors.white.withOpacity(0.2))` for true glass effects.
*   **Typography**: Use `GoogleFonts` (e.g., Inter, SF Pro equivalents) and strictly define `letterSpacing`, `height` (line-height), and `fontWeight` for all TextStyles.

## 2. Fluid & Intuitive Animations
*   **No abrupt changes**. Every state change (hover, pressed, loaded) MUST be animated or transition smoothly.
*   **Implicit Animations**: Use `AnimatedContainer`, `AnimatedOpacity`, and `AnimatedPositioned` instead of raw `setState` blocks that cause jarring jumps.
*   **Hero Transitions**: Use `Hero` tags for images or cards navigating across routes.

## 3. Adaptive Mobile & Desktop Layouts
*   **The Cross-Platform Rule**: You must never hardcode a layout that only works on Mobile if compiling for Desktop/Web.
*   **Responsive Wrappers**: Always use `LayoutBuilder` or external responsive packages to switch from a `BottomNavigationBar` (Mobile) to a `NavigationRail` or Custom Sidebar (Desktop). 
*   **Hover States**: Mobile touch doesn't have hover, but Desktop does. All interactive buttons MUST have defined `onHover` states to feel native on PC.
*   **Safe Areas**: Always wrap top-level mobile scaffolds in `SafeArea` to avoid notches and hardware bars. Keep layout integrity intact.

## 4. Execution Requirement
Before writing Flutter UI code, execute your "Pre-flight" check to verify you are using the precise colors from the Theme Vault and that your layout accounts for both Desktop resizing and Mobile constraints. You MUST run `flutter analyze` after every major UI block.
