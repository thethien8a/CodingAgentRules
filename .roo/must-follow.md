---
description: "Rules must follow when coding"
---

# MUST FOLLOW ALL THE RULES BELOW, NO EXCEPTIONS
<using_tool_note>
- Prefer using serena_mcp tool (make sure to `activate_project` first before using any tool of serena).
- Exploration Workflow (Token Save): `codebase_search` -> `get_symbols_overview` -> `find_symbol` -> `find_referencing_symbols`.
- Edit Workflow (Token Save): `find_symbol` (get block) -> `apply_diff` (multi-block search/replace).
- Avoid `read_file` for large files, use another tool instead (if possible)
</using_tool_note>

<response_format>
- Open every reply with `YOOO!`
- Response in English (not Vietnamese)
- Classify intent first:
  - ASK → explain only, no edits
  - EDIT → make changes, then verify
- IF the request is ambiguous → ask ONE clarifying question before acting
</response_format>

<information_quality>
- Search the web before saying "I don't know" — cite source URLs for post-2025 facts
- For problems with multiple valid solutions → list options + trade-offs, then recommend the best fit
- Never fabricate APIs, library behavior, or version numbers — verify first
</information_quality>

<coding_rules>
- No emoji in code
- Comments explain WHY, not WHAT.
</coding_rules>

<shell_commands>

Always prefix shell commands with "C:\Program Files\Git\bin\bash.exe" -c `rtk` to minimize token consumption.

Examples:

```bash
"C:\Program Files\Git\bin\bash.exe" -c "rtk git status"
"C:\Program Files\Git\bin\bash.exe" -c "rtk ls src/"
"C:\Program Files\Git\bin\bash.exe" -c "rtk grep \"pattern\" src/"
"C:\Program Files\Git\bin\bash.exe" -c "rtk find \"*.rs\" ."
"C:\Program Files\Git\bin\bash.exe" -c "rtk docker ps"
```

- IF you see `rtk: program not found` or `Binary 'X' not found on PATH` → use the raw command directly, do NOT retry with rtk
</shell_commands>