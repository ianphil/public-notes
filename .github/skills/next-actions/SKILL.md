---
name: next-actions
description: "Manage next-action lists for initiatives, domains, expertise, people, and inbox."
---
# Next Actions

Manage next-action lists for initiatives, domains, expertise, people, and inbox.

## Triggers

- `/next-action`
- `/next-actions`
- "add next action", "list next actions", "mark next action done"

## Usage

```
/next-action {subcommand} {scope} {name?} {args...}
```

### Subcommands

#### list

```
/next-action list {scope} {name?}
```

Show open actions with line numbers. Scopes: `initiative`, `domain`, `expertise`, `person`, `inbox` (no name needed for inbox).
If the `next-actions.md` file doesn't exist, create it with the template below and report "No actions yet."

#### add

```
/next-action add {scope} {name?} {action}
```

Append `- [ ] {action}` to the **Open** section of the target `next-actions.md`. Create the file (and folder) if missing.

#### done

```
/next-action done {scope} {name?} {index}
```

Mark the open action at `{index}` (from `list` output) as done: change `- [ ]` to `- [x]` and move it to the **Done** section.

#### move

```
/next-action move {index} {scope} {name}
```

Move the open action at `{index}` from `inbox/next-actions.md` to the target list. Remove it from inbox and append it to the target's **Open** section. Create the destination folder and file if they don't exist.

## File locations

| Scope | Path |
|-------|------|
| initiative | `initiatives/{name}/next-actions.md` |
| domain | `domains/{name}/next-actions.md` |
| expertise | `expertise/{name}/next-actions.md` |
| person | `domains/people/{name}/next-actions.md` |
| inbox | `inbox/next-actions.md` |

## Template

When creating a new `next-actions.md`, use:

```markdown
# Next Actions

## Open


## Done
```
