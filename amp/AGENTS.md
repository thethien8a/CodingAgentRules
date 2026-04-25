# Global Rules

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

<serena_setup>
Trigger: ANY task that involves reading/searching/editing files 

Steps (in order, no skipping):
1. Call `mcp__serena__check_onboarding_performed`
2. If not done → call `mcp__serena__onboarding`
3. Then use serena tools for all subsequent code operations

Skip ONLY for: pure conceptual questions, reading single config/doc file (yaml/json/md/env), or web research tasks.

Self-check before answering ANY "what does X do in this project" question: did I use `mcp__serena__search_for_pattern` or `find_symbol`? If no → I violated the rule.
</serena_setup>

<skills_autoload>
Auto-load skill IMMEDIATELY (before any other tool call) when the task matches its description. No exceptions, no "I'll skip this short task".

Mapping (load when trigger matches), example:
- Python code (read/write/review/refactor `.py`) → `python-clean-code` + `serena-code`
- Code edit/search/navigate inside `src/` → `serena-code`
- Debug error / investigate bug / "not working" / stack trace → `debugger`
- Web search / find docs / code examples → `exa-search`

Self-check before first non-trivial tool call: does this task match a skill trigger above? If yes → load it now via the `skill` tool, do NOT proceed without loading.

You only need to load a skill ONCE per conversation. After loaded, follow its instructions.
</skills_autoload>

<response_format>
- Open every reply with `YOOO!`
- Mirror user's language (Vietnamese ↔ English)
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
- Prefer prefixing with `rtk` for token optimization (e.g. `rtk git status`)
- IF you see `rtk: program not found` or `Binary 'X' not found on PATH` → use the raw command directly, do NOT retry with rtk
</shell_commands>