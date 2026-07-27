---
title: "Module 02: Learning Outcomes to Curriculum Map"
---

# Module 02: Learning Outcomes → Curriculum Map

*Feeds: Day 1, 2:15–3:00 PM (outcomes) + Day 2, 10:15–11:00 AM (curriculum map)*

A "learning outcome" is just a specific sentence describing what a student should be able to *do* by the end of a unit (not just "understand" it). A "curriculum map" is your week-by-week sequence of topics. This module builds both.

## Before you start: which track are you on?

How much of this module you need depends on the track from your application:

- **Track I — New Course/Program Design:** the full session below, as written.
- **Track II — Assignment Development:** you likely already have a course and syllabus, and are here to build one (or a few) new or updated assignments; not a whole course. Still outline a learning outcome for each assignment you're building, scoped to that assignment rather than a full 3–5-outcome course-wide pass. Work through it one thing at a time: assignment topic first, then your students' prior experience, then the HPC+AI angle. If you already have course-wide outcomes, map the assignment against the existing one it serves instead of drafting new. Treat the curriculum map as "where does this sit in my existing schedule."
- **Track III — Course/Program Revision:** you have existing outcomes to revise, not draft fresh; use the "already have outcomes" branch in Step 1. Curriculum map becomes a check-and-adjust pass on your existing schedule.

Whichever track: before moving on to [Module 04](module-04.html), each HPC-based assignment or outcome also needs a dataset or resource identified (`course-site/resources/datasets.md`); this is a prerequisite for building it, not optional busywork.

**A distinction worth being explicit about, every track:** the HPC-based (and AI-based) flag describes what *you want your students* to do to complete the assignment — using HPC resources and an AI coding assistant themselves — not that you used Claude to help build the assignment material. Those are different things; the goal is an assignment where students use HPC + AI, not just one Claude helped you write.

## Part 1: Learning outcomes

### Step 1: Draft 3–5 outcomes

Ask your AI coding assistant to help turn a rough sense of "what I want students to be able to do" into properly scoped outcomes:

> *"Help me write 3-5 learning outcomes for a [course topic] course. Students range from [prior experience]. I want at least one outcome where students themselves use HPC resources and an AI coding assistant to complete the work."*

Already have learning outcomes drafted for this course? Paste them in and ask your AI coding assistant to map them against the HPC requirement instead of starting from scratch.

### Step 2: Map each outcome to an assessment

For each outcome, note: how it'll be assessed (assignment, quiz, exam), and whether it's HPC-based. You don't need the technical details yet; just flag it. [Module 04](module-04.html) is where the actual assignment gets designed.

### Step 3: Fill in the table

In `course-toolkit/learning-outcomes-map.md`:

```
| Module | Learning Outcome | Assessment | HPC-Based? |
|---|---|---|---|
```

## Part 2: Curriculum map

### Step 4: Sequence your modules

Working from your outcomes table, sketch a week-by-week map:

> *"Given these learning outcomes [paste table], suggest a logical order across N weeks, noting where the HPC-based assignment should land."*

### Step 5: Build the public schedule

In `course-site/schedule.md`; topic and assignment-due-date only, no grading detail (that stays private).

## Checkpoint

<ul class="checklist">
<li><code>course-toolkit/learning-outcomes-map.md</code> has outcomes (3-5 for Track I, or one per assignment for Track II/III), each mapped to an assessment</li>
<li>At least one outcome flagged as HPC-based, with a dataset or resource identified for it (<code>course-site/resources/datasets.md</code>)</li>
<li><code>course-site/schedule.md</code> has a full module sequence with assignment due dates (Track I), or an updated/confirmed schedule showing where this week's assignment(s) land (Track II/III)</li>
</ul>

Next: [Module 03: Draft Your Syllabus](module-03.html)
