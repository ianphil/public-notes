# Copilot Instructions

## Repository Overview

This directory (`C:\src\public-notes`) is a **git worktree** of the private repo at `C:\src\miss-moneypenny`, checked out on the orphan branch `public-branch`. It has no shared history with the private repo's `master` branch.

The remote `public` points to `git@github.com:ianphil/public-notes.git` (a public GitHub repo).

## Purpose

Selectively publish individual notes from the private repo without exposing its history or unpublished content.

## Workflow

- **Add a file from the private repo:**
  ```sh
  git checkout master -- path/to/file.md
  ```
  Run this from within the `C:\src\public-notes` worktree.

- **Commit and push to the public repo:**
  ```sh
  git push public public-branch:main
  ```

## Committing

Always commit manually using the git CLI. **Never use `skill(commit)` or invoke the commit skill.**

```sh
git add -A
git commit -m "Your message here"
git push public public-branch:main
```

**Never** include a `Co-authored-by` trailer or any attribution to Copilot in commit messages.

## Rules

- **Never** push `master` to the `public` remote.
- Only push `public-branch` to the `public` remote.
- Files here are hand-picked from the private repo — do not bulk-copy or expose unreviewed content.
- **Never** use `skill(commit)` — commit manually with the git CLI as shown above.
