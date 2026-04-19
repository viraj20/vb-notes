---
type: source-summary
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Cannon-Linux for Beginners.md
---

# Linux for Beginners (Cannon)

Parent: [[../index|Learning MOC]]

Jason Cannon's introductory Linux/CLI book. VB captured 16 highlights — mostly reference material: FHS, `ls` flags, chmod octals. This page is a **lookup shortcut**, not a narrative summary.

## What VB captured

### Filesystem hierarchy (loc 312)
See [[../concepts/unix-filesystem-hierarchy|Unix filesystem hierarchy]] for the full table.

Quick reference:
- `/bin` — executables
- `/etc` — config
- `/home` — home dirs
- `/opt` — third-party software
- `/tmp` — temporary, cleared on reboot
- `/usr` — user programs
- `/var` — variable data, most notably log files

For application-local installs, the `/usr/local/<app>/{bin,etc,lib,logs}` convention (loc 373) mirrors the root layout.

### Navigation
- `cd -` — jump to previous directory; equivalent to `cd $OLDPWD` (loc 508–510)
- `man -k KEYWORD` — search the man pages when you don't know the command (loc 484)
- `ls -F` — append type-indicator characters to names (loc 587)
- `ls -ld DIR` — list the directory itself, not its contents (loc 628)
- `tree -d` / `tree -C` — directories-only / colorised (loc 619)
- `less` navigation: Enter=line, Space=page, `g`=top, `G`=bottom (loc 451)

### Permissions (loc 665, 752, 777)
See [[../concepts/unix-file-permissions|Unix file permissions]] for the full treatment.

File type column: `-` regular, `d` directory, `l` symlink.

Octal cheat sheet:
| Octal | Binary | Meaning |
|---|---|---|
| 0 | 000 | --- |
| 1 | 001 | --x |
| 2 | 010 | -w- |
| 4 | 100 | r-- |
| 5 | 101 | r-x |
| 6 | 110 | rw- |
| 7 | 111 | rwx |

`chmod a=r file` sets exactly read-for-all (`=` clears other bits, unlike `+`/`-`).

### Misc
- Escape spaces with `\` (loc 651).
- `~mail` expands to user mail's home dir (loc 297).
- `chgrp GROUP FILE` to change group ownership (loc 830).

## Related

- [[../concepts/unix-filesystem-hierarchy|Unix filesystem hierarchy]] — FHS concept
- [[../concepts/unix-file-permissions|Unix file permissions]] — chmod/chown concept
- [[systems-performance|Systems Performance]] (Gregg) — the next step once basics are fluent
- [[../../synthesis/linux-fundamentals-for-sre|Linux fundamentals for SRE]] — synthesis bridge to BMS work
