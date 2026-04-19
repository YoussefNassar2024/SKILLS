# Theme Vault Catalog

Always pick a Persona from this list (or derive a highly specific variation) before starting a project.

## 1. SaaS Modern (Apple / Stripe Inspired)
*   **Vibe:** Professional, incredibly clean, high trust, spacious.
*   **Background (Light):** `oklch(0.99 0.01 260)` (Very slightly cool off-white)
*   **Surface:** `oklch(1 0 0)` (Pure white) with delicate shadow: `shadow-[0_2px_10px_rgb(0,0,0,0.03)]`
*   **Primary Action Color:** `oklch(0.5 0.2 260)` (Vibrant Blurple)
*   **Text (Primary):** `oklch(0.2 0.05 260)` (Deep slate, never pure black)
*   **Typography:** Inter or SF Pro Display.
*   **Border Radius:** `rounded-xl` (12px) or `rounded-2xl` (16px).
*   **Micro-Interaction:** Very subtle scale `hover:scale-[1.01]` and opacity changes `hover:opacity-80`.

## 2. Cyberpunk 2077
*   **Vibe:** Aggressive, tech-heavy, neon, dark mode exclusively.
*   **Background:** `oklch(0.15 0.05 270)` (Deep charcoal)
*   **Surface:** `oklch(0.2 0.05 270)`
*   **Primary Action Color:** `oklch(0.8 0.25 100)` (Neon Yellow/Cyber Yellow)
*   **Secondary Action:** `oklch(0.6 0.2 300)` (Neon Magenta/Fuchsia)
*   **Typography:** Orbitron, Rajdhani, or Roboto Mono.
*   **Border Radius:** `rounded-none` (0px). Sharp edges.
*   **Effects:** Heavy use of `glitch` effects on hover, `shadow-[4px_4px_0_theme(colors.yellow.400)]` for buttons.

## 3. Neo-Brutalism
*   **Vibe:** Quirky, bold, high-contrast, trendy (Gumroad/Figma inspired).
*   **Background:** `oklch(0.95 0.05 100)` (Warm cream or distinct pastel like mint green).
*   **Surface:** `oklch(1 0 0)` (White).
*   **Primary Action Color:** `oklch(0.5 0.2 20)` (Vivid Orange) or `oklch(0.5 0.2 200)` (Vivid Blue).
*   **Text (Primary):** `oklch(0 0 0)` (Pure Black).
*   **Typography:** Space Grotesk, Manrope, or Helvetica Now.
*   **Border Radius:** `rounded-none` to `rounded-sm` with **thick borders**.
*   **Effects:** `border-4 border-black`, hard shadows: `shadow-[4px_4px_0_black]` expanding to `[6px_6px]` on hover.

## 4. Glassmorphic Aurora
*   **Vibe:** Immersive, dreamy, 3D, premium macOS-style depth.
*   **Background:** Needs a colorful mesh gradient or blurred aesthetic image under everything. `bg-gradient-to-br from-indigo-500 via-purple-500 to-pink-500`.
*   **Surface (Cards):** `bg-white/10` or `bg-black/20`.
*   **Backdrop Filter:** `backdrop-blur-xl` or `backdrop-blur-2xl`.
*   **Border:** `border border-white/20` (subtle highlight edge).
*   **Typography:** SF Pro, Outfit, or Poppins. White text with text-shadow.
*   **Border Radius:** `rounded-3xl` (24px) for organic, smooth shapes.
*   **Micro-Interaction:** Glow effects `hover:shadow-glow` using `framer-motion`.

## 5. Web3 / Dark Fintech
*   **Vibe:** Money, futuristic, secure, exclusive.
*   **Background:** `oklch(0.1 0 0)` (Almost pure black `#0A0A0A`).
*   **Surface (Cards):** `oklch(0.15 0 0)` (Very dark gray `#111111`) with subtle linear gradient overlay `bg-gradient-to-b from-white/5 to-transparent`.
*   **Primary Action Color:** `oklch(0.7 0.2 160)` (Vibrant Emerald/Matrix Green).
*   **Text:** `oklch(0.9 0 0)` for headers, `oklch(0.6 0 0)` for muted text.
*   **Border:** Very thin `border-white/10`.
*   **Typography:** Inter or Clash Display.

## 6. Nordic Clean / Editorial
*   **Vibe:** Sophisticated, typography-first, minimalist, fashion/magazine.
*   **Background:** `oklch(0.98 0.02 50)` (Oatmeal / warm stone).
*   **Surface:** Transparent or matching background. Use margins to separate content, not boxes.
*   **Primary Action Color:** `oklch(0.3 0 0)` (Dark gray, almost black).
*   **Typography:** Playfair Display (Serif) for massive headings, Lora (Serif) or Inter (Sans) for body.
*   **Layout:** Extreme whitespace. `py-24`, massive gaps `gap-16`. Asymmetrical grids.

*(More to be derived dynamically based on these golden archetypes if requested)*
