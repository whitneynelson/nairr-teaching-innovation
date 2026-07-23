---
title: Day 1
---

<span class="day-pill">Day 1 · Monday, July 27</span>

# Set Up | GitHub Course Builder

## Schedule

| Time | Session |
|:---|:---|
| 9:30 – 10:00 AM | Arrival, coffee, informal networking |
| 10:00 – 10:30 AM | Welcome, daily agenda review & introductions |
| 10:30 – 12:30 PM | What is NAIRR? A tour of the ecosystem. Set up your course-builder repos: GitHub + GitHub Pages |
| 12:30 – 1:30 PM | Lunch |
| 1:30 – 2:00 PM | What goes into AI & a shared repo; what's safe, what's not |
| 2:00 – 2:15 PM | Scale-first design: creating assignments & courses for HPC; why HPC? |
| 2:15 – 3:00 PM | Creating and mapping your learning outcomes |
| 7:00 – 8:00 PM | [All White Party](#evening) |

## What you'll build today

### Set up your two repos & environment

You're not starting from a blank repo; you're using a pre-built template. For each of `course-site` (public) and `course-toolkit` (private):

#### 1. Create your repos from the template

1. Go to the template repos: [github.com/whitneynelson/course-site](https://github.com/whitneynelson/course-site) and [github.com/whitneynelson/course-toolkit](https://github.com/whitneynelson/course-toolkit)
2. Click the green **"Use this template"** button → **"Create a new repository"**
3. Name it whatever you'll actually use going forward
4. Set visibility: `course-site` → **Public**, `course-toolkit` → **Private**

#### 2. Clone both locally

```bash
git clone https://github.com/YOUR-USERNAME/your-course-site.git
git clone https://github.com/YOUR-USERNAME/your-course-toolkit.git
```

Open both folders side by side in your editor.

#### 3. Connect Claude Code

Claude Code is the extension that lets you talk to Claude directly inside your editor:

- **VS Code:** Extensions view (`Cmd+Shift+X` / `Ctrl+Shift+X`) → search "Claude Code" → install → sign in.
- **Antigravity:** same shortcut → install "Claude Code" from Open VSX → sign in (an API key is the more reliable fallback right now).
- **Either editor, if the extension won't connect:** `npm install -g @anthropic-ai/claude-code`, then run `claude` in your terminal.

#### 4. Send a test prompt

Once connected, send one test prompt; coders can ask it to explain a file in the repo, non-coders can ask it to write a one-line Slurm script and explain what it does.

<div class="card">

You don't need to already know Slurm, Python, or bash to build an HPC-based assignment this week. You need to know what you want the assignment to *do*; your AI-powered coding assistant handles the syntax, whether you're writing code yourself or asking for it in plain English.

</div>

### Why repo structure matters

The two folders you just created aren't just storage; they're the environment Claude works inside all week, and a well-organized one makes every prompt you write from here forward more effective. Notice that `course-site` already ships with a `CLAUDE.md` (root instructions for how Claude should operate in that repo) and a `skills/` folder (step-by-step guides Claude reads before walking you through each module). That's deliberate: a README stating intent, docs explaining decisions, and clear guardrails give Claude the same context a new collaborator would need, so it plans and writes better code with less back-and-forth. Keep that same discipline as you build out your own course content this week; the more your repo documents itself, the less you'll have to re-explain to Claude in every session.

### Draft your learning outcomes

Draft 3–5 learning outcomes for your course; at least one should involve using HPC resources. For each, note how it'll be assessed (assignment, quiz, exam) and whether it's HPC-based. You don't need the technical details of the HPC assignment yet, just the flag; that gets built out on Day 2 and 3.

Already have learning outcomes drafted for this course? Paste them in and ask your AI-powered coding assistant to map them against the HPC requirement instead of starting from scratch.

## Full module instructions

- [Module 00–01: Set Up Your Repos & Environment](modules/module-00-01.html); includes full troubleshooting (GitHub tokens, credential errors, extension issues)
- [Module 02: Learning Outcomes → Curriculum Map](modules/module-02.html); outcomes portion starts today

## Reference material

- [Setup: Git, VS Code/Antigravity, and Morehouse Supercomputing Facility](resources/setup-git-vscode-tacc.html)
- [Git basics + cheat sheet](resources/git-basics.html)

## This evening {#evening}

**All White Party** in the main area of the Royalton Plaza, 7:00-8:00 PM, weather permitting.

Next up: **Day 2**; curriculum map, syllabus draft, and HPC acclimation begins.
