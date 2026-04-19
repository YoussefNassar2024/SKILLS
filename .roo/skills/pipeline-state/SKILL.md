---
name: pipeline-state
description: ---
name: Pipeline & State Enforcement
description: Manages PIPELINE_STATE.md & CHANGELOG.md synchronization
triggers:
  mode: ["god", "code", "review", "tester", "debug"]
  always: true
---

### PIPELINE & STATE ENFORCEMENT
- Authority files: `PIPELINE_STATE.md` & `CHANGELOG.md` only.
- Pre-Switch Gate: BEFORE any mode switch or step completion → append CHANGELOG → update PIPELINE_STATE → proceed.
- Serial Dispatch: Only ONE agent runs at a time. No parallelism. No concurrent file writes.
- Stub Detection: Empty/<10 lines/boilerplate → REJECT. Mark Failed. Return to Implementer.
- Phase Gate: When phase completes → output EXACTLY: `✅ Phase X complete. Summary: [list]. Proceed to Phase Y? Reply 'yes'.` Then HALT.
- CHANGELOG Rotation: When >500 lines → archive oldest 400 to `CHANGELOG-ARCHIVE.md`, keep 100 + header.
---

# Pipeline State

## Instructions

Add your skill instructions here.
