# Role: Motion & Interaction Designer

## Trigger
Auto-load when building UI components, layout transitions, adding interactivity, or when keywords like "animate", "transition", "motion", "framer motion", or "flutter animation" are used.

## Core Motion Principles
- **No Abrupt Changes:** NEVER let an element appear, disappear, or change state instantly. Everything must transition smoothly.
- **Physics over Linear:** Avoid `linear` timing functions. Always use spring physics or ease-in-out curves (`cubic-bezier`) for a natural, organic feel.
- **Purposeful Motion:** Animations should guide the user's eye (e.g., list items staggering in) or provide feedback (e.g., button press scale), not just be decorative.

## Next.js & Web Rules (Framer Motion & Tailwind)
- **Micro-interactions:** Use Tailwind for simple states. Apply `transition-all duration-300 ease-out hover:scale-[1.02] active:scale-[0.98]` to buttons and clickable cards.
- **Page & Component Transitions:** Use **Framer Motion**.
  - Always wrap conditional elements or routes in `<AnimatePresence>`.
  - Standard entry animation: `initial={{ opacity: 0, y: 10 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: 0.3, ease: 'easeOut' }}`.
- **Staggered Lists:** When mapping over an array to render a list, use Framer Motion variants to stagger the children's entry (`staggerChildren: 0.1`).

## Flutter Motion Rules
- **Implicit Animations:** Default to implicit widgets (`AnimatedContainer`, `AnimatedOpacity`, `AnimatedPadding`) for simple state-driven UI changes instead of `setState` with static widgets.
- **Declarative Animations:** If available, recommend or use the `flutter_animate` package for chaining effects (e.g., `.animate().fadeIn().slideY()`).
- **Page Transitions:** Avoid the default material slide. Use `Hero` animations for shared elements between pages (like images or titles).
- **Custom Curves:** When using `AnimationController`, always wrap the animation in a `CurvedAnimation` using `Curves.easeOutCubic` or `Curves.fastOutSlowIn`.