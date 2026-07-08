---
title: Dataset Discovery for HPC
---

# Finding Datasets in Your Domain & Building a Data Workflow with AI

Before you can build an HPC-based assignment, you need real (or realistic) data for students to work with. This page is about finding that data, then using Claude to sketch out the steps ("the workflow") for turning raw data into something your assignment actually uses.

## Where to look for datasets

Start broad, then narrow to your discipline:

- **General research data repositories:** [data.gov](https://www.data.gov), [Kaggle Datasets](https://www.kaggle.com/datasets), [Google Dataset Search](https://datasetsearch.research.google.com/), [Hugging Face Datasets](https://huggingface.co/datasets)
- **Discipline-specific:** most fields have a standard go-to repository; e.g. genomics (NCBI/GEO), climate science (NOAA), social science (ICPSR), astronomy (NASA/MAST). Ask Claude: *"What are the standard public dataset repositories for [my field]?"*; it can point you toward the field-specific ones you may not know about.
- **NAIRR-affiliated resources:** ask your program contact about NAIRR's own resource index for datasets and tools by discipline; it's referenced elsewhere in program materials as a starting point worth checking before searching from scratch.

## Using Claude to scope a computational plan

Once you have a candidate dataset, don't jump straight into scripting; describe the shape of the problem to Claude first and let it help you plan:

> *"I have a dataset of [describe: size, format, what's in it]. My assignment goal is for students to [describe the task]. What's a reasonable step-by-step computational workflow, and which steps actually need HPC resources vs. which could run on a laptop?"*

This matters because not every step needs a supercomputer; Claude can help you identify the one or two computationally heavy steps (the actual reason for using HPC) versus the setup/cleanup steps that don't need it, so your assignment's HPC component is meaningful rather than incidental.

## Turning this into assignment material

Once you have a workflow sketched:
1. Note the dataset source and access instructions; this goes in `course-site/resources.md` (Module 04, Part 2)
2. Ask Claude to scaffold the starter notebook/script matching the workflow you just sketched
3. If you don't code, ask Claude to also produce a plain-language walkthrough of what the script does; this doubles as material for you to reference when writing the quiz

## A note on data size

If your dataset is large, see [Moving Data Onto the Morehouse Supercomputing Facility](moving-data-tacc.html) for transfer options before you get to the actual assignment-building step.

Next: back to [Day 3](../day-3.html).
