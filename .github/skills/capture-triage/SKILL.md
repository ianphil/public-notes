---
name: capture-triage
description: "Quick capture, inbox listing, and classification of notes into domains, initiatives, and expertise."
---
# Capture & Triage Notes

Quick capture for notes, plus inbox listing and classification.

## Triggers

- `/note {target} {content}`
- `/inbox`
- `/classify {filename} {type} {name}`
- "quick capture", "add a note", "triage inbox", "move inbox note"

## /note {target} {content}

When `/note` is used:

1. Parse the input to identify a potential **target** and **content**.
2. Search for a matching location:
   - `domains/people/{target}/` for people
   - `initiatives/{target}/` for projects
   - `expertise/{target}/` for learning topics
3. If a match is found:
   - Create or update `{target}.md` in that location.
   - If the file is new, add the appropriate template below.
   - Append a new entry with the current date/time and the content.
4. If no match is found and the target seems like a category (person name, project name, topic):
   - Ask: "I don't see {target} yet. Should I create it in domains/people/, initiatives/, or expertise/?"
   - Create the folder and `{target}.md` based on the response.
   - Add the appropriate template and append the new entry.
   - Also create `next-actions.md` using the template below.
5. If no clear target can be inferred:
   - Put the note in `inbox/YYYYMMDD-HHMM-{slug}.md`, where `{slug}` is the first few words of the content, lowercased and hyphenated.
   - Use the Inbox template below (just the content).

## /inbox

When `/inbox` is used:

1. List all files in the `inbox/` folder.
2. For each file, show:
   - Filename
   - First line or title of the note
   - Date modified
3. If the inbox is empty, say "Inbox is empty!"
4. Suggest using `/classify` to move notes to the right place.

## /classify {filename} {type} {name}

When `/classify` is used:

1. Verify the file exists in `inbox/`.
2. Determine the destination based on `{type}`:
   - `person`: `domains/people/{name}/`
   - `domain`: `domains/{name}/`
   - `initiative`: `initiatives/{name}/`
   - `expertise`: `expertise/{name}/`
3. Create the destination folder if it doesn't exist.
4. If the folder was just created, also create `next-actions.md` using the template below.
5. Append the inbox note content into `{name}.md` in the destination (create it with the template if missing).
6. Remove the inbox file after appending.
7. Confirm the move: "Appended {filename} to {destination}/{name}.md".

## Templates

### People (domains/people/)
```
# {Name}

## {Date} {Time}

### Notes

{content}

### Decisions


### Next Steps

```

### Initiatives
```
# {Project}

## {Date} {Time}

### Notes

{content}

### Decisions


### Next Steps

```

### Expertise
```
# {Topic}

## {Date} {Time}

### Notes

{content}

### Resources

```

### Inbox
```
# {Date} {Time}

{content}
```

### Next Actions
```
# Next Actions

## Open


## Done
```
