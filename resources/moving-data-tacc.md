---
title: Moving Data Onto the Morehouse Supercomputing Facility
---

# Copying, Transferring, and Running Scripts on Large Datasets with the Morehouse Supercomputing Facility

Your data usually starts on your own laptop or an external source, but the actual computing happens on the Morehouse Supercomputing Facility's machines, so before you can run anything, you need to get the data there. This page covers the three common ways to do that, from simplest to most robust.

## Option 1: `scp`; for small-to-medium files

Secure copy, built into every Mac/Linux terminal and Git Bash on Windows:

```bash
# from your laptop to the cluster
scp my-dataset.csv username@hpc-system:/path/to/destination/

# from the cluster back to your laptop
scp username@hpc-system:/path/to/file.csv ./
```

Fine for single files up to a few hundred MB. It will feel slow or may time out for anything larger; move to Option 2 or 3.

## Option 2: `rsync`; for larger transfers, or ones you might redo

`rsync` only copies what's changed, and can resume if interrupted; much friendlier than `scp` for large or repeated transfers:

```bash
rsync -avz --progress my-data-folder/ username@hpc-system:/path/to/destination/
```

- `-a` preserves file structure and permissions
- `-v` shows you what's happening
- `-z` compresses during transfer
- `--progress` shows a progress bar, useful for anything that'll take more than a few seconds

## Option 3: Globus; for genuinely large datasets (10s of GB or more)

Globus is a web-based transfer service designed for exactly this: moving large research datasets reliably between your machine and HPC storage, with automatic retry if the connection drops. If your dataset is large enough that `rsync` feels impractical, ask your program contact whether Globus endpoints are set up for your allocation; this is worth setting up once rather than fighting large `scp`/`rsync` transfers repeatedly.

## Running your script once the data is there

Once your data is on the Morehouse Supercomputing Facility, you submit jobs to actually process it; this is what the HPC Acclimation sessions (Modules 1–3 in the Day 2–3 schedule) walk through: `idev` for interactive sessions, `sbatch`/Slurm for batch jobs. If you don't code, describe to your AI-powered coding assistant what you want the script to do with your (now-uploaded) dataset, and ask it to write the Slurm submission script for you, explained line by line.

## Common pitfalls

- **Path typos**; double-check the destination path exists before transferring; a typo silently creates a new folder rather than erroring, which can be confusing later.
- **Forgetting to check disk quota**; large transfers can fail partway through if you hit your allocation's storage limit. Check your quota before a big transfer, not after it fails.
- **Transferring, then immediately running a job before the transfer finishes**; for large transfers, confirm the copy is complete (file sizes match) before submitting a job that reads the data.

Next: [Dataset Discovery](dataset-discovery.html), or back to [Day 3](../day-3.html).
