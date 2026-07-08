---
title: Day 1
---

<span class="day-pill">Day 1 · Monday, July 27</span>

# Set Up — GitHub Course Builder

## Schedule

| Time | Session | Lead |
|:---|:---|:---|
| 9:30 – 10:00 AM | Arrival, coffee, informal networking | — |
| 10:00 – 10:30 AM | Welcome from TACC, daily agenda review & introductions | Dr. Jordan |
| 10:30 – 12:30 PM | What is NAIRR? A tour of the ecosystem. Set up your course-builder repos: GitHub + GitHub Pages | Whitney |
| 12:30 – 1:30 PM | Lunch | |
| 1:30 – 2:00 PM | What goes into AI & a shared repo — what's safe, what's not | Dr. Jordan |
| 2:00 – 2:15 PM | Scale-first design: creating assignments & courses for HPC — why HPC? | Whitney |
| 2:15 – 3:00 PM | Creating and mapping your learning outcomes | Independent |
| Evening | All White Party | Ms. Dawson |

## What you'll build today

### Set up your two repos & environment

You're not starting from a blank repo — you're using a pre-built template. For each of `course-site` (public) and `course-toolkit` (private):

1. Click the green **"Use this template"** button → **"Create a new repository"**
2. Name it whatever you'll actually use going forward
3. Set visibility: `course-site` → **Public**, `course-toolkit` → **Private**
4. Clone both locally, side by side:
   ```bash
   git clone https://github.com/YOUR-USERNAME/your-course-site.git
   git clone https://github.com/YOUR-USERNAME/your-course-toolkit.git
   ```

Then connect **Claude Code**, the extension that lets you talk to Claude directly inside your editor:

- **VS Code:** Extensions view (`Cmd+Shift+X` / `Ctrl+Shift+X`) → search "Claude Code" → install → sign in.
- **Antigravity:** same shortcut → install "Claude Code" from Open VSX → sign in (an API key is the more reliable fallback right now).
- **Either editor, if the extension won't connect:** `npm install -g @anthropic-ai/claude-code`, then run `claude` in your terminal.

Once connected, send one test prompt — coders can ask Claude to explain a file in the repo; non-coders can ask it to write a one-line Slurm script and explain what it does.

<div class="card">

**The whole point of this week:** you don't need to already know Slurm, Python, or bash to build an HPC-based assignment. You need to know what you want the assignment to *do* — Claude handles the syntax, whether you're writing code yourself or asking for it in plain English.

</div>

### Draft your learning outcomes

Draft 3–5 learning outcomes for your course — at least one should involve using HPC resources. For each, note how it'll be assessed (assignment, quiz, exam) and whether it's HPC-based. You don't need the technical details of the HPC assignment yet, just the flag — that gets built out on Day 2 and 3.

## Reference material

- Full setup walkthrough with troubleshooting (GitHub tokens, credential errors, extension issues): available in your `course-site` repo's Builder Guide once created

Next up: **Day 2** — curriculum map, syllabus draft, and HPC acclimation begins.
