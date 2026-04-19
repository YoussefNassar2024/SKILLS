# Tailwind CSS v4: Core Architecture

Tailwind CSS v4 is a significant shift from previous versions. It is a CSS-native engine. We do not use `tailwind.config.js` or `tailwind.config.ts`. All configuration is done inside CSS using the `@theme` directive.

## 1. The Entry Point: CSS First
Your `app/globals.css` or `styles.css` is the heart of the engine.

```css
@import "tailwindcss";

@theme {
  /* 
    Tokens map to class names. 
    --color-brand-blue will generate text-brand-blue, bg-brand-blue, etc. 
  */
  --color-brand-primary:   oklch(0.5 0.2 260);
  --color-brand-secondary: oklch(0.6 0.25 300);
  --color-surface-light:   oklch(0.99 0.01 260);
  --color-surface-dark:    oklch(0.15 0.05 270);

  /* Typography */
  --font-display: "Clash Display", "Mona Sans", sans-serif;
  --font-body: "Inter", sans-serif;

  /* Custom Spacing / Shadows */
  --shadow-neon: 0 0 10px var(--color-brand-primary), 0 0 20px var(--color-brand-primary);
  --radius-extreme: 48px;
}

/* Custom utilities */
@utility glass-card {
  background-color: rgb(255 255 255 / 0.1);
  backdrop-filter: blur(24px);
  border: 1px solid rgb(255 255 255 / 0.2);
}
```

## 2. Layout Integrity: The Stretchy Constraint
Next.js Layouts must never cut off prematurely.

```tsx
// app/layout.tsx
export default function RootLayout({ children }) {
  return (
    <html lang="en">
      <body className="min-h-screen flex flex-col font-body bg-surface-light antialiased text-slate-800">
        <GlobalNavbar />
        {/* flex-1 mandates this container pushes the footer down to fill the screen */}
        <main className="flex-1 flex w-full">
           {children}
        </main>
        <GlobalFooter />
      </body>
    </html>
  );
}
```

## 3. Dark Mode
In v4, dark mode relies strictly on the `prefers-color-scheme` media query by default. If manual toggle is needed via classes, use the `dark:` variant and coordinate with the `ThemeProvider` from `next-themes`.

```tsx
<div className="bg-surface-light dark:bg-surface-dark transition-colors duration-300">
   <h1 className="text-brand-primary dark:text-brand-secondary">Hello</h1>
</div>
```

## 4. Complex UIs & Component Libraries
We use a hybrid approach to UI components to achieve maximum speed and aesthetic quality.

- **DaisyUI 5**: Use DaisyUI class names (`btn`, `card`, `input`) for all standard UI primitives. Remember that DaisyUI 5 is native to Tailwind v4, so you only need `@plugin "daisyui";` in `globals.css`. Never use `tailwind.config.js`. Customize DaisyUI using the Theme Vault variables.
- **Headless UI / Radix UI**: Use these for complex accessible components (Dropdowns, Tabs) if DaisyUI doesn't cover the specific interaction need.
- **Magic UI**: Use Magic UI purely for premium "Wow" factor components (Marquees, Animated Counters, Blur Fades, Retro Grids). 

```tsx
// Using DaisyUI (standard) + Magic UI (wow factor)
<div className="card bg-base-100 shadow-xl">
  <div className="card-body">
    <h2 className="card-title">Standard DaisyUI Card</h2>
    <BlurFade> {/* Magic UI Wrapper */}
       <button className="btn btn-primary">DaisyUI Button</button>
    </BlurFade>
  </div>
</div>
```
