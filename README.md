# bsdfetch

A simple system information tool written in POSIX `sh`, specifically tailored for BSD operating systems. 

`bsdfetch` is a fork of [pfetch](https://github.com/dylanaraps/pfetch) with all non-BSD operating system support removed. It focuses exclusively on OpenBSD, FreeBSD, NetBSD, and DragonFlyBSD, providing cleaner code and fixing system-specific bugs found in the original script.

## Changes and Fixes

- **BSD Only:** Removed all Linux, macOS, Haiku, Minix, Solaris, IRIX, and SerenityOS code to keep the script minimal and focused.
- **Fixed OpenBSD Memory Detection:** The original `pfetch` incorrectly parsed the 3rd column (`avm` - active virtual memory) of `vmstat`, which often reported values higher than physical RAM due to counting virtual memory. `bsdfetch` now correctly calculates used memory (`active + wired` pages) using `vmstat -s`, matching the real system usage reported by tools like `btop` and `top`.
- **Disk Partition Layout:** Added a new `disk` info module. Unlike the original `pfetch`, `bsdfetch` now properly detects and lists the sizes of all mounted real filesystem partitions (e.g., `/`, `/var`, `/usr`, `/home`), which is especially useful for OpenBSD's default disk layout. It uses `df -Pk` for POSIX compliance across all supported BSDs.
- **Renamed:** The script and internal references have been renamed from `pfetch` to `bsdfetch`.

## Supported Operating Systems

- OpenBSD (Primary target)
- FreeBSD
- NetBSD
- DragonFlyBSD

## Installation

You can easily install `bsdfetch` on your BSD system using `ftp` (or `curl`/`wget` if preferred).

```sh
ftp -o /usr/local/bin/bsdfetch https://raw.githubusercontent.com/Kwakakwakakawa/bsdfetch/refs/heads/main/bsdfetch
chmod +x /usr/local/bin/bsdfetch
