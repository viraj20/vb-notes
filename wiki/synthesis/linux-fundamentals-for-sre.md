---
type: synthesis
domain: synthesis
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Cannon-Linux for Beginners.md
  - sources/learning/books/Kindle Highlights/Gregg-Systems Performance.md
  - sources/learning/books/Kindle Highlights/Murphy_et_al-Site Reliability Engineering.md
---

# Linux fundamentals for SRE

Parent: [[index|Synthesis MOC]]

Bridges [[../learning/index|learning]] (Cannon, Gregg, the SRE canon) and [[../work/index|work]] (BMS systems). A map of what Linux-level knowledge is load-bearing for SRE work.

## The staircase

SRE competence on Linux isn't a flat checklist — it's a staircase, and each step depends on the one below.

### Step 1 — Navigation and file literacy ([[../learning/books/linux-for-beginners|Cannon]])
- [[../learning/concepts/unix-filesystem-hierarchy|FHS]] — know where config, logs, binaries live without having to search.
- [[../learning/concepts/unix-file-permissions|Permissions]] — read `ls -l` fluently; `chmod 600` the muscle memory for SSH keys.
- `less`, `grep`, `find`, `awk`, `xargs` — the CLI vocabulary that turns tickets back into work.

**Failure mode if missing:** tickets that should take 10 minutes become Slack threads.

### Step 2 — Processes, resources, signals (not in Cannon; Gregg territory)
- `ps`, `top`, `htop` — what's running, what's it costing.
- Signals (`SIGTERM`, `SIGKILL`, `SIGHUP`) — how to ask processes to stop, and what happens when they won't.
- File descriptors, ulimits, `/proc` — why the process won't start, why it's leaking.

**Failure mode if missing:** "restart the service" becomes the whole toolbox.

### Step 3 — Observability methodology ([[../learning/books/systems-performance|Gregg]])
- [[../learning/concepts/use-method|USE method]] per resource: utilization, saturation, errors.
- [[../learning/concepts/golden-signals|Golden signals]] per service: latency, traffic, errors, saturation.
- [[../learning/concepts/latency-vs-throughput|Latency vs throughput]] — never average latency; percentiles or you're lying.

**Failure mode if missing:** you chase the wrong thing for the first 30 minutes of an outage.

### Step 4 — The SRE canon ([[../learning/books/site-reliability-engineering|Murphy et al.]])
- [[../learning/concepts/error-budget|Error budgets]] — the SLO contract, how you stop shipping when reliability debt piles up.
- [[../learning/concepts/toil|Toil]] — the work that defeats its own success; eliminate it, don't tolerate it.
- [[../learning/concepts/fault-vs-failure|Fault vs failure]] — what the user sees vs. what the system actually did.

**Failure mode if missing:** heroics replace process; on-call becomes personality-based instead of system-based.

## The transfer to BMS work

Every BMS service sits on Linux. Every production incident eventually terminates in one of:

- "Where is this log?" → [[../learning/concepts/unix-filesystem-hierarchy|FHS]]
- "Why won't this process start?" → [[../learning/concepts/unix-file-permissions|permissions]] / ulimits / disk / memory
- "What's saturated?" → [[../learning/concepts/use-method|USE method]]
- "Is the user experience actually bad?" → [[../learning/concepts/golden-signals|golden signals]]
- "Should we keep shipping?" → [[../learning/concepts/error-budget|error budget]]

This is the spine. Every BMS-specific tool, dashboard, or runbook is a shortcut over this spine; when the shortcut fails, the spine is what you fall back to.

## Bookshelf, shortest-to-longest path

1. [[../learning/books/linux-for-beginners|Linux for Beginners]] (Cannon) — CLI and FHS primer.
2. [[../learning/books/systems-performance|Systems Performance]] (Gregg) — methodology + Linux-specific tooling.
3. [[../learning/books/site-reliability-engineering|Site Reliability Engineering]] (Murphy et al.) — the Google playbook.
4. [[../learning/books/designing-data-intensive-applications|Designing Data-Intensive Applications]] (Kleppmann) — when your services become distributed.
5. [[../learning/books/system-design-interview|System Design Interview]] (Xu) — compact checklist for scaling.

## Related

- [[index|Synthesis MOC]]
- [[sre-practice-for-bms|SRE practice for BMS]] — companion synthesis
- [[../learning/index|Learning MOC]]
- [[../work/index|Work MOC]]
