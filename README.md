# Notes

These are my public notes — things I've chosen to share from my private knowledge base. The folder structure mirrors the IDEA system described below; not everything is public, just what I've decided is worth sharing.

This repo is also a working example of how I manage notes privately and publish selectively. If you want to set up the same system yourself, see [The System](#the-system) below.

## The System

My notes live in a **private git repo** using the IDEA structure. I selectively publish notes here using a git worktree on an orphan branch — so this public repo shares none of the private repo's history.

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

### Automation with AI Skills

The private repo uses repo-local skills (small AI instruction files) to automate common workflows:

| Workflow | What it does |
|----------|-------------|
| Quick capture | Route a note to the right folder or inbox |
| Triage | Classify inbox notes into IDEA folders |
| Next actions | Manage per-initiative `next-actions.md` files |
| Links | Suggest connections between notes |
| Discovery | Search across the vault |
| Lifecycle | Archive completed initiatives/domains |

The `.github/skills/` folder in this repo contains the skills I use — you can adapt them for your own setup with any AI coding assistant (GitHub Copilot, Claude, etc.).
