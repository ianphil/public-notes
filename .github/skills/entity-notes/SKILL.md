---
name: entity-notes
description: "Create domain, initiative, expertise, and person entities and notes, including shortcuts."
---
# Entity Notes & Shortcuts

Create domains, initiatives, expertise topics, and people notes. Handle shortcut commands for existing entities.

## Triggers

- `/meta-domain {name}`
- `/meta-initiative {name}`
- `/meta-expertise {name}`
- `/meta-person {name}`
- `/domain-{name}`, `/initiative-{name}`, `/expertise-{name}`, `/person-{name}`
- Existing shortcuts:
  - `/initiative-deploy-prod`
  - `/initiative-gabm`
  - `/initiative-kill-eud`
  - `/initiative-vibe-playground`
  - `/person-brooke-philpot`

## /meta-domain | /meta-initiative | /meta-expertise | /meta-person

When a `/meta-*` command is used:

1. Create the target folder:
   - domain → `domains/{name}/`
   - initiative → `initiatives/{name}/`
   - expertise → `expertise/{name}/`
   - person → `domains/people/{name}/`
2. Create or update `{name}.md` in that folder.
3. If the file is new, add the appropriate template below.
4. Ask what to note about {Name} and append a new entry with the current date/time and the response in **Notes**.
5. Create `next-actions.md` using the template below if it doesn't already exist.
6. Confirm the update and suggest future usage:
   - `/note {name} {content}`
   - or `/domain-{name}`, `/initiative-{name}`, `/expertise-{name}`, `/person-{name}` to open a fresh note.

## Shortcut commands (/domain-{name}, /initiative-{name}, /expertise-{name}, /person-{name})

When a shortcut command is used:

1. Create the target folder if it doesn't exist (same paths as above).
2. Create or update `{name}.md` with the appropriate template if missing.
3. Ask what to note and append a new entry with the current date/time in **Notes**.
4. Create `next-actions.md` if missing.
5. Confirm the note was updated.

## Templates

### Domain / Initiative / Person
```
# {Name}

## {Date} {Time}

### Notes


### Decisions


### Next Steps

```

### Expertise
```
# {Name}

## {Date} {Time}

### Notes


### Resources

```

### Next Actions
```
# Next Actions

## Open


## Done
```
