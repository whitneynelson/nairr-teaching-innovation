---
title: "Module 04: Module Builder"
---

# Module 04: Module Builder

*Feeds: Part 1: Day 2, 1:30–3:00 PM · Part 2: Day 3, 10:30–11:30 AM · Part 3: Day 4, 2:30–3:00 PM*

This is the module where you build one complete unit of your course; lecture, slides, quiz, and assignment; as a repeatable pattern you'll copy for every other unit later. It's spread across three days on purpose.

## Before you start

Pick **one module** from your curriculum map (`course-site/schedule.md`) to build fully, end to end.

## Part 1: Lecture outline + slide deck (Day 2)

### Step 1: Outline the module

> *"Draft a lecture outline for [module topic], covering [outcome]. Include a short intro, 2-3 core concepts, and a wrap-up tying to the HPC assignment."*

Already have lecture notes or slides for this module? Bring them, and ask Claude to restructure them into this format rather than starting over.

### Step 2: Build the slide deck

Source lives in Canva or Slides; export a PDF and archive it once done.
- **If you code:** Claude can also generate a deck directly (e.g. via `pptxgenjs`).
- **If you don't code:** stick with Canva/Slides; Claude can still help write the outline and speaker notes.

### Step 3: Split public vs. private

- `course-site/modules/module-XX.md` → student-facing outline, slides link, assignment link
- `course-toolkit/lecture-prep-notes/module-XX-notes.md` → your full prep notes

## Part 2: Quiz + assignment supplementary material (Day 3)

*(The "moving data onto HPC" walkthrough right before this session is the technical backbone for the assignment you're building here; see [Dataset Discovery](../resources/dataset-discovery.html) if you haven't done that yet.)*

### Step 4: Build the quiz

In `course-toolkit/quizzes/module-XX-quiz.md`, with a full answer key. Stays private.

### Step 5: Build the assignment's supplementary material

In `course-site/resources.md`; datasets, reference links, setup instructions.
- **If you code:** ask Claude to scaffold the actual assignment notebook/script now.
- **If you don't code:** describe the assignment goal and dataset and let Claude draft the starter notebook/script *and* a plain-language explanation.

Already have an assignment written for this module? Upload or paste it and have Claude adapt it rather than drafting from nothing.

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
<li>Assignment supplementary material in <code>course-site/resources.md</code></li>
<li>Public file re-checked for accidental private content</li>
</ul>

Next: [Module 05: Grading Scale & Rubrics](module-05.html)
