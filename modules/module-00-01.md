---
title: "Module 00-01: Set Up Your Repos & Environment"
---

# Module 00–01: Set Up Your Repos & Environment

*Feeds: Day 1, 10:30 AM – 12:30 PM*

<div class="card">

**In plain terms:** this module is just installing software and creating two folders (repos) that will hold your course. Nothing here requires coding experience.

</div>

## What you'll need before starting

<ul class="checklist">
<li>A GitHub account</li>
<li>Git installed (<code>git --version</code> works in your terminal)</li>
<li>VS Code or Antigravity installed</li>
<li>TACC account + MFA set up</li>
</ul>

Missing any of these? See [Setup: Git, VS Code, TACC](../resources/setup-git-vscode-tacc.html) first.

## Step 1: Create your two repos from the template

You're not starting from a blank repo — you're using a pre-built template.

1. Go to the template repos (your facilitator has the link): `course-site` and `course-toolkit`
2. On each, click the green **"Use this template"** button → **"Create a new repository"**
3. Name it whatever you'll actually use going forward (e.g. `intro-to-ml-course-site`)
4. Set visibility: `course-site` → **Public**, `course-toolkit` → **Private**
5. Click **Create repository**

You now have your own copy of both, no shared history tying back to the template.

## Step 2: Clone both repos locally

```bash
git clone https://github.com/YOUR-USERNAME/your-course-site.git
git clone https://github.com/YOUR-USERNAME/your-course-toolkit.git
```

<div class="card">

**In plain terms:** "cloning" just means downloading a working copy onto your own computer. Open both folders side by side in your editor.

</div>

## Step 3: Walk the environment

- **course-site** = everything a student will eventually see. Nothing goes here until it's ready to be public.
- **course-toolkit** = grading, exams, attendance, your real prep notes. Never gets published.
- **builder-guide/** (inside course-site) = this walkthrough itself, numbered 00–10, one module per session.

## Step 4: Connect Claude Code

Claude Code lets you talk to Claude directly inside your editor — it reads your files, writes and edits, and runs commands from a sidebar panel.

**VS Code:** Extensions view (`Cmd+Shift+X` / `Ctrl+Shift+X`) → search "Claude Code" → install (official Anthropic publisher) → open any file → click the orange spark icon (✱) → sign in.

**Antigravity:** same Extensions shortcut → install "Claude Code" from Open VSX → open the panel from the Spark icon → sign in (an API key is the more reliable fallback right now, since this integration is newer).

**If the extension won't connect**, fall back to the command line, which works the same everywhere:
```bash
npm install -g @anthropic-ai/claude-code
```
Then run `claude` in your editor's integrated terminal.

### Using it — coders vs. non-coders

- **If you code:** ask Claude to write, refactor, or debug directly — e.g. *"Refactor this data-loading function to run in parallel across nodes."*
- **If you don't code:** describe what you want in plain language — e.g. *"Write a Slurm batch script that runs my Python script `analyze.py` on 4 nodes for 2 hours, and explain each line so I understand what it's doing."*

Either way works. Building an HPC assignment doesn't require you to already know Slurm, Python, or bash — it requires knowing what you want the assignment to *do*.

## Troubleshooting

**"Password authentication is not supported"** — get a Personal Access Token: [github.com/settings/tokens](https://github.com/settings/tokens) → **Generate new token (classic)** → check `repo` scope → generate → copy immediately (shown once) → paste it when Git prompts for a password.

**"Repository not found"** — check for a URL typo, and whether the repo landed under your personal account vs. an org.

**403 error when pushing** — usually a stale cached credential. Clear it (Mac: Keychain Access → search "github.com" → delete; Windows: Credential Manager → remove the `git:https://github.com` entry), then re-check your remote URL:
```bash
git remote -v
git remote set-url origin https://github.com/YOUR-USERNAME/your-repo.git
```

**Claude Code extension doesn't show up** — make sure an actual file is open, not just a folder. Try "Developer: Reload Window." In Antigravity, if the CLI doesn't recognize the extension, use the CLI fallback above instead.

## Checkpoint

<ul class="checklist">
<li><code>course-site</code> repo created (public) and cloned locally</li>
<li><code>course-toolkit</code> repo created (private) and cloned locally</li>
<li>Both folders open in your editor and briefly explored</li>
<li>Claude Code installed and connected</li>
<li>One test prompt sent successfully</li>
</ul>

Next: [Module 02 — Learning Outcomes & Curriculum Map](module-02.html)
