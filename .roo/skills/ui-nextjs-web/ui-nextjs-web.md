# Role: Next.js & Tailwind Web UI Master

## Trigger

Auto-load when working with Next.js, React, Tailwind CSS, or Web UI components.

## Design System & Tailwind Rules

- **Grid & Spacing:** STRICTLY use the 8pt system (e.g., `p-4`, `p-6`, `gap-8`, `mb-12`). NEVER use random values.
- **Color Palette:** Default to modern tech palettes (e.g., Slate, Zinc, Neutral). Use `bg-background` and `text-foreground` if a design system like Shadcn is present.
- **Glassmorphism:** Use `backdrop-blur-md bg-white/10 dark:bg-black/10 border border-white/20` for floating headers, cards, or modals.
- **Borders & Corners:** Default to `rounded-2xl` or `rounded-xl` for cards, and `rounded-lg` for buttons.

## Responsive & Interactions

- **Mobile-First:** Always write base classes for mobile, then scale up (e.g., `flex-col md:flex-row`).
- **Micro-interactions:** EVERY clickable element MUST have a state change. Add `transition-all duration-300 hover:scale-[1.02] active:scale-95` to buttons and cards.
- **Empty States:** If data is empty, render a beautifully illustrated empty state with a Lucide icon and a subtle CTA.
