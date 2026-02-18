---
name: discovery
description: "Search notes and list recently modified notes across the vault."
---
# Discovery (Search & Recent)

Search across notes or list recently modified notes.

## Triggers

- `/search {query}`
- `/recent`
- `/recent {n}`
- "search notes", "recent notes", "find notes about"

## /search {query}

When `/search` is used:

1. Search for `{query}` across all markdown files in:
   - `domains/`
   - `initiatives/`
   - `expertise/`
   - `inbox/`
   - `Archive/`
2. Show results grouped by location with:
   - File path
   - Matching line(s) with context
3. If no results are found, say: `No notes found matching '{query}'`.

## /recent {n?}

When `/recent` is used:

1. Find all markdown files across:
   - `domains/`
   - `initiatives/`
   - `expertise/`
   - `inbox/`
2. Exclude `Archive/` from results (those are intentionally inactive).
3. Sort by modification time (most recent first).
4. Show the top N results (default 10) with:
   - File path
   - Title (first heading or first line)
   - Last modified date/time
