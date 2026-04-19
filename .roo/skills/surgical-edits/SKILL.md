---
name: surgical-edits
description: ---
name: Surgical Edits & Diff Mandate
description: Enforces strict replacement rules to prevent file corruption
triggers:
  mode: ["code", "review", "debug", "tester", "god"]
  always: true
---

### SURGICAL EDITS — NON-NEGOTIABLE

- Existing file → `replace_file_content` (change ONLY exact modified blocks).
- Multiple changes → `multi_replace_file_content`.
- New file → `write_to_file`.
- NEVER use `write_to_file` on existing files to overwrite them unless explicitly replacing the entire content is safer (for small files < 100 lines).
- If `replace_file_content` fails on string mismatch: `view_file` to get exact content (including whitespace), retry with exact matching blocks.
- All paths: Must be absolute or relative as per the tool environment.
- NEVER include unchanged lines in your `TargetContent`. ONLY the precisely identified block being changed.

---

# Surgical Edits

## Instructions

1. **Precision First**: Before editing, use `view_file` to capture the exact context and line numbers.
2. **Atomic Changes**: Prefer `multi_replace_file_content` when making multiple related changes across a file to maintain atomic integrity.
3. **Validation**: Immediately after a replace operation, use `view_file` or a linting command to ensure the file is syntactically correct.
4. **Failure Recovery**: if a replacement fails, DO NOT guess the content. Read the file again.
