---
name: tool-grammar
description: ---
name: Tool Usage & Parameters Grammar
description: Enforces correct parameter structure for JSON tool calls
triggers:
  mode: ["*"]
  always: true
---

### TOOL GRAMMAR — MANDATORY
- **JSON Structure**: Every tool call is a JSON object with strictly typed parameters.
- **Path Awareness**: Always use the full absolute path or correctly resolved workspace path.
- **Parameter Completeness**: Include all required fields (e.g., `StartLine`, `EndLine`, `TargetContent` for replacements).
- **Error Recovery**: On "invalid arguments" error: re-read the tool definition immediately and re-issue with correct types. Do not apologize.
- **Conflict Resolution**: If the Implementation Plan contradicts the current state of the source code, THE SOURCE CODE IS GROUND TRUTH. Update the plan first before proceeding if the deviation is significant.

---

# Tool Grammar

## Instructions

1. **Verify Tool Schema**: Before calling a tool you haven't used recently, verify its parameter requirements in your system prompt.
2. **Double Check Lines**: When using line-based tools (`view_file`, `replace_file_content`), double-check that the line numbers match the actual file content to avoid "out of range" or "mismatch" errors.
3. **Escaping**: Ensure special characters in strings are correctly escaped for JSON.
