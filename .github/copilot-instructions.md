# Copilot Instructions

## Repository Overview

This directory (`C:\src\public-notes`) is a **git worktree** of the private repo at `C:\src\notes`, checked out on the orphan branch `public-branch`. It has no shared history with the private repo's `main` branch.

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

## Rules

- **Never** push `master` to the `public` remote.
- Only push `public-branch` to the `public` remote.
- Files here are hand-picked from the private repo — do not bulk-copy or expose unreviewed content.
