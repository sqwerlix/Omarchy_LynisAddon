# Omarchy Lynis addon

Scan this Omarchy machine with Lynis from **Setup → Security → Lynis**, then choose what to fix.

## Install

`lynis` is required. `arch-audit` adds Arch package advisories to a full scan.

```bash
install -Dm755 bin/omarchy-lynis-scan ~/.local/bin/omarchy-lynis-scan
```

Copy the object in `menu.jsonc` into `~/.config/omarchy/extensions/omarchy-menu.jsonc`. The menu reloads when that file is saved.

You can also run `omarchy-lynis-scan` in a terminal. Scans other than Pentest ask for your sudo password there.

## Scan modes

1. **Quick** — whole system, no pauses
2. **Step through** — whole system, Enter between sections
3. **One area** — authentication, kernel, SSH, firewall, and the other Lynis groups
4. **Pentest** — unprivileged scan
5. **Last report** — open the previous results

## Fixes

After the scan:

- **A** applies every reviewed automatic fix, after showing the list and why the rest stay notes
- **N** applies nothing
- **Y** asks for each one. Inside that prompt, **a** applies the remaining fixes and **q** stops

Automatic fixes are only:

- a package `arch-audit` already has a patched version for
- turning NTP on, when it is off
- enabling ufw, when it is installed but inactive
- removing other-write from a world-writable file under `/etc`
- the reviewed sysctl values, in `/etc/sysctl.d/99-omarchy-lynis.conf`
- blocking `dccp`, `sctp`, `rds`, `tipc`, and firewire storage, in `/etc/modprobe.d/99-omarchy-lynis.conf`
- a short authorized-use notice appended to `/etc/issue`
- `127.0.1.1 <hostname>` in `/etc/hosts` when the hostname is missing
- `* soft core 0` and `* hard core 0` in `/etc/security/limits.d/99-omarchy-lynis.conf`

USB storage, compilers, password aging, kernel-module lockdown, SysRq, IP forwarding, one-way BPF, new scanners or accounting services, and advisories with no patched package stay notes. Choosing A prints the reason for each of those.

Applied actions are logged at `~/.local/state/omarchy-lynis/applied.log`.

## Features

Planned work lives in [Features](Features/). Each item has its own folder. The list started in `bin/plans.md`.
