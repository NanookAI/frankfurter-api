# Agent Instructions

This repository contains an Agent Skill that teaches AI agents how to use the
Frankfurter exchange rate API (https://frankfurter.dev/). The deliverable is
documentation, not application code.

## Layout

- `skills/frankfurter-api/SKILL.md` — skill entry point (frontmatter + quick reference)
- `skills/frankfurter-api/references/endpoints.md` — full v2 endpoint reference
- `skills/frankfurter-api/references/v1-api.md` — legacy v1 API notes

## Conventions

- **English only in all files.** No Chinese or other non-English text in any
  committed file, including examples and comments.
- **Verify before documenting.** Every request/response example must be checked
  against the live API (`curl https://api.frankfurter.dev/v2/...`) before it goes
  into the docs. Do not copy response shapes from memory — the API evolves.
- **v2 is the primary API.** New content goes in `SKILL.md` / `endpoints.md`.
  `v1-api.md` exists only for people maintaining legacy code; keep it minimal.
- **Keep SKILL.md lean** (well under 500 lines). Detailed material belongs in
  `references/`, with a clear pointer from SKILL.md telling the reader when to
  open it.
- **Explain the why.** When documenting a pitfall or rule, state the reason
  (e.g. "Cloudflare returns 403 for the default Python-urllib User-Agent") so
  agents can generalize instead of pattern-matching.

## Known live-API facts worth preserving

These were discovered by testing and are not in the official docs:

- The public API returns **403** for the default `Python-urllib` User-Agent
  (Cloudflare). `curl`, `fetch`, and `python-requests` work; a custom
  `User-Agent` fixes `urllib`.
- Weekends/holidays have no new data; the returned `date` field is authoritative.
- Error bodies look like `{"status": 404, "message": "not found"}`.

## Validation checklist before committing

1. `grep -rnP '[\x{4e00}-\x{9fff}]' . --exclude-dir=.git` returns nothing (no CJK text).
2. Any changed example URL was re-run against the live API.
3. SKILL.md frontmatter still has valid `name` and `description` fields, and the
   description stays short (~1-2 sentences) while keeping trigger keywords:
   exchange rate, currency conversion, forex, historical FX.
