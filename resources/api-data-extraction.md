---
title: API Data Extraction with Your AI Coding Assistant
---

# API Data Extraction with Your AI Coding Assistant

<div class="card">

Two walkthroughs, same skill at two different scales, both using plain-language prompts to your AI coding assistant, no prior coding required.

- **Part 1** pulls a small, keyless dataset on your laptop, then uploads it to the Morehouse Supercomputing Facility through your browser (Tapis).
- **Part 2** pulls a much larger, API-key-gated dataset, but runs the extraction directly on the cluster; you paste the script into an interactive `idev` session on the [TAP Analysis Portal](idev-tap-portal.html) rather than downloading it to your laptop first.

That contrast is the point: small data is fine to handle locally and hand off; data at real HPC scale is faster and more reliable to pull straight from the cluster's own connection than to download and re-upload.

</div>

## Part 1: A small dataset, no API key

### The dataset

We're using the CDC's [Behavioral Risk Factor Surveillance System (BRFSS)](https://www.cdc.gov/brfss/data_tools.htm), specifically the "How is your general health?" question, self-reported by state for 2023 (Excellent / Very good / Good / Fair / Poor). It's public, requires no account, no API key, and no sign-up; the API returns plain JSON from a single URL.

### 1. Quick check: is Python installed?

Ask your AI coding assistant to check for you rather than doing this yourself: in your editor's terminal (VS Code or Antigravity), ask Claude:

> *"Check whether Python 3 is installed on my computer, and tell me the version."*

Claude will run `python3 --version` and read you the result.

- **Mac:** this almost always comes back with a version already; it ships with the same Xcode Command Line Tools install that gave you `git`.
- **Windows:** if it's missing, ask Claude: *"Walk me through installing Python 3 on Windows."* It'll point you to [python.org](https://www.python.org/downloads/) and remind you to check "Add python.exe to PATH" during setup, the step people most often miss.

### 2. Prompt your AI coding assistant

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

### 3. What you should get back

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

### 4. Run it and confirm, locally

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

### 5. Upload the file via TAPIS

The file is small, so skip the terminal entirely and upload it straight from your browser using the Tapis portal already covered in [Accessing the Morehouse Supercomputing Facility via TAPIS](accessing-tapis.html):

1. Go to [morehouse.tapis.io/#/login](https://morehouse.tapis.io/#/login) and log in with your TACC username and password (Tapis won't prompt for MFA at this step).
2. On the dashboard, select **Systems** in the left panel, then choose **vista** from the Public Systems list.
3. If you haven't already authenticated, click **Authenticate with TMS Keys** on the Vista system card; Tapis creates and manages the SSH keypair for you, no manual setup needed. A green check confirms it worked.
4. Click **Go to $HOME** on the Vista system card to open your file browser on Vista.
5. Use the upload control in the file browser toolbar (look for an upload/add-file icon) to select `brfss_general_health_2023.csv` from your computer and upload it into your home directory, or a subfolder you've created for this exercise.

<div class="card">

The file browser's exact button labels can shift slightly between Tapis releases; if something doesn't match exactly what's described here, the flow (log in → Systems → vista → authenticate → $HOME → upload) still holds.

</div>

Refresh the file listing and confirm `brfss_general_health_2023.csv` appears with a non-zero file size, a few KB, roughly matching what you saw locally. That's your confirmation for Part 1; no SSH, no terminal on the cluster side needed.

### Part 1 checklist

<ul class="checklist">
<li>Python 3 confirmed installed (or installed this session)</li>
<li>Extraction script written (by you and Claude, or copied from above) and run successfully</li>
<li><code>brfss_general_health_2023.csv</code> exists locally with 270 data rows</li>
<li>Logged into <a href="https://morehouse.tapis.io/#/login">morehouse.tapis.io</a> and authenticated Vista with TMS Keys</li>
<li>File uploaded and visible in the Vista file browser with a matching file size</li>
</ul>

---

## Part 2: A larger dataset, with an API key, run on the cluster

### The dataset

This time we're pulling from the EPA's [Air Quality System (AQS) API](https://www.epa.gov/outdoor-air-quality-data): hourly ozone readings across several states for a full year. Unlike BRFSS, this needs a (free, instant) API key, and it's genuinely large; hourly readings from every monitor in even a handful of states for a year adds up fast. That size is exactly why this one runs on the cluster instead of your laptop: faster network, more disk, and no multi-hour download sitting on your home Wi-Fi.

### 1. Get a free API key

In your browser, go to:

```
https://aqs.epa.gov/data/api/signup?email=YOUR_EMAIL@example.edu
```

replacing the email with your real address. This is a single automated request; there's no application or approval wait. Your API key arrives by email within a few minutes. Keep the email and key handy, you'll need both for every request.

### 2. Prompt your AI coding assistant

Back on your laptop, before heading to TAP, ask Claude to write the script (you'll paste it into the cluster terminal in Step 4, so write it here where it's easiest to iterate):

> *"I want a Python script that pulls hourly air quality data from the EPA's public AQS API and saves it to a CSV file. Use only Python's built-in libraries, no extra installs. My email and API key will be set as environment variables called `AQS_EMAIL` and `AQS_KEY` — don't hardcode them in the script. The script should:*
> 1. *Loop over this list of state FIPS codes: `06` (California), `48` (Texas), `36` (New York), `17` (Illinois), `42` (Pennsylvania), `12` (Florida)*
> 2. *For each state, call `https://aqs.epa.gov/data/api/sampleData/byState` with `param=44201` (ozone), `bdate=20230101`, `edate=20231231`, plus my email, key, and the state code*
> 3. *Print how many rows came back for each state as it goes*
> 4. *Append every state's rows into a single CSV file called `aqs_ozone_2023.csv`*
> 5. *Wait a few seconds between requests so I'm not hammering a shared public API*
> 6. *At the end, print the total row count*
>
> *Explain what each part does in plain language, like I've never coded before."*

### 3. What you should get back

A reference version, matching the same request shape and parameters used above:

```python
import csv
import json
import os
import time
import urllib.request

EMAIL = os.environ["AQS_EMAIL"]
KEY = os.environ["AQS_KEY"]

PARAM = "44201"  # Ozone
YEAR = "2023"
STATES = ["06", "48", "36", "17", "42", "12"]  # CA, TX, NY, IL, PA, FL

OUTPUT_FILE = "aqs_ozone_2023.csv"

writer = None
total_rows = 0

with open(OUTPUT_FILE, "w", newline="") as out:
    for state in STATES:
        url = (
            "https://aqs.epa.gov/data/api/sampleData/byState"
            f"?email={EMAIL}&key={KEY}&param={PARAM}"
            f"&bdate={YEAR}0101&edate={YEAR}1231&state={state}"
        )
        print(f"Requesting state {state}...")
        with urllib.request.urlopen(url) as response:
            payload = json.loads(response.read().decode())

        rows = payload.get("Data", [])
        print(f"  {len(rows)} rows for state {state}")

        if rows:
            if writer is None:
                writer = csv.DictWriter(out, fieldnames=list(rows[0].keys()))
                writer.writeheader()
            writer.writerows(rows)
            total_rows += len(rows)

        time.sleep(5)  # be polite to a shared public API

print(f"\nDone. {total_rows} total rows saved to {OUTPUT_FILE}")
```

<div class="card">

I verified the AQS API is live and confirmed its exact parameter names and signup mechanism against the real service. I did not run this specific script end-to-end (that requires a real API key tied to an email, which isn't something to generate on your behalf) — pilot it yourself before handing it to a room of non-coders, the same way you'd check any new exercise.

</div>

AQS limits each request to at most one calendar year of data, which is why the script loops state-by-state rather than requesting multiple years at once. Six states of hourly ozone for a year is already a meaningfully large pull; add more state codes to the list (or add a second `PARAM`, e.g. `88101` for PM2.5) to push it further toward the GB range. Expect the run to take a few minutes, not seconds; that's normal.

### 4. Launch an idev session and paste in the script

1. Follow [Launching an idev Session on the TAP Analysis Portal](idev-tap-portal.html) to get a terminal running on a Vista compute node.
2. Once connected, check Python is available: `python3 --version`. If it's not found, try `module load python3` (module names can vary by system; check `module avail python` or ask your facilitator if that doesn't work).
3. Set your API credentials as environment variables, replacing the placeholders with your real values:
   ```bash
   export AQS_EMAIL="your_email@example.edu"
   export AQS_KEY="your_actual_key"
   ```
4. Open a terminal text editor and create the script file:
   ```bash
   nano extract_aqs_data.py
   ```
5. Paste in the script from Step 3 (Claude's version, or the reference one above), then save and exit (`Ctrl+O`, Enter, `Ctrl+X` in nano).

### 5. Run it and confirm, on the cluster

```bash
python3 extract_aqs_data.py
```

Once it finishes, confirm the file landed and check its size:

```bash
ls -lh aqs_ozone_2023.csv
wc -l aqs_ozone_2023.csv
```

`wc -l` should roughly match the total row count the script printed, plus 1 for the header row. `ls -lh` shows the file size in human-readable form (K/M/G); with six states of hourly ozone for a full year, expect this well into the hundreds of MB, and into GB territory if you extended the state list or added a second pollutant. That confirms the extraction: the data made it onto the cluster, at a scale that wouldn't have been practical to pull to your laptop first.

### Part 2 checklist

<ul class="checklist">
<li>AQS API key received by email</li>
<li>Extraction script written (by you and Claude, or copied from above)</li>
<li>idev session launched via the TAP Analysis Portal</li>
<li>Environment variables set, script pasted into a file, and run on the compute node</li>
<li><code>aqs_ozone_2023.csv</code> exists on the cluster; file size and row count confirmed</li>
</ul>

---

Next: [Moving Data Onto the Morehouse Supercomputing Facility](moving-data-tacc.html), [Launching an idev Session on the TAP Analysis Portal](idev-tap-portal.html), or back to [Day 3](../day-3.html).
