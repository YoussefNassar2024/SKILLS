---
name: financial-calculation
description: ---
name: Financial Calculation & Risk Formula Enforcement
description: Ensures mathematical correctness for residual risk, clamping, capital calculations, and rounding rules
triggers:
  mode: ["code", "review", "tester"]
  keyword: ["residual", "inherent", "clamping", "capital", "calculation", "formula", "round", "decimal", "percentage"]
---

### FINANCIAL CALCULATION RULES
- **Residual Formula**: `residual = inherent - (avg_reduction * inherent)`. `avg_reduction` = weighted average of control effectiveness (effective=0.70, partially=0.40, ineffective=0.00).
- **Clamping Guarantee**: Result MUST be clamped: `Math.max(1, Math.min(inherent, residual))` per component (likelihood/impact/score).
- **Rounding**: All financial values rounded to 2 decimals using `toFixed(2)` + `parseFloat()` to avoid string artifacts and floating point drift.
- **Edge Cases**: Handle `inherent = 0`, `no controls assigned`, `null effectiveness` → default to `residual = inherent`.
- **Test Mandate**: Every calculation function must have tests for: (1) normal range, (2) edge cases (0/null), and (3) precision verification.

---

# Financial Calculation

## Instructions

1. **Precision Utility**: Use the internal `roundFinancial()` utility instead of raw `Math.round`.
2. **Formula Audit**: When updating a formula, verify against the `CRMS_Project_Breakdown.md` specifications.
3. **Unit Tests**: Add a test file in `__tests__/calculations/` for any new logic involving capital or risk scores.
4. **Data Types**: Use `Decimal` types for intermediary calculations when handling currency to prevent loss of precision.
