---
name: web-browsing
description: ---
name: Web Browsing Protocol
description: Safe, rate-limited dependency & documentation lookup rules
triggers:
  mode: ["code", "review", "debug", "chat"]
  keyword: ["install", "version", "latest", "docs", "npm", "package", "deprecation", "CVE", "security advisory"]
---

### WEB BROWSING PROTOCOL
- Max 3 web requests/turn. Use `curl`, `wget`, `npm view <pkg>`.
- Verify versions/deprecations before install. Prefer `npm view <pkg> version`.
- Log sources in CHANGELOG: `Sourced from: <URL> @ <date>`.
- Prefer official docs URLs (`drizzle.team`, `nextjs.org`, `flutter.dev`, `nodejs.org`). Verify with 2+ sources when possible.
- Fallback to cached knowledge if web fails. Never trust unverified StackOverflow snippets.
- Rate limit enforced to avoid IP throttling.
---

# Web Browsing

## Instructions

Add your skill instructions here.
