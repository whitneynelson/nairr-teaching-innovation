---
title: Git Basics and Cheat Sheet
---

# Git Basics & Cheat Sheet

<div class="card">

Git tracks changes for a whole folder of files instead of one document; it saves snapshots of your work over time, and GitHub is the website that stores those snapshots online so you (and Claude) can access them from anywhere.

</div>

## The five commands you'll actually use this week

| Command | What it does |
|---|---|
| `git clone <url>` | Download a copy of a repo onto your computer. You'll run this once per repo, on Day 1. |
| `git status` | "What's changed since my last save?"; run this anytime you're unsure what state your files are in. |
| `git add <file>` (or `git add -A` for everything) | Mark changed files as "ready to save." |
| `git commit -m "message"` | Take the actual snapshot, with a short note describing what changed. |
| `git push` | Upload your snapshots to GitHub, so they're backed up and visible online. |

## A typical work session

```bash
# see what changed
git status

# stage everything you changed
git add -A

# save a snapshot with a description
git commit -m "Draft learning outcomes"

# upload it to GitHub
git push
```

You'll do a version of this loop every time you finish a chunk of work this week; draft something, commit it, push it.

## If something goes wrong

- **"Password authentication is not supported"**; GitHub needs a Personal Access Token instead of your password. See the troubleshooting section in [Module 00–01](../modules/module-00-01.html).
- **Merge conflicts**; unlikely this week since you're mostly working solo in your own repo, but if you see one, stop and ask rather than force-pushing over it; Claude Code can also help you read and resolve a conflict if you paste it in and ask.
- **Not sure what state you're in**; `git status` is always safe to run and never changes anything. When in doubt, run it first.

Next: back to [Setup](setup-git-vscode-tacc.html), or return to the [Pre-Event](../pre-event.html) checklist.
