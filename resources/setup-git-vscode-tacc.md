---
title: Setup - Git, VS Code, and Morehouse Supercomputing Facility
---

# Installing Git, VS Code/Antigravity, and Logging Into the Morehouse Supercomputing Facility

Before this week starts, you need three things on your computer: a way to save/share your work (Git), an editor to write in (VS Code or Antigravity), and access to the supercomputer you'll run assignments on (the Morehouse Supercomputing Facility). None of this requires prior coding experience; it's just installing software and creating accounts, the same as setting up any new app.

## 1. Install Git

Git tracks changes to your files and is how your course repos get created, saved, and shared.

- **Mac:** open Terminal and type `git --version`. If it's not installed, your Mac will prompt you to install the Xcode Command Line Tools; say yes.
- **Windows:** download and install [Git for Windows](https://git-scm.com/download/win). Accept the default options during setup unless you have a specific reason not to.
- **Verify it worked:** open a terminal (Mac: Terminal app; Windows: the "Git Bash" app that Git for Windows installs) and run:
  ```bash
  git --version
  ```
  You should see a version number, e.g. `git version 2.43.0`.

## 2. Install an editor: VS Code or Antigravity

This is where you'll open your course files and talk to Claude Code.

- **VS Code:** download from [code.visualstudio.com](https://code.visualstudio.com/); pick your operating system, run the installer, accept defaults.
- **Antigravity:** an alternative editor also supported this week; download from your program's provided link and install the same way.

Either one works identically for this program; use whichever you're more comfortable with, or the one your facilitator recommends.

## 3. Create your Morehouse Supercomputing Facility account and set up MFA

The Morehouse Supercomputing Facility is the supercomputer provider your HPC assignments will run on.

1. Request your account at [bpccenter.org/current-programs/cbpc-hpc-resources](https://www.bpccenter.org/current-programs/cbpc-hpc-resources), using your .edu email address; **approval can take a few business days**, which is why this step is due two weeks before the accelerator, not the week of. (Under the hood, the allocation itself runs on TACC's Vista system; this is a backend detail and doesn't change how you request or use your account.) Questions about the account itself go to Dr. Ashley Scruse, Deputy Director (ashley.scruse@morehouse.edu).
2. Once approved, set up multi-factor authentication (MFA) through Duo or Okta, whichever your account setup specifies. This is the same idea as MFA on your bank or email; a phone app that confirms it's really you logging in.
3. **Logging in, Mac or PC:** access this week happens through your browser and, later, through Tapis (covered in Module 00–01 and the HPC Acclimation sessions); you do not need a special client installed beyond what's listed above. If your specific program setup requires an SSH client on Windows, PuTTY or the Git Bash terminal that came with Git for Windows both work; confirm the exact login endpoint with your program contact, since this can vary by cohort. For the full request-to-walkthrough path, including a runnable example, see [Accessing the Morehouse Supercomputing Facility via TAPIS](accessing-tapis.html).

<div class="card">

**If anything here doesn't match what you were told in your welcome email** (account portal links, specific login endpoints), trust your program contact's instructions over this page and let them know so it can get corrected here too.

</div>

## Checklist

<ul class="checklist">
<li>Git installed, <code>git --version</code> works in your terminal</li>
<li>VS Code or Antigravity installed</li>
<li>Morehouse Supercomputing Facility account requested (and approved, if enough lead time)</li>
<li>MFA (Duo/Okta) set up on your Morehouse Supercomputing Facility account</li>
</ul>

Next: see [Accessing the Morehouse Supercomputing Facility via TAPIS](accessing-tapis.html) for the full walkthrough, [Git Basics & Cheat Sheet](git-basics.html) if you're new to Git, or head back to the [Pre-Event](../pre-event.html) checklist.
