---
title: API Data Extraction with Your AI Coding Assistant
---

# API Data Extraction with Your AI Coding Assistant

<div class="card">

Two walkthroughs, same skill at two different scales, both using plain-language prompts to your AI coding assistant, no prior coding required, and no terminal: Claude writes the code, you run it by clicking through a Jupyter notebook.

- **Part 1** pulls a small, keyless dataset in a notebook on your laptop, then uploads the result to the Morehouse Supercomputing Facility through your browser (Tapis).
- **Part 2** pulls a much larger, API-key-gated dataset, but runs the extraction directly on the cluster; you run it in a Jupyter notebook launched via the [TAP Analysis Portal](idev-tap-portal.html) rather than downloading it to your laptop first.

That contrast is the point: small data is fine to handle locally and hand off; data at real HPC scale is faster and more reliable to pull straight from the cluster's own connection than to download and re-upload.

</div>

## Part 1: A small dataset, no API key

### The dataset

We're using the CDC's [Behavioral Risk Factor Surveillance System (BRFSS)](https://www.cdc.gov/brfss/data_tools.htm), specifically the "How is your general health?" question, self-reported by state for 2023 (Excellent / Very good / Good / Fair / Poor). It's public, requires no account, no API key, and no sign-up; the API returns plain JSON from a single URL.

### 1. Quick check: can you run a Jupyter notebook?

Ask your AI coding assistant to check for you; there's no need to open a terminal yourself for this, or anything else in this walkthrough:

> *"Check whether I can run a Jupyter notebook in this editor — is Python installed, and is the Jupyter extension set up? If anything's missing, help me through install it."*

Claude can check and install what's needed on its own; you're approving what it does, not typing commands yourself.


### 2. Prompt your AI coding assistant

Open a new chat with Claude (Claude Code extension in your editor) and describe the task in plain language; something like:

> *"I want a Jupyter notebook, not a plain script, that pulls public health survey data from a government API and saves it to a CSV file. Put everything in one cell I can run by clicking the Run button. Don't use any extra installed packages — just Python's built-in libraries. Here's the exact URL to call:*
>
> *`https://data.cdc.gov/resource/dttw-5yxu.json?topic=Overall%20Health&year=2023&break_out=Overall`*
>
> *It returns JSON. The cell should:*
> 1. *Request that URL*
> 2. *Print how many records came back*
> 3. *Save the records to a CSV file called `brfss_general_health_2023.csv`*
> 4. *Print the first 3 rows so I can see what came back*
>
> *Explain what each part does in plain language, like I've never coded before."*

### 3. What you should get back

Claude's code may differ slightly in style from what's below, that's fine; what matters is it hits the same URL and produces the same kind of output. Here's a tested, working version for reference, in case you want to compare or paste it into your notebook cell directly:

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

### 4. Run it and confirm, in the notebook

Open `extract_brfss_data.ipynb` in your editor and click the **Run** button (▶) on the cell. The output prints directly below it:

```
Requesting: https://data.cdc.gov/resource/dttw-5yxu.json?topic=Overall%20Health&year=2023&break_out=Overall
Received 270 rows.
Saved to brfss_general_health_2023.csv

First 3 rows:
  Alaska: Excellent - 15.7%
  Alaska: Very good - 31.5%
  Alaska: Good - 34.4%
```

270 rows is expected: 5 responses (Excellent, Very good, Good, Fair, Poor) across roughly 54 U.S. states and territories. If your row count is way off from that, ask Claude to help you debug straight from the notebook's error output before moving on.

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
<li>Confirmed (via Claude) that Python and Jupyter are ready in your editor</li>
<li>Notebook written (by you and Claude, or copied from above) and run successfully by clicking Run</li>
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

replacing the email with your real address. This is a single automated request; there's no application or approval wait.

<div class="card">

**Verify your email before trying to use the key.** AQS sends a verification email to the address you signed up with; the key doesn't work until you've confirmed it. If your first request fails with an authentication error right after signing up, this is the first thing to check, not your code.

</div>

Keep the email and key handy, you'll need both for every request; Step 5 below has you save them to a file rather than typing them into the notebook itself.

### 2. Prompt your AI coding assistant

Back on your laptop, before heading to TAP, ask Claude to write the notebook (you'll run it on the cluster in Step 6, so write it here where it's easiest to iterate):

> *"I want a Jupyter notebook that pulls hourly ozone data from the EPA's public AQS API and saves it to a CSV file. Use only Python's built-in libraries, no extra installs. Requirements:*
> 1. *Read my email and API key from a text file called `aqs_credentials.txt` sitting in the same folder — line 1 is my email, line 2 is my key. Don't put my key directly in the notebook.*
> 2. *Loop over these states: California (06), Texas (48), New York (36), Illinois (17), Pennsylvania (42), Florida (12)*
> 3. *For each state, request ozone (param 44201) for all of 2023 from `https://aqs.epa.gov/data/api/sampleData/byState`*
> 4. *Include a `TEST_MODE` switch that, when on, only pulls one state and one week, so I can confirm everything works before running the full year across all six states*
> 5. *Print a readable progress message for each state, and a clear error message if a request fails (e.g. bad credentials)*
> 6. *Save everything into one CSV file called `aqs_ozone_2023.csv`, and print the total row count at the end*
>
> *Explain what each part does in plain language, like I've never coded before."*

### 3. What you should get back

A reference version, matching the same request shape and safety features described above:

```python
"""
Downloads hourly ozone (param 44201) sample data for 2023 from the EPA's
AQS API for a list of states, and saves all of it into one CSV file.

Reads your email and API key from a file called aqs_credentials.txt,
which must sit in the same folder as this notebook and contain exactly
two lines:
    your_email@example.com
    YOUR-API-KEY-HERE
"""

import csv
import json
import time
import urllib.error
import urllib.parse
import urllib.request

CREDENTIALS_FILE = "aqs_credentials.txt"


def load_credentials():
    with open(CREDENTIALS_FILE, "r", encoding="utf-8") as file:
        lines = [line.strip() for line in file if line.strip()]

    if len(lines) < 2:
        raise SystemExit(
            f"'{CREDENTIALS_FILE}' should have two lines: your email, "
            "then your API key. Please check the file and try again."
        )

    return lines[0], lines[1]


EMAIL, API_KEY = load_credentials()

# Set this to True for a quick test (one state, one week), or False to pull
# the full request (all six states, all of 2023). Always test with True
# first to confirm your credentials and setup work before running the
# full, much slower pull.
TEST_MODE = True

BASE_URL = "https://aqs.epa.gov/data/api/sampleData/byState"
OUTPUT_FILE = "aqs_ozone_2023.csv"
PARAM = "44201"  # ozone
BDATE = "20230101"

# All six states, with human-readable names for the print-outs.
ALL_STATES = [
    ("06", "California"),
    ("48", "Texas"),
    ("36", "New York"),
    ("17", "Illinois"),
    ("42", "Pennsylvania"),
    ("12", "Florida"),
]

if TEST_MODE:
    EDATE = "20230107"  # just the first week of January
    STATES = ALL_STATES[:1]  # just California, to keep the test fast
else:
    EDATE = "20231231"  # the full year
    STATES = ALL_STATES

PAUSE_SECONDS = 5  # how long to wait between requests


def fetch_state_rows(state_code):
    # Build the query string (everything after the "?" in the URL) from a
    # dictionary of parameters, so we don't have to hand-assemble it.
    query = {
        "email": EMAIL,
        "key": API_KEY,
        "param": PARAM,
        "bdate": BDATE,
        "edate": EDATE,
        "state": state_code,
    }
    url = f"{BASE_URL}?{urllib.parse.urlencode(query)}"

    try:
        with urllib.request.urlopen(url) as response:
            payload = json.loads(response.read())
    except urllib.error.HTTPError as error:
        # The AQS API usually explains what went wrong in the response
        # body (bad email/key, bad parameter, etc.), so show that instead
        # of just the generic "400 Bad Request".
        details = error.read().decode("utf-8", errors="replace")
        raise SystemExit(
            f"Request for state {state_code} failed "
            f"({error.code} {error.reason}):\n{details}"
        )

    # The AQS API wraps the actual rows inside a "Data" field.
    return payload.get("Data", [])


def main():
    total_rows = 0
    writer = None
    csv_file = open(OUTPUT_FILE, "w", newline="", encoding="utf-8")

    try:
        for index, (state_code, state_name) in enumerate(STATES):
            print(f"Requesting {state_name} ({state_code})... this can take a minute or more.")
            rows = fetch_state_rows(state_code)
            print(f"{state_name} ({state_code}): {len(rows)} rows")

            if rows:
                # Create the CSV header the first time we see any real data,
                # using whatever fields the API happens to return.
                if writer is None:
                    fieldnames = list(rows[0].keys())
                    writer = csv.DictWriter(csv_file, fieldnames=fieldnames)
                    writer.writeheader()

                writer.writerows(rows)
                total_rows += len(rows)

            # Pause between requests, but not after the very last one.
            if index < len(STATES) - 1:
                time.sleep(PAUSE_SECONDS)
    finally:
        csv_file.close()

    print(f"\nTotal rows saved: {total_rows}")


main()
```

AQS limits each request to at most one calendar year of data, which is why the loop goes state-by-state rather than requesting multiple years at once. Six states of hourly ozone for a year is already a meaningfully large pull; add more state codes to `ALL_STATES` (or a second `PARAM`, e.g. `88101` for PM2.5) to push it further toward the GB range. With `TEST_MODE = False`, expect the run to take several minutes, not seconds; that's normal.

### 4. Launch a Jupyter session via TAP

Follow [Launching an idev Session on the TAP Analysis Portal](idev-tap-portal.html), with one difference: at the application-selection step, choose **Jupyter** rather than plain `idev` if the portal offers it as a separate option. It runs on the same `idev` mechanism underneath, but drops you straight into a JupyterLab interface in your browser instead of a bare terminal, no command line involved from here on.

<div class="card">

Portal option labels can vary by TACC release; if you only see `idev` listed and no separate Jupyter option, check with your facilitator before falling back to a terminal-based session.

</div>

### 5. Create your credentials file

Still no terminal: in JupyterLab's file browser (the panel on the left), click **New → Text File**, name it `aqs_credentials.txt`, and enter two lines:

```
your_email@example.edu
your_actual_api_key
```

Save it (Ctrl+S / Cmd+S). Keeping the key in its own file, rather than in the notebook, means it never ends up in a cell's saved output if you share the notebook later.

### 6. Create the notebook and test it

1. In JupyterLab, click **New → Notebook**, and paste the script from Step 3 (Claude's version, or the reference one above) into the first cell.
2. Leave `TEST_MODE = True` and click **Run** (▶) on the cell.
3. Confirm you see one state's worth of rows print out, ending with a `Total rows saved` line, and no authentication error. If you do see an authentication error, re-check Step 1's email verification before anything else.

### 7. Run the full pull and confirm

Once the test succeeds, change `TEST_MODE = True` to `TEST_MODE = False` in the cell and click **Run** again. This time it loops all six states and will take a few minutes.

When it finishes, confirm two things without ever opening a terminal:

- The cell's own output ends with a `Total rows saved: N` line.
- In the JupyterLab file browser, `aqs_ozone_2023.csv` appears with a file size shown right next to it; with six states of hourly ozone for a full year, expect this well into the hundreds of MB, and into GB territory if you extended the state list or added a second pollutant.

That's the confirmation: the data made it onto the cluster, at a scale that wouldn't have been practical to pull to your laptop first.

### Part 2 checklist

<ul class="checklist">
<li>AQS API key received by email, and the verification email confirmed</li>
<li>Notebook written (by you and Claude, or copied from above)</li>
<li>Jupyter session launched via the TAP Analysis Portal</li>
<li><code>aqs_credentials.txt</code> created via the JupyterLab file browser (not typed into the notebook)</li>
<li>Test run (<code>TEST_MODE = True</code>) succeeded with no authentication errors</li>
<li>Full run (<code>TEST_MODE = False</code>) complete; <code>aqs_ozone_2023.csv</code> visible in the file browser with a matching row count and file size</li>
</ul>

---

Next: [Moving Data Onto the Morehouse Supercomputing Facility](moving-data-tacc.html), [Launching an idev Session on the TAP Analysis Portal](idev-tap-portal.html), or back to [Day 3](../day-3.html).
