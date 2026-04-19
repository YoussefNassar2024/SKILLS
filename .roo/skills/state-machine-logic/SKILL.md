---
name: state-machine-logic
description: ---
name: State Machine & Lifecycle Enforcement
description: Enforces guard conditions, transition rules, and trigger chains for Risk/Loss/Control lifecycles
triggers:
  mode: ["code", "review", "tester"]
  file: ["*.ts", "*.dart"]
  keyword: ["status", "transition", "guard", "trigger", "lifecycle", "Risk", "LossEvent", "ControlTest", "ActionPlan"]
---

### STATE MACHINE RULES
- **Guard Conditions**: Every state transition MUST check pre-conditions (e.g., `canApprove = user.role === 'risk_manager' && risk.status === 'pending_review'`).
- **Immutable History**: Once a state transition occurs, the previous state + timestamp + actor must be logged in `audit_logs` BEFORE the update.
- **Trigger Chains**: If `control_test.status = 'failed'` → MUST trigger: (1) recalc residual risk, (2) create notification, (3) escalate if RAG = 'red'.
- **No Direct Status Writes**: NEVER set `risk.status = 'approved'` directly. Always use the `transitionRisk()` service method that enforces guards + logging.
- **Test Coverage**: Every transition path must have a unit test for SUCCESS and FAILURE (rejected guard).

---

# State Machine Logic

## Instructions

1. **Service Layer**: Wrap all status changes in a dedicated service method (e.g., `updateRiskStatus`).
2. **Audit Call**: Use the `logger.auditStateChange()` helper to ensure consistency.
3. **Transaction**: Guard conditions and state updates must run within a single database transaction.
4. **Validation**: Validate that the NEW state is a valid neighbor of the OLD state according to the state machine diagram.
