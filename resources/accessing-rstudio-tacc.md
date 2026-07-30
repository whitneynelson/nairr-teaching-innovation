---
title: Accessing RStudio on the Morehouse Supercomputing Facility
---

# Accessing RStudio on the Morehouse Supercomputing Facility

<div class="card">

RStudio isn't installed on your laptop by default in this program's workflow &mdash; instead, you run it directly on the Morehouse Supercomputing Facility's systems, close to the data and compute. There are two ways to get to it, depending on which system you're on. Start with Option 1 if you want the simplest point-and-click path.

</div>

## Option 1: TAP Portal (Stampede only)

The TACC Analysis Portal ([tap.tacc.utexas.edu](https://tap.tacc.utexas.edu)) can launch RStudio directly in your browser, no SSH client or terminal commands required. **This option is only available on the Stampede system** &mdash; RStudio is not listed as a TAP application on Vista.

1. Go to [tap.tacc.utexas.edu](https://tap.tacc.utexas.edu) and log in with your TACC username and password, then complete MFA.
2. From the portal home page, select **Stampede** as the system, then choose **New Session**.
3. Set:
   - **Application:** RStudio
   - **Allocation/Project:** your course or program allocation
   - **Queue:** `development` for a quick test session
   - **Nodes:** 1
   - **Time:** keep it short (e.g. 01:00:00) for testing
4. Submit the session. Once the job moves from queued to running, click **Connect** &mdash; RStudio opens directly in a browser tab, already logged into a shell on the compute node.
5. When you're done, end the session from the portal so the node is released back to the queue.

This is the best option for students who aren't comfortable at a command line, or as a fallback if a local setup is giving someone trouble &mdash; but it only works on Stampede.

## Option 2: Vista, wrapping RStudio through Python/Jupyter

RStudio isn't available as a TAP application on Vista. The workaround is to launch RStudio Server as a proxied app inside a Jupyter session, using the `jupyter-rsession-proxy` Python package &mdash; Jupyter handles the browser connection, and RStudio runs behind it.

1. Start (or reuse) a Jupyter session on Vista &mdash; via TAP (**Vista** system → **Jupyter** application) or from the terminal after `idev`.
2. In a terminal inside that Jupyter session, create a Python environment with the proxy package and an R installation:

   ```bash
   python3 -m venv rstudio-env
   source rstudio-env/bin/activate
   pip install jupyter-server-proxy jupyter-rsession-proxy
   conda install -c conda-forge r-base
   ```

3. Restart the Jupyter server (or refresh the JupyterLab tab) so it picks up the new proxy extension.
4. From the JupyterLab launcher, look for an **RStudio** tile and click it. JupyterLab opens RStudio in a new browser tab, proxied through the same connection as your Jupyter session &mdash; no separate SSH tunnel or VNC step needed.

This is more setup than Option 1, but it's currently the only way to get RStudio running on Vista rather than Stampede; useful if your work needs Vista's hardware specifically (e.g. GPU-attached notebooks) and you also want an R environment alongside it.

---

Next: back to [Additional Resources](../additional-resources.html).
