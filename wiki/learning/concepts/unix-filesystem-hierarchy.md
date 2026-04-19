---
type: concept
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Cannon-Linux for Beginners.md
---

# Unix filesystem hierarchy

Parent: [[../index|Learning MOC]]

The conventions that govern what goes where on a Unix/Linux system. Formally standardised as the **Filesystem Hierarchy Standard (FHS)**; in practice, the convention SRE work assumes at all times.

## Top-level layout (Cannon, loc 312)

| Path | Purpose |
|---|---|
| `/` | Root of the hierarchy. *Unrelated* to the `root` user. |
| `/bin` | Essential binaries/executables. |
| `/etc` | System configuration files. |
| `/home` | User home directories. |
| `/opt` | Optional / third-party software. |
| `/tmp` | Temporary space; typically cleared on reboot. |
| `/usr` | User-related programs and libraries. |
| `/var` | Variable data — most importantly, log files. |

Additional paths not captured in Cannon's highlights but load-bearing in practice: `/sbin` (system binaries), `/dev` (device files), `/proc` (kernel/process VFS), `/sys` (sysfs), `/lib` (shared libs), `/boot` (kernel + bootloader), `/root` (root user's home).

## Application-local convention (loc 373)

Applications installed outside the distro's package manager typically mirror `/` under `/usr/local/<app>`:

- `/usr/local/apache/bin` — binaries
- `/usr/local/apache/etc` — config
- `/usr/local/apache/lib` — libraries
- `/usr/local/apache/logs` — logs

This mirroring is why `find /var/log` vs `find /usr/local/*/logs` both produce meaningful output — logs are where *either* the FHS or the app-local convention says they are.

## Why this matters for SRE work

- **Triage speed.** When a service misbehaves, you know to look at `/var/log`, `/etc`, and `/tmp` in that order — not because of a runbook but because of FHS.
- **Observability tool placement.** Agents like `node_exporter` drop in `/usr/local/bin`; their configs in `/etc/<tool>/`; their state in `/var/lib/<tool>/`.
- **Disk alerting.** `/var` filling up is the single most common reason a box "just stops" — logs and databases both live there.

## Related

- [[../books/linux-for-beginners|Linux for Beginners]] — source
- [[unix-file-permissions|Unix file permissions]] — the companion concept
- [[../books/systems-performance|Systems Performance]] (Gregg) — the performance tooling that assumes FHS fluency
- [[../../synthesis/linux-fundamentals-for-sre|Linux fundamentals for SRE]] — bridges to BMS work
