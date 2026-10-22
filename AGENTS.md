# AGENTS.md

Gui's personal design system. Read `PRINCIPLES.md` before designing or building UI anywhere that uses it.

- Source of truth: `tokens/tokens.json` (W3C DTCG). Figma and the Claude Design artifact are downstream copies.
- Components read `mapped.*` and `responsive.*` only. Never raw hex or `brand.*`.
- Any new text or surface color must be contrast-checked (AA 4.5:1) in dark and light before it is added.
- Commit every change with a message describing what changed.
