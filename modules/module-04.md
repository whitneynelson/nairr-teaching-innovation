---
title: "Module 04: Module Builder"
---

# Module 04: Module Builder

*Feeds: Part 1: Day 2, 2:30–3:00 PM · Part 2: Day 3, 11:00 AM–12:30 PM · Part 3: Day 4, 2:30–3:00 PM*

This is the module where you build one complete unit of your course; lecture, slides, quiz, and assignment; as a repeatable pattern you'll copy for every other unit later. It's spread across three days on purpose.

## Before you start

Pick **one module** from your curriculum map (`course-site/schedule.md`) to build fully, end to end.

**On Track II?** You likely already know exactly which assignment you came here to build, rather than picking generically from a curriculum map. If so, skip that framing and just confirm which existing course/unit it belongs to — this module is your main goal for the week, not a side quest.

**Before scaffolding anything, identify a dataset or resource** (`course-site/resources/datasets.md`). This applies no matter your track — an HPC-based assignment without an identified dataset isn't buildable yet. Haven't done this yet? See [Dataset Discovery](../resources/dataset-discovery.html) before Step 1.

## Part 1: Lecture outline + slide deck (Day 2)

### Step 1: Outline the module

> *"Draft a lecture outline for [module topic], covering [outcome]. Include a short intro, 2-3 core concepts, and a wrap-up tying to the HPC assignment."*

Already have lecture notes or slides for this module? Bring them, and ask your AI coding assistant to restructure them into this format rather than starting over.

### Step 2: Build the slide deck

Source lives in Canva or Slides; export a PDF and archive it once done.
- **If you code:** your AI coding assistant can also generate a deck directly (e.g. via `pptxgenjs`).
- **If you don't code:** stick with Canva/Slides; your AI coding assistant can still help write the outline and speaker notes.

### Step 3: Split public vs. private

- `course-site/modules/module-XX.md` → student-facing outline, slides link, assignment link
- `course-toolkit/lecture-prep-notes/module-XX-notes.md` → your full prep notes

## Part 2: Quiz + assignment supplementary material (Day 3)

*(The "moving data onto HPC" walkthrough right before this session is the technical backbone for the assignment you're building here; see [Dataset Discovery](../resources/dataset-discovery.html) if you haven't done that yet.)*

### Step 4: Build the quiz

In `course-toolkit/quizzes/module-XX-quiz.md`, with a full answer key. Stays private.

### Step 5: Build the assignment's supplementary material

First, a question separate from your own coding comfort: **do the students in this course code?** This decides the assignment's structure, not just how you build it.

- **Students code:** they get a starter notebook/script with clear TODOs to complete themselves, submitted as their own batch/interactive job; the normal case.
- **Students don't code:** don't hand them something to edit as code. Two patterns work well instead:
  - **Pre-run, then interpret:** you (or your AI coding assistant) run the computation ahead of time; students receive the output; plots, tables, job logs; and the assignment is entirely about interpreting and reasoning about it.
  - **Config-only:** students get a notebook where the only thing they touch is one or two clearly labeled input values (a date range, a sample size, a threshold); they change the value, click Run All, and never read or write code as code.
  Either way, the graded deliverable becomes understanding and reasoning (e.g. *"the job took 40 minutes on 1 node vs. 6 on 8; why?"*), not code correctness. See [Sample Assignments: "If your students don't code"](../resources/sample-assignments.html) for more.

In `course-site/resources/`: the dataset into `datasets.md`, setup instructions and any tools/software into `tools.md`, and which pattern above this assignment uses alongside whichever of the two it's most relevant to.
- **If you code:** ask your AI coding assistant to scaffold the actual assignment notebook/script now.
- **If you don't code:** describe the assignment goal and dataset and let your AI coding assistant draft the starter notebook/script *and* a plain-language explanation.

Already have an assignment written for this module? Upload or paste it and have your AI coding assistant adapt it rather than drafting from nothing.

## Part 3: Finish building the module (Day 4)

### Step 6: Close any gaps

Does `course-site/modules/module-XX.md` link to everything; slides, assignment, quiz link (not quiz content)?

### Step 7: Public/private leak check

Re-read the public file and confirm no answer keys, grading notes, or private prep content made it in.

## Checkpoint

<ul class="checklist">
<li>Lecture outline + slide deck built and linked in <code>course-site/modules/module-XX.md</code></li>
<li>Full prep notes in <code>course-toolkit/lecture-prep-notes/module-XX-notes.md</code></li>
<li>Quiz with answer key in <code>course-toolkit/quizzes/</code></li>
<li>Dataset identified in <code>course-site/resources/datasets.md</code>, tools/setup instructions in <code>resources/tools.md</code></li>
<li>Public file re-checked for accidental private content</li>
</ul>

Next: [Module 05: Grading Scale & Rubrics](module-05.html)
