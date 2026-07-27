---
title: "Module 13: ML Hub for Tapis (Optional, CS Track)"
---

# Module 13: ML Hub for Tapis

**Optional, self-paced, CS track.** Not part of the live agenda. This module assumes you already code; it's an added-depth alternative or supplement to `module-04` for instructors teaching CS/programming courses who want to go further into applied ML and model deployment specifically.

## A technical note

ML Hub for Tapis ([`tapis-project/ml-hub`](https://github.com/tapis-project/ml-hub) on GitHub) is a developer-facing REST-API framework, not a non-coder-friendly tool; using it means Git, Python 3.10+, and some Docker familiarity. It's a third optional CS-track module alongside `module-11` (parallel computing) and `module-12` (containerization); it isn't a replacement for the general-track Tapis session everyone else uses, which stays simple via the interactive/batch job path covered on Day 2.

## Before you start

Get a module number in mind: does this fill a slot already on your curriculum map, or is it a bonus module beyond it? This reuses the same build pattern as `module-04`; if you haven't done that one yet, it's worth doing first.

## Step 1: Lecture outline

Cover, at minimum:
- What ML Hub adds on top of Tapis: discovering, downloading, and running inference against pre-trained models (initially via Hugging Face) without hand-building that infrastructure
- The three core pieces: Models Hub (browse/download), Inference Service (submit a request, get a prediction back), Training Engine (fine-tune on your own data)
- A concrete example: one small, well-known Hugging Face model walked through discovery → download → inference end to end
- A wrap-up tying back to your course's HPC assignment thread: why inference or fine-tuning at this scale needs HPC rather than a laptop

Already have material on applied ML/model deployment? Bring it and ask your AI coding assistant to restructure it into this format rather than starting over.

Draft into `course-site/modules/module-XX.md` (public outline) and `course-toolkit/lecture-prep-notes/module-XX-notes.md` (your full prep notes).

## Step 2: Runnable assignment

Ask your AI coding assistant to scaffold:
1. A small script or notebook querying the Models Hub API for a specific pre-trained model (e.g. a small classification or text model on Hugging Face)
2. An inference request against that model via the Inference Service, run on a compute node, not a login node
3. Optionally, for a more advanced assignment: a fine-tuning pass via the Training Engine on a small labeled dataset
4. A Slurm batch script wrapping whichever of the above the assignment uses, with each `#SBATCH` line explained

Draft supplementary material into `course-site/resources/`: the dataset (if any) into `datasets.md`, starter code and setup instructions into `tools.md`.

## Step 3: Quiz

Draft into `course-toolkit/quizzes/module-XX-quiz.md`, with a full answer key. Mix conceptual questions (e.g. "why does fine-tuning need HPC when inference on a pre-trained model might not?") with applied ones (e.g. reading an inference request's output/error). Stays private.

## Step 4: Public/private leak check

Re-read `course-site/modules/module-XX.md`; confirm no answer keys, prep notes, or grading detail made it into the public file.

## Checkpoint

<ul class="checklist">
<li>Module number confirmed (curriculum-map slot or bonus module)</li>
<li>Lecture outline in <code>course-site/modules/module-XX.md</code>, full prep notes in <code>course-toolkit/lecture-prep-notes/module-XX-notes.md</code></li>
<li>Model discovery, inference (and optionally fine-tuning) code drafted; supplementary material in <code>course-site/resources/</code></li>
<li>Quiz with answer key in <code>course-toolkit/quizzes/</code></li>
<li>Public file re-checked for accidental private content</li>
</ul>

Pairs with [Module 11: Parallel Computing with MPI & OpenMP](module-11.html) and [Module 12: Containerization for Reproducibility](module-12.html); none depend on each other.
