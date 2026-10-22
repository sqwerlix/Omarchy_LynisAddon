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

- **A** applies every automatic fix, after showing the list
- **N** applies nothing
- **Y** asks for each one. Inside that prompt, **a** applies the rest and **q** stops

Automatic fixes are only:

- a package `arch-audit` already has a patched version for
- turning NTP on, when it is off
- enabling ufw, when it is installed but inactive
- removing other-write from a world-writable file under `/etc`

Other Lynis findings are printed as notes and left unchanged. That includes SSH settings, sysctls, and package advisories that do not have a patched package yet.

Applied actions are logged at `~/.local/state/omarchy-lynis/applied.log`.
