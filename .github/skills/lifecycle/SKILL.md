---
name: lifecycle
description: "Archive entities. Use when the user says 'archive', 'move to archive', 'archive initiative', 'archive domain', 'archive person', or wants to move items to Archive."
---
# Lifecycle (Archive)

Archive entities to the Archive folder.

## Triggers

- `/archive {type} {name}`
- "archive this"

## /archive {type} {name}

Move a domain, initiative, or person to the Archive folder.

Where:
- `{type}` is one of: `person`, `domain`, `initiative`
- `{name}` is the name used when creating it (lowercase, hyphens)

Steps:

1. Identify the source folder based on type:
   - `person`: `domains/people/{name}/`
   - `domain`: `domains/{name}/`
   - `initiative`: `initiatives/{name}/`
2. Move the folder to `Archive/{type}/{name}/`.
3. Confirm what was archived.
