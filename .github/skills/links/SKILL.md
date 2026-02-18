---
name: links
description: "Wiki link management and vault index generation. Suggest links for notes, add them, and maintain vault-index.md."
---
# Links & Vault Index

Manage wiki links across the vault and maintain a searchable index of all notes.

## Triggers

- `/links` — suggest wiki links for a specific note
- `/links {filepath}` — suggest wiki links for the given note
- `/vault-index` — regenerate `vault-index.md` at the repo root
- "suggest links", "update vault index", "find connections"

## /links {filepath?}

When `/links` is used:

1. Determine the target note:
   - If `{filepath}` is provided, use that note.
   - If not, ask: "Which note should I find links for?"
2. Read the target note content.
3. Read `vault-index.md` from the repo root to get a catalog of all notes and their summaries.
   - If `vault-index.md` doesn't exist, tell the user to run `/vault-index` first.
4. For each entry in the vault index (excluding the target note itself):
   - Check if the note's title, filename, or key concepts appear in the target note's content.
   - Check if the target note's content discusses topics that relate to the indexed note's summary.
5. Present suggestions grouped by confidence:
   - **Strong matches**: The note's title or a key phrase appears verbatim in the target text — show the exact sentence and how the link would read.
   - **Likely related**: Overlapping concepts or topics — explain the connection briefly.
6. Ask which links to add. For each accepted link:
   - Weave the `[[link]]` into an existing sentence naturally. Links should be part of the reasoning, not footnotes.
   - If no natural insertion point exists, append a short connecting sentence.
7. After adding links, confirm what was changed.

### Link Style Rules

- **Weave, don't footnote.** `"because [[quality is the hard part]] we need to focus on curation"` not `"See also: quality-is-the-hard-part"`.
- **Link text = note title.** Use `[[Note Title]]` matching the filename without extension, spaces instead of hyphens, title case.
- **Don't over-link.** Only link on first mention per note. 2-5 links per note is healthy; 10+ is noise.
- **Cross-folder links are the point.** The most valuable links connect initiatives ↔ expertise ↔ domains.

## /vault-index

When `/vault-index` is used:

1. Scan all markdown files in:
   - `domains/` (recursive)
   - `initiatives/` (recursive)
   - `expertise/` (recursive)
   - `inbox/`
   - `Archive/` (recursive)
2. Skip non-note files:
   - `next-actions.md` files
   - Files in `.obsidian/`, `.copilot/`, `.ainotes/`
   - Image files and non-markdown files
3. For each note, read it and produce:
   - **Path**: relative path from repo root
   - **Title**: first `#` heading, or filename if no heading
   - **Summary**: one sentence describing the note's content (max ~15 words)
   - **Key concepts**: 2-5 key topics, people, or tools mentioned
4. Write the index to `vault-index.md` at the repo root in this format:

```markdown
# Vault Index

Generated: {YYYY-MM-DD}

## Domains

| Note | Summary | Key Concepts |
|------|---------|--------------|
| [[Note Title]] (`path`) | One sentence summary | concept, concept |

## Initiatives

| Note | Summary | Key Concepts |
|------|---------|--------------|
| [[Note Title]] (`path`) | One sentence summary | concept, concept |

## Expertise

| Note | Summary | Key Concepts |
|------|---------|--------------|
| [[Note Title]] (`path`) | One sentence summary | concept, concept |

## Inbox

| Note | Summary | Key Concepts |
|------|---------|--------------|
| [[Note Title]] (`path`) | One sentence summary | concept, concept |

## Archive

| Note | Summary | Key Concepts |
|------|---------|--------------|
| [[Note Title]] (`path`) | One sentence summary | concept, concept |
```

5. Confirm completion with a count: "Indexed {N} notes across {M} folders."

### Index Guidelines

- Summaries should be **opinionated and specific**, not generic. "Autonomous bash loop for running Claude Code unattended" not "A pattern for AI agents."
- Key concepts should be **linkable** — they're the terms `/links` will match against.
- Archive notes get indexed but are marked as archived context, not active work.
- The index is the vault's table of contents for both the agent and Obsidian.
