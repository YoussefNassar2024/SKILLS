---
name: security-compliance
description: ---
name: Security & Compliance Enforcement
description: Enforces input validation, audit integrity, PII handling, and regulatory reporting rules
triggers:
  mode: ["code", "review", "debug"]
  keyword: ["auth", "RBAC", "permission", "audit", "PII", "GDPR", "regulatory", "financial", "capital", "report"]
---

### SECURITY & COMPLIANCE RULES
- **Input Validation**: ALL user inputs must be validated server-side (Zod). Never trust client-side validation alone.
- **SQL Injection Prevention**: Use parameterized queries ONLY via Drizzle ORM. NEVER concatenate user input into SQL strings.
- **Audit Log Integrity**: Audit records must be immutable. Use `INSERT ONLY` pattern. NEVER `UPDATE`/`DELETE` audit_logs.
- **PII Handling**: Fields like `user_email`, `department_head`, `loss_amount` must be encrypted at rest (AES-256) and masked in high-visibility logs.
- **RBAC Enforcement**: Every API endpoint/Server Action must check `req.user.role` AND `req.user.department_scope` before data access.
- **Regulatory Reports**: Capital calculation reports must use exact rounding to 2 decimal places and be signed by the Risk Officer in the audit trail.

---

# Security Compliance

## Instructions

1. **Schema Validation**: For every Server Action in Next.js, define a Zod schema and parse `formData` or input objects immediately.
2. **Audit Trait**: When performing a sensitive operation (e.g., approving a risk), invoke the `createAuditRecord()` helper within the same DB transaction.
3. **Encryption**: Use the project's utility `encryptPII()` before saving fields marked as PII in the database schema.
4. **Access Check**: Use `getAuthSession()` or equivalent and throw an `UnauthorizedError` if the role check fails.
