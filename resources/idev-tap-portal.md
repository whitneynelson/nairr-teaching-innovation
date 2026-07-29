---
title: Launching an idev Session on the TAP Analysis Portal
---

# Launching an idev Session on the TAP Analysis Portal

<div class="card">

TAP (the TACC Analysis Portal, at [tap.tacc.utexas.edu](https://tap.tacc.utexas.edu)) is the point-and-click way to get an interactive session on a compute node — the browser equivalent of running `idev` from the command line. No SSH client or terminal commands required; useful for students who aren't comfortable at a command line yet, or as a fallback if a local SSH setup is giving someone trouble.

</div>

## 1. Log in

Go to [tap.tacc.utexas.edu](https://tap.tacc.utexas.edu) and sign in with your TACC username and password, then complete MFA (TACC Token app or a pairing code), the same credentials and MFA flow used everywhere else on the Morehouse Supercomputing Facility.

## 2. Start a new session

From the portal home page, select **Vista** as the system, then choose **New Session**.

## 3. Configure the session

Set:

- **Application:** idev
- **Allocation/Project:** your course or program allocation
- **Queue:** `development` for quick testing (short wait, short time limit); switch to a production queue for longer or heavier work
- **Nodes:** 1 (the default for most classroom exercises)
- **Time:** keep it short (e.g. 01:00:00) for testing — you can always start a new session if you need more time

## 4. Submit and connect

Submit the session. Like any Slurm job, it queues before it runs; the portal shows status as it moves from queued to running. Once it's running, click **Connect** (or **Open Terminal**) to get an interactive shell directly on the compute node — that's the idev session, live in your browser.

## 5. End the session

When you're done, close the session or cancel the job from the portal so the node is released back to the queue for others.

---

Portal labels and layout can shift between TACC releases — if a button name above doesn't match what you see, the underlying flow (log in → select system → configure → connect) still holds.

Next: back to [Additional Resources](../additional-resources.html).
