---
title: "Module 11: Parallel Computing with MPI & OpenMP (Optional, CS Track)"
---

# Module 11: Parallel Computing with MPI & OpenMP

**Optional, self-paced, CS track.** Not part of the live agenda. This module assumes you already code; it's an added-depth alternative or supplement to `module-04` for instructors teaching CS/programming courses, going past "AI writes the script for you" into the mechanics of parallel programming itself.

## Before you start

Get a module number in mind: does this fill a slot already on your curriculum map, or is it a bonus module beyond it? Either way, this reuses the same build pattern as `module-04`; if you haven't done that one yet, it's worth doing first so the pattern is familiar.

## Step 1: Lecture outline

Cover, at minimum:
- Shared-memory (OpenMP) vs. distributed-memory (MPI) parallelism, and why the distinction matters once code moves from a laptop to a multi-node cluster
- When to reach for which: OpenMP for parallelizing loops within a single node's cores; MPI for spreading work across multiple nodes
- A concrete example (e.g. parallel sum or matrix multiply) shown in both models
- A wrap-up tying back to your course's HPC assignment thread

Already have material on parallel computing? Bring it and ask your AI coding assistant to restructure it into this format rather than starting over.

Draft into `course-site/modules/module-XX.md` (public outline) and `course-toolkit/lecture-prep-notes/module-XX-notes.md` (your full prep notes).

## Step 2: Runnable assignment

Ask your AI coding assistant to scaffold:
1. A small, parallelizable problem in serial form (a deliberately slow baseline)
2. An OpenMP version (e.g. `#pragma omp parallel for` in C, or a threaded equivalent)
3. An MPI version (e.g. `mpi4py` in Python, or `MPI_Send`/`MPI_Recv` in C)
4. A Slurm batch script for each version, with every `#SBATCH` line explained; pay close attention to `--ntasks` vs. `--cpus-per-task`, since getting these mismatched lets a job run without erroring while quietly not parallelizing at all

Draft supplementary material into `course-site/resources/`: the dataset (if any) into `datasets.md`, starter code and setup instructions into `tools.md`.

## Step 3: Quiz

Draft into `course-toolkit/quizzes/module-XX-quiz.md`, with a full answer key. Mix conceptual questions (e.g. "why didn't this OpenMP code speed up on 8 cores?") with applied ones (e.g. reading a Slurm job's wall-clock output). Stays private.

## Step 4: Public/private leak check

Re-read `course-site/modules/module-XX.md`; confirm no answer keys, prep notes, or grading detail made it into the public file.

## Checkpoint

<ul class="checklist">
<li>Module number confirmed (curriculum-map slot or bonus module)</li>
<li>Lecture outline in <code>course-site/modules/module-XX.md</code>, full prep notes in <code>course-toolkit/lecture-prep-notes/module-XX-notes.md</code></li>
<li>OpenMP + MPI starter code and Slurm scripts drafted in <code>course-site/resources/tools.md</code>; dataset (if any) in <code>resources/datasets.md</code></li>
<li>Quiz with answer key in <code>course-toolkit/quizzes/</code></li>
<li>Public file re-checked for accidental private content</li>
</ul>

Pairs with [Module 12: Containerization for Reproducibility](module-12.html); neither depends on the other.
