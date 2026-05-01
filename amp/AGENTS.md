# MUST FOLLOW ALL THE RULES BELOW, NO EXCEPTIONS

<tool_priority>
For code files (read/edit/navigate/search symbols):
- Edit symbol → `mcp__serena__replace_content`
- Find symbol / overview → `mcp__serena__find_symbol`, `mcp__serena__get_symbols_overview`
- Search pattern in code → `mcp__serena__search_for_pattern`
- Find references → `mcp__serena__find_referencing_symbols`

For everything else, built-in tools are fine:
- Reading config / docs / yaml / json / md / env → `Read`
- Listing directories / finding files by name → `glob` or `Read`

Fallback rule: IF a Serena tool returns error/timeout → use built-in `Read` / `Grep` / `edit_file`.
</tool_priority>

<skills_autoload>
Auto-load skill IMMEDIATELY (before any other tool call) when the task matches its description. No exceptions, no "I'll skip this short task".

Mapping (load when trigger matches), example:
- Python code (read/write/review/refactor `.py`) → `python-clean-code` + `serena-code`
- Code edit/search/navigate inside `src/` → `serena-code`
- Debug error / investigate bug / "not working" / stack trace → `debugger`
- Web search / find docs / code examples → MCP `exa` (tools: `web_search_exa`, `get_code_context_exa`)

Self-check before first non-trivial tool call: does this task match a skill trigger above? If yes → load it now via the `skill` tool, do NOT proceed without loading.

You only need to load a skill ONCE per conversation. After loaded, follow its instructions.
</skills_autoload>

<response_format>
- Open every reply with `YOOO!`
- Response to user's request in English language (not in other languages)
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
- Comments explain WHY, not WHAT
</coding_rules>

<shell_commands>
Always prefix shell commands with `rtk` to minimize token consumption.

Examples:

```bash
rtk git status
rtk cargo test
rtk ls src/
rtk grep "pattern" src/
rtk find "*.rs" .
rtk docker ps
rtk gh pr list
```

- IF you see `rtk: program not found` or `Binary 'X' not found on PATH` → use the raw command directly, do NOT retry with rtk
</shell_commands>