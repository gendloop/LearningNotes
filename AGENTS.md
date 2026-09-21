# AGENTS.md

## What This Repo Is

GitBook-based personal learning notes (Chinese, zh-hans). Documentation-only — no application code, no test suite, no lint/typecheck commands.

## Build & Preview

```bash
npm run build   # builds to _book/
npm run serve   # preview at localhost:4000
```

Requires Node.js and `gitbook-cli` (pinned to 3.2.3 in scripts).

## Adding New Pages

When adding or removing docs, update **all three**:
1. `SUMMARY.md` — GitBook's table of contents (pages not listed won't appear in the built book)
2. Root `README.md` — top-level index
3. Parent category `README.md` (e.g. `docs/tools/README.md` when adding a tool)

## Content Conventions

- All content is written in **Chinese** (zh-hans).
- New pages go under `docs/<category>/<topic>/` with a `README.md` as the topic index.
- Per `.editorconfig`: 2-space indent, UTF-8, CRLF, trim trailing whitespace.
- Per `.markdownlint.json`: line length (MD013), inline HTML (MD033), and first-line heading (MD041) rules are disabled.
- GitBook language is set to `zh-hans` in `book.json`.
