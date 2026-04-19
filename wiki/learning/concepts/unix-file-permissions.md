---
type: concept
domain: learning
status: draft
created: 2026-04-19
updated: 2026-04-19
sources:
  - sources/learning/books/Kindle Highlights/Cannon-Linux for Beginners.md
---

# Unix file permissions

Parent: [[../index|Learning MOC]]

The Unix discretionary-access model: every file has an owner, a group, and three triplets of read/write/execute bits (for owner, group, and others).

## The `ls -l` first column (Cannon loc 665)

The leading character is the file type, not a permission:

- `-` regular file
- `d` directory
- `l` symbolic link
- (others not in the highlights: `c` char device, `b` block device, `s` socket, `p` named pipe)

Followed by nine permission bits in three triplets: `rwxrwxrwx` → owner / group / other.

## Octal encoding (loc 777)

Each triplet is a 3-bit number:

| Octal | Binary | rwx | Meaning |
|---|---|---|---|
| 0 | 000 | --- | No permissions |
| 1 | 001 | --x | Execute only |
| 2 | 010 | -w- | Write only |
| 3 | 011 | -wx | Write and execute |
| 4 | 100 | r-- | Read only |
| 5 | 101 | r-x | Read and execute |
| 6 | 110 | rw- | Read and write |
| 7 | 111 | rwx | Full |

So `chmod 644 file` = `rw-r--r--` (owner rw, group/other r). `chmod 755 dir` = `rwxr-xr-x`. `chmod 600 id_rsa` = `rw-------` (the SSH convention).

## Symbolic modes and the `=` gotcha (loc 752)

`+` adds a bit, `-` removes, `=` sets exactly:

- `chmod u+x file` — add execute for user
- `chmod a=r file` — set exactly read for all, clearing existing write/execute
- `chmod go-w file` — remove write from group and other

The `=` form is the dangerous one: it clears bits you didn't mention.

## Group ownership

- `chgrp GROUP FILE` — change group (loc 830)
- `chown USER:GROUP FILE` — change owner and group (not in the highlights but standard)
- Files created in a directory with the setgid bit (`chmod g+s`) inherit the directory's group — useful for shared project directories.

## Why this matters for SRE work

- **"Permission denied" is the single most common first-hour symptom.** Reading `ls -l` fluently turns a ticket back into work.
- **Secret material.** SSH keys (`600`), service-account credentials (`400` or `600`), TLS private keys (`600`) — wrong perms either break the service or leak the secret. Both fail detectable.
- **Runbooks that `sudo chmod 777` are wrong.** It's almost always a group or owner issue, not a permission-breadth issue.
- **Systemd unit files in `/etc/systemd/system/`** (usually `644`) and their drop-ins are a frequent "why won't it pick up my change" culprit.

## Related

- [[../books/linux-for-beginners|Linux for Beginners]] — source
- [[unix-filesystem-hierarchy|Unix filesystem hierarchy]] — companion concept
- [[../../synthesis/linux-fundamentals-for-sre|Linux fundamentals for SRE]] — bridges to BMS work
