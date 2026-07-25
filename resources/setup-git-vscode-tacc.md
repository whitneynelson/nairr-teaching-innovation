---
title: Setup - Git, VS Code, and Morehouse Supercomputing Facility
---

# Installing Git, VS Code/Antigravity (or Claude Desktop), and Logging Into the Morehouse Supercomputing Facility

Before this week starts, you need three things on your computer: a way to save/share your work (Git or GitHub Desktop), a way to write files and talk to Claude (an editor, or Claude Desktop if you'd rather skip installing an IDE), and access to the supercomputer you'll run assignments on (the Morehouse Supercomputing Facility). None of this requires prior coding experience; it's just installing software and creating accounts, the same as setting up any new app.

## 1. Choose your setup: Option A (editor) or Option B (no IDE)

Everything downstream; cloning your repos, editing files, talking to Claude; works the same either way. Pick once and stick with it for the week.

### Option A: Git + VS Code or Antigravity

- **Install Git:**
  - **Mac:** open Terminal and type `git --version`. If it's not installed, your Mac will prompt you to install the Xcode Command Line Tools; say yes.
  - **Windows:** download and install [Git for Windows](https://git-scm.com/download/win). Accept the default options during setup unless you have a specific reason not to.
  - **Verify it worked:** open a terminal (Mac: Terminal app; Windows: the "Git Bash" app that Git for Windows installs) and run:
    ```bash
    git --version
    ```
    You should see a version number, e.g. `git version 2.43.0`.
- **Install an editor:**
  - **VS Code:** download from [code.visualstudio.com](https://code.visualstudio.com/); pick your operating system, run the installer, accept defaults.
  - **Antigravity:** an alternative editor also supported this week; download from your program's provided link and install the same way.
  - Either one works identically for this program; use whichever you're more comfortable with, or the one your facilitator recommends.
- You'll talk to Claude through the **Claude Code** extension inside your editor (see Module 00–01, Step 4).

### Option B: GitHub Desktop + Claude Desktop (no IDE, no terminal)

Prefer not to install a code editor at all? This path skips both the editor and the command line.

- **GitHub Desktop:** download from [desktop.github.com](https://desktop.github.com/) and sign in with your GitHub account. This is what you'll use to clone, save, and publish your repos with buttons instead of Git commands.
- **Claude Desktop:** download from [claude.ai/download](https://claude.ai/download) and sign in with your Claude Pro, Max, Team, or Enterprise account. In **Settings → Connectors**, enable the **Filesystem** connector and point it at the folder where you'll keep your cloned repos; this lets you talk to Claude in a normal chat window and have it read and write your course files directly, the same job the Claude Code extension does inside an editor.
- Nothing here requires typing a command; GitHub Desktop and Claude Desktop are both point-and-click apps.

If you're unsure which to pick: Option B is the faster on-ramp if you've never used a code editor or terminal before; Option A gives you a bit more visibility into what's happening under the hood, which some coders prefer. Either gets you to the same place by Friday.

## 2. Create your Morehouse Supercomputing Facility account and set up MFA

The Morehouse Supercomputing Facility is the supercomputer provider your HPC assignments will run on.

1. Request your account at [bpccenter.org/current-programs/cbpc-hpc-resources](https://www.bpccenter.org/current-programs/cbpc-hpc-resources), using your .edu email address; **approval can take a few business days**, which is why this step is due two weeks before the accelerator, not the week of. (Under the hood, the allocation itself runs on TACC's Vista system; this is a backend detail and doesn't change how you request or use your account.) Questions about the account itself go to Dr. Ashley Scruse, Deputy Director (ashley.scruse@morehouse.edu).
2. Once approved, set up multi-factor authentication (MFA) through Duo or Okta, whichever your account setup specifies. This is the same idea as MFA on your bank or email; a phone app that confirms it's really you logging in.
3. **Logging in, Mac or PC:** access this week happens through your browser and, later, through Tapis (covered in Module 00–01 and the HPC Acclimation sessions); you do not need a special client installed beyond what's listed above. If your specific program setup requires an SSH client on Windows, PuTTY or the Git Bash terminal that came with Git for Windows both work; confirm the exact login endpoint with your program contact, since this can vary by cohort. For the full request-to-walkthrough path, including a runnable example, see [Accessing the Morehouse Supercomputing Facility via TAPIS](accessing-tapis.html).

<div class="card">

**If anything here doesn't match what you were told in your welcome email** (account portal links, specific login endpoints), trust your program contact's instructions over this page and let them know so it can get corrected here too.

</div>

## Checklist

<ul class="checklist">
<li>Option A: Git installed (<code>git --version</code> works in your terminal) and VS Code or Antigravity installed &mdash; <em>or</em> &mdash; Option B: GitHub Desktop and Claude Desktop installed, with the Filesystem connector enabled</li>
<li>Morehouse Supercomputing Facility account requested (and approved, if enough lead time)</li>
<li>MFA (Duo/Okta) set up on your Morehouse Supercomputing Facility account</li>
</ul>

Next: see [Accessing the Morehouse Supercomputing Facility via TAPIS](accessing-tapis.html) for the full walkthrough, [Git Basics & Cheat Sheet](git-basics.html) if you're new to Git, or head back to the [Pre-Event](../pre-event.html) checklist.
