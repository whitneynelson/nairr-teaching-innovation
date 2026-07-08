---
title: Sample Assignments by Discipline
---

# Sample Assignments | Tools & Datasets by Discipline

If you're staring at a blank page trying to imagine what an "HPC-based assignment" even looks like in your field, this page is a set of starting points, not a prescription. Adapt, don't adopt wholesale.

## How to use this page

Pick the discipline closest to yours, use the sample as a starting prompt for Claude rather than a finished assignment: *"Adapt this assignment idea for a [your course level] course on [your topic], using [your actual dataset if you have one]."*

## Life sciences / biology

- **Sample idea:** students align short DNA/RNA sequences against a reference genome using a standard bioinformatics tool (e.g. BLAST or a simple aligner), submitted as a batch job rather than run locally, then interpret the output.
- **Where data comes from:** NCBI/GEO, or a de-identified/synthetic dataset if working with sensitive samples.

## Physical sciences / astronomy / climate

- **Sample idea:** students run a parameter sweep (the same simulation repeated across a range of input values) as parallel array jobs, then aggregate and visualize the results.
- **Where data comes from:** NASA/MAST for astronomy, NOAA for climate; many fields have a standard simulation tool that's already HPC-friendly.

## Social sciences

- **Sample idea:** students run a large-scale text or survey analysis (e.g. topic modeling across a large text corpus) that would be impractical on a laptop due to dataset size, submitted as a single substantial batch job.
- **Where data comes from:** ICPSR, or a public survey/text dataset in your specific subfield.

## Computer science / data science

- **Sample idea:** students train a model across a parameter grid or on a dataset too large for a laptop, comparing runtime/accuracy tradeoffs across configurations; a natural fit for demonstrating *why* HPC matters, not just how to use it.
- **Where data comes from:** Kaggle, Hugging Face Datasets, or your own research data.

## Humanities / interdisciplinary

- **Sample idea:** large-scale text mining or corpus analysis across a digitized archive too large to process locally (e.g. analyzing word frequency or sentiment trends across a large historical text collection).
- **Where data comes from:** many humanities archives now publish machine-readable corpora; ask Claude to help identify one for your specific area.

## A framing question worth asking yourself

For any of these: what specifically requires HPC here; scale, speed, or parallelism? If you can't answer that in one sentence, the assignment may work fine on a laptop, and the HPC framing should be applied to a different part of your course instead. This connects to Day 1's "Scale-First Design: Why HPC?" session.

Next: back to [Day 4](../day-4.html).
