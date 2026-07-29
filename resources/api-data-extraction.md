---
title: API Data Extraction with Your AI Coding Assistant
---

# API Data Extraction with Your AI Coding Assistant

<div class="card">

This walks through pulling a real dataset from a public API using plain-language prompts to your AI coding assistant, no prior coding required. By the end you'll have a real data file on your laptop, then moved onto the Morehouse Supercomputing Facility. That file is what the next session (HPC Acclimation, Modules 2–3: launching a Jupyter session via `idev` on the [TAP Analysis Portal](idev-tap-portal.html), submitting it, and reading the output) uses to confirm the extraction worked. No calculations in either session; just extract, move, and confirm.

</div>

## The dataset

We're using the CDC's [Behavioral Risk Factor Surveillance System (BRFSS)](https://www.cdc.gov/brfss/data_tools.htm), specifically the "How is your general health?" question, self-reported by state for 2023 (Excellent / Very good / Good / Fair / Poor). It's public, requires no account, no API key, and no sign-up; the API returns plain JSON from a single URL. That combination — free, keyless, small — is why it's the pick for a first end-to-end walkthrough; other datasets on the accelerator's list (e.g. Census/ACS, EPA AQS) need an API key request first, an extra step worth skipping for this exercise.

## 1. Quick check: is Python installed?

Ask your AI coding assistant to check for you rather than doing this yourself: in your editor's terminal (VS Code or Antigravity), ask Claude:

> *"Check whether Python 3 is installed on my computer, and tell me the version."*

Claude will run `python3 --version` and read you the result.

- **Mac:** this almost always comes back with a version already; it ships with the same Xcode Command Line Tools install that gave you `git`.
- **Windows:** if it's missing, ask Claude: *"Walk me through installing Python 3 on Windows."* It'll point you to [python.org](https://www.python.org/downloads/) and remind you to check "Add python.exe to PATH" during setup, the step people most often miss.

## 2. Prompt your AI coding assistant

Open a new chat with Claude (Claude Code extension in your editor) and describe the task in plain language; something like:

> *"I want a short Python script that pulls public health survey data from a government API and saves it to a CSV file. Don't use any extra installed packages — just Python's built-in libraries. Here's the exact URL to call:*
>
> *`https://data.cdc.gov/resource/dttw-5yxu.json?topic=Overall%20Health&year=2023&break_out=Overall`*
>
> *It returns JSON. Please write a script that:*
> 1. *Requests that URL*
> 2. *Prints how many records came back*
> 3. *Saves the records to a CSV file called `brfss_general_health_2023.csv`*
> 4. *Prints the first 3 rows so I can see what came back*
>
> *Explain what each part of the script does in plain language, like I've never coded before."*

## 3. What you should get back

Claude's script may differ slightly in style from what's below, that's fine; what matters is it hits the same URL and produces the same kind of output. Here's a tested, working version for reference, in case you want to compare or paste it directly:

```python
import csv
import json
import urllib.request

URL = (
    "https://data.cdc.gov/resource/dttw-5yxu.json"
    "?topic=Overall Health&year=2023&break_out=Overall"
).replace(" ", "%20")

OUTPUT_FILE = "brfss_general_health_2023.csv"

print(f"Requesting: {URL}")
with urllib.request.urlopen(URL) as response:
    data = json.loads(response.read().decode())

print(f"Received {len(data)} rows.")

for row in data:
    row.pop("geolocation", None)

fieldnames = []
for row in data:
    for key in row:
        if key not in fieldnames:
            fieldnames.append(key)

with open(OUTPUT_FILE, "w", newline="") as f:
    writer = csv.DictWriter(f, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows(data)

print(f"Saved to {OUTPUT_FILE}")
print("\nFirst 3 rows:")
for row in data[:3]:
    print(f"  {row['locationdesc']}: {row['response']} - {row['data_value']}%")
```

Ask Claude to explain any line you're curious about; that's a better use of the time than trying to memorize the syntax yourself.

## 4. Run it and confirm, locally

Ask Claude to run the script for you, or run it yourself in the terminal:

```bash
python3 extract_brfss_data.py
```

You should see something like:

```
Requesting: https://data.cdc.gov/resource/dttw-5yxu.json?topic=Overall%20Health&year=2023&break_out=Overall
Received 270 rows.
Saved to brfss_general_health_2023.csv

First 3 rows:
  Alaska: Excellent - 15.7%
  Alaska: Very good - 31.5%
  Alaska: Good - 34.4%
```

270 rows is expected: 5 responses (Excellent, Very good, Good, Fair, Poor) across roughly 54 U.S. states and territories. If your row count is way off from that, ask Claude to help you check the URL and try again before moving on.

## 5. Move the file onto the Morehouse Supercomputing Facility

Now that the file exists locally, get it onto the cluster the same way any dataset gets there; see [Moving Data Onto the Morehouse Supercomputing Facility](moving-data-tacc.html) for the full options. For a single small CSV like this one, `scp` is enough:

```bash
scp brfss_general_health_2023.csv username@hpc-system:/path/to/destination/
```

If you're not sure of your username, hostname, or destination path, that's covered in [Connecting to Vista: an SSH guide for every platform](connecting-to-vista-ssh.html).

## 6. Confirm it arrived

SSH in and check the file landed intact:

```bash
ssh username@hpc-system
ls -la /path/to/destination/brfss_general_health_2023.csv
wc -l /path/to/destination/brfss_general_health_2023.csv
```

`wc -l` should report 271 (270 data rows plus the header row); if it doesn't match what you saw locally in Step 4, the transfer may have been interrupted, re-run the `scp` command.

## What's next

With the file confirmed on the cluster, the next session picks up from here: launch an interactive Jupyter session via `idev` on the [TAP Analysis Portal](idev-tap-portal.html), open the notebook, load `brfss_general_health_2023.csv`, and confirm it reads in correctly (row count, column names, a preview) — no calculations, just proving the data made the trip.

## Checklist

<ul class="checklist">
<li>Python 3 confirmed installed (or installed this session)</li>
<li>Extraction script written (by you and Claude, or copied from above) and run successfully</li>
<li><code>brfss_general_health_2023.csv</code> exists locally with 270 data rows</li>
<li>File copied onto the Morehouse Supercomputing Facility via <code>scp</code></li>
<li>Row count on the cluster confirmed to match (271 lines including header)</li>
</ul>

Next: [Moving Data Onto the Morehouse Supercomputing Facility](moving-data-tacc.html), [Launching an idev Session on the TAP Analysis Portal](idev-tap-portal.html), or back to [Day 3](../day-3.html).
