# Public Notes

Selectively shared notes from [Miss Moneypenny](https://github.com/ianphil/miss-moneypenny) — an AI chief of staff built on GitHub Copilot. The private repo contains the full system; this repo shares the parts worth sharing.

## What's Here

| File | About |
|------|-------|
| [`expertise/building-a-chief-of-staff.md`](expertise/building-a-chief-of-staff.md) | Walkthrough: building a persistent, personable AI assistant with identity, memory, retrieval, and session continuity |
| [`expertise/IDEA-notes-setup.md`](expertise/IDEA-notes-setup.md) | Tutorial: setting up IDEA-structured notes with git |
| [`expertise/git-orphan-branch-public-publishing.md`](expertise/git-orphan-branch-public-publishing.md) | How to selectively publish from a private repo using orphan branches |

## The System

These notes live in a **private git repo** using the IDEA structure. I selectively publish notes here using a git worktree on an orphan branch — so this public repo shares none of the private repo's history.

### IDEA Structure

| Folder | Purpose |
|--------|---------|
| **I**nitiatives | Projects with a defined end goal |
| **D**omains | Recurring areas of responsibility |
| **E**xpertise | Notes on things I learn |
| **A**rchive | Completed or inactive items |
| Inbox | Quick capture, triaged later |

Not all folders will be present here — only what I've chosen to share publicly.

### Publishing Workflow

Notes move from private → public by cherry-picking individual files:

```sh
# From within the public worktree
git checkout master -- expertise/some-note.md
git commit -m "Publish note on X"
git push public public-branch:main
```

See [`expertise/git-orphan-branch-public-publishing.md`](expertise/git-orphan-branch-public-publishing.md) for the full setup guide.
