---
title: "Module 12: Containerization for Reproducibility (Optional, CS Track)"
---

# Module 12: Containerization for Reproducibility

**Optional, self-paced, CS track.** Not part of the live agenda. This module assumes you already code; it's an added-depth alternative or supplement to `module-04` for instructors teaching CS/programming courses.

## A technical note

Docker itself typically can't run directly on shared HPC systems; its daemon needs root access, which multi-user clusters don't grant. The Morehouse Supercomputing Facility supports **Apptainer** (formerly Singularity) instead: you build and test a container with Docker on your own machine, then convert it to a `.sif` Apptainer image to actually run it on the cluster. Keep that two-step reality in mind as you build this module; "just run Docker on the cluster" is the most common point of confusion for students new to HPC containers.

## Before you start

Get a module number in mind: does this fill a slot already on your curriculum map, or is it a bonus module beyond it? This reuses the same build pattern as `module-04`; if you haven't done that one yet, it's worth doing first.

## Step 1: Lecture outline

Cover, at minimum:
- Why reproducibility matters: "works on my machine" failures, dependency drift, and why research computing specifically cares (an unrerunnable result isn't verifiable)
- Docker locally, Apptainer on the cluster: the root-access constraint, and the build → convert → run workflow
- A concrete example: containerizing a small script with a couple of dependencies, end to end
- A wrap-up tying back to your course's HPC assignment thread

Already have material on containers? Bring it and ask your AI coding assistant to restructure it into this format rather than starting over.

Draft into `course-site/modules/module-XX.md` (public outline) and `course-toolkit/lecture-prep-notes/module-XX-notes.md` (your full prep notes).

## Step 2: Runnable assignment

Ask your AI coding assistant to scaffold:
1. A small script with a couple of real dependencies (something that'd plausibly break on a version mismatch)
2. A `Dockerfile` that builds a working image locally
3. The conversion step to an Apptainer `.sif` image
4. A Slurm batch script that runs the `.sif` image on the cluster (`apptainer exec` or `apptainer run`), with each line explained

Draft supplementary material (starter code, Dockerfile, setup instructions) into `course-site/resources.md`.

## Step 3: Quiz

Draft into `course-toolkit/quizzes/module-XX-quiz.md`, with a full answer key. Mix conceptual questions (e.g. "why can't you just run the Docker image directly on the cluster?") with applied ones (e.g. debugging a failed Apptainer build). Stays private.

## Step 4: Public/private leak check

Re-read `course-site/modules/module-XX.md`; confirm no answer keys, prep notes, or grading detail made it into the public file.

## Checkpoint

<ul class="checklist">
<li>Module number confirmed (curriculum-map slot or bonus module)</li>
<li>Lecture outline in <code>course-site/modules/module-XX.md</code>, full prep notes in <code>course-toolkit/lecture-prep-notes/module-XX-notes.md</code></li>
<li>Dockerfile, Apptainer conversion steps, and Slurm script drafted; supplementary material in <code>course-site/resources.md</code></li>
<li>Quiz with answer key in <code>course-toolkit/quizzes/</code></li>
<li>Public file re-checked for accidental private content</li>
</ul>

Pairs with [Module 11: Parallel Computing with MPI & OpenMP](module-11.html); neither depends on the other.
