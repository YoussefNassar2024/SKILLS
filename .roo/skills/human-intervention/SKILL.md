---
name: human-intervention
description: ---
name: Human Intervention & Error Recovery
description: Handles stop/cancel/wait, crash recovery, and state reconciliation
triggers:
  mode: ["*"]
  keyword: ["stop", "cancel", "wait", "halt", "pause", "resume"]
---

### HUMAN INTERVENTION & RECOVERY
- If user says `stop/cancel/wait/interrupt` → HALT immediately. Do not complete current action.
- Write partial CHANGELOG entry: `Status: Interrupted by human. Note: [what was completed]`.
- Update `PIPELINE_STATE.md`: `step_status = interrupted`. WAIT until user says `resume`.
- Crash Recovery: If `step_status = implementing/reviewing/testing` without completion → read last CHANGELOG, verify syntax (`npx tsc --noEmit`), invalid → `git restore` → mark failed.
- State Reconciliation: If `PIPELINE_STATE.md` vs `CHANGELOG.md` inconsistent → trust `CHANGELOG` (append-only), fix `PIPELINE_STATE.md`.

---

# Human Intervention

## Instructions

1. **State Snapshot**: Before halting, save the current file state to a temporary branch or `.roo/temp/` if significant work was done.
2. **Reasoning**: Always ask the user *why* they interrupted if it wasn't a manual "stop" (e.g., if a tool failed repeatedly).
3. **Resumption**: When resuming, re-verify the environment state (files, database, dependencies) to ensure no manual changes were made during the pause.
4. **Transparency**: Always notify the user of exactly which files were restored during a crash recovery.
