---
name: nextjs-framework
description: ---
name: Next.js Framework & App Router Guidelines
description: Enforces Next.js 16 (App Router) architectural standards and Best Practices
triggers:
  mode: ["code", "review", "debug"]
  file: ["app/**", "pages/**", "next.config.*", "middleware.ts"]
  keyword: ["Server Component", "Client Component", "server-only", "use client", "generateStaticParams", "revalidate"]
---

### NEXT.JS FRAMEWORK GUIDELINES
- **App Router First**: Prefer `app/` directory over `pages/`. Use Server Components by default.
- **Data Fetching**: Use `fetch()` in Server Components with appropriate `next: { revalidate: ... }` tags.
- **Server Actions**: All mutations must use Server Actions (`'use server'`) with Zod validation.
- **Client Components**: Keep leaf-level. Use `'use client'` ONLY when using hooks (useState, useEffect) or event listeners.
- **Styles**: Use Tailwind 4 CSS variables and logical properties.
- **Performance**: Export `unstable_instant` from routes when fixing slow navigations (refer to docs).

---

# Next.js Framework

## Instructions

1. **Before any code change** in `app/` or `components/`, read the relevant guide in `.roo/skills/nextjs-framework/docs/`.
2. Ensure you are using the correct router pattern (App Router vs Pages Router).
3. Verify that Server/Client component boundaries are optimized.
4. If modifying navigation or suspense, refer to `docs/01-app/02-guides/instant-navigation.mdx`.
