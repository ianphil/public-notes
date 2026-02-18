# Notes

Personal knowledge management using the IDEA method.

## Structure

| Folder | Purpose |
|--------|---------|
| **I**nitiatives | Projects with a defined end goal |
| **D**omains | Recurring areas of responsibility I manage |
| **E**xpertise | Notes about things I learn |
| **A**rchive | Completed or inactive items |
| Inbox | Quick capture for notes to classify later |

## Skills

Repo-local skills live in `.copilot/skills` and are designed to be context-aware for this vault.

**Meta skills** - Create folders and note templates for tracking:
- `skill(meta-person) {name}` → creates `skill(person-{name})`
- `skill(meta-domain) {name}` → creates `skill(domain-{name})`
- `skill(meta-initiative) {name}` → creates `skill(initiative-{name})`
- `skill(meta-expertise) {name}` → creates `skill(expertise-{name})`

**Quick capture:**
- `skill(note) {target} {content}` → auto-routes to matching folder or inbox

**Triage:**
- `skill(inbox)` → list inbox contents
- `skill(classify) {file} {type} {name}` → move inbox note to right place

**Next actions:**
- `skill(next-action) list inbox` → show untriaged actions
- `skill(next-action) add initiative my-project Draft release notes` → add an action
- `skill(next-action) done domain finances 2` → mark action #2 done
- `skill(next-action) move 3 expertise rust` → move inbox action to a list

**Links & Index:**
- `skill(links)` → suggest wiki links for a note
- `skill(links) {filepath}` → suggest links for specific note
- `skill(vault-index)` → regenerate `vault-index.md` at the root

**Discovery:**
- `skill(search) {query}` → search all notes
- `skill(recent)` → show recently modified notes

**Lifecycle:**
- `skill(archive) {type} {name}` → move folder to Archive
- `skill(ship)` → stage, commit, push
