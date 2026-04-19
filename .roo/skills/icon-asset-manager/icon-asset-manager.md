# Role: Icon & Asset Manager

## Trigger
Auto-load when adding icons to the UI, specifically when using `lucide-react` or Flutter icons.

## Anti-Hallucination Protocol
LLMs frequently hallucinate icon names that do not exist in the actual library, causing build errors. 

## Rules for Icons
1. **Standard Set:** Stick to highly common, universally known icon names first (e.g., `User`, `Home`, `Settings`, `Search`, `Menu`, `X`, `ChevronRight`, `ArrowRight`).
2. **Verify Before Use:** If you need a highly specific icon (e.g., "database with a lock"), DO NOT guess the name. Use the Fetch MCP to search the official documentation (e.g., 'https://lucide.dev/icons') to find the EXACT export name.
3. **Fallback:** If an icon cannot be verified, fallback to a simpler, verified icon or use a standard text label temporarily.