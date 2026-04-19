---
name: i18n-rtl
description: ---
name: Internationalization & RTL Layout Enforcement
description: Enforces Arabic/English toggle, RTL layout flipping, translated labels, and Arabic PDF generation
triggers:
  mode: ["code", "review"]
  file: ["*.tsx", "*.dart", "*.ts"]
  keyword: ["i18n", "translation", "Arabic", "RTL", "locale", "dir=", "lang=", "Cairo", "PDF", "logical properties"]
---

### I18N & RTL RULES
- **Locale Switching**: 
  - **Next.js**: Use `next-intl`. Store preference in cookie/middleware.
  - **Flutter**: Use `easy_localization`. Store in shared_preferences.
- **RTL Layout**: Apply `dir="rtl"` to root. Use CSS logical properties: `margin-inline-start` instead of `margin-left`.
- **Translated Lookups**: Dropdown values from `system_lookups` must be fetched with `?lang=...` or using the localized DB field.
- **Arabic PDFs**: Use Cairo fonts (NotoSansArabic). Embed fonts to avoid rendering issues.
- **Bidirectional Text**: Use `<bdi>` or `unicode-bidi: isolate` for mixed Arabic/English content (e.g., risk titles with ID codes).

---

# I18n Rtl

## Instructions

1. **Logical Styling**: Never use `left` or `right` in CSS. Always use `start` and `end`.
2. **Icon Flipping**: Flip directional icons (arrows) in RTL unless they are "progress" indicators that are culturally agnostic.
3. **Lazy Loading**: Lazy load translation bundles per page to keep initial hydration fast.
4. **Number Formatting**: Use `Intl.NumberFormat` with the appropriate locale to ensure digits are displayed correctly (e.g., Hindi vs Arabic-Indic digits).
