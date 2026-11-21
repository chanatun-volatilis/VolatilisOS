# VolatilisOS 2.0 Beta — historical archive

> **Archive preparation; ISO publication pending version verification.** This branch documents the recovered **VolatilisOS V2.0 Beta** generation. The ISO supplied for this archive was inspected and identifies itself as **VolatilisOS 2.1**, so it is **not** published here as V2.0. The correct V2.0 ISO is still needed. **No source code is distributed by this branch.**

**Latest public release:** [VolatilisOS 2.2 Beta, “Navy Horizon”](https://github.com/chanatun-volatilis/VolatilisOS/tree/main)  
**Next historical branch:** [VolatilisOS 2.1](https://github.com/chanatun-volatilis/VolatilisOS/tree/version-2.1)

VolatilisOS is an independently developed, experimental x86 operating-system project written in C and low-level assembly. This historical branch preserves the **2.0 Beta era** separately from the actively developed 2.2 release line.

## What we can verify about V2.0

Two screenshots dated **1 and 5 August 2026** visibly identify the CLI as **“VolatilisOS v2.0”**. In these images:

- The shell identifies itself as **vsh 2.0**, with multiple workspaces, command history and redirection/pipes.
- The screen shows an **80×25 VGA text interface**, an i386 protected-mode kernel and `vfetch` hardware/system information.
- The reported root filesystem is **VLFS2** on `/dev/ata0p1`. On-screen notes also describe a **VFS** routing paths to filesystems, `/dev` and `/proc`.
- A built-in **C interpreter**, command-line tools, an interactive text editor and a prototype `install` command are described or shown.
- The boot description mentions a **custom bootloader and GRUB**.

The existence of an installer command does **not** establish that V2.0 can safely install to a real computer. Treat all installation/disk writes as **experimental and unverified**. These are screenshot-grounded observations, not a fresh V2.0 source build or automated test report.

## ISO download

**Not yet available for V2.0 Beta on this branch.** The provided file `volatilis-master.iso` was checked against the accompanying `VOS V2.1 Beta.zip` and found to be byte-identical. Its GRUB menu labels the kernels *VolatilisOS v2.1 GUI Edition* and *VolatilisOS v2.1 CLI Edition*. Publishing it here as V2.0 would mislabel the release.

When a matching V2.0 ISO is provided, this section can list its actual filename, size, SHA-256 checksum, verified boot-menu label and a safe QEMU boot command. **No source archive or development files will be included.**

## August 2026 snapshots

The supplied **Volatilis gallery** includes August 2026 captures. The intended *single desktop image* is:

**Desktop candidate:** `Screenshot 2569-08-09 at 15.10.41.png` — blue desktop, launcher, file manager, calculator and image windows. It is dated August, but its precise version is **not independently proven**, so it should be captioned “August 2026 desktop-era snapshot,” not claimed to show a verified V2.0 ISO.

**CLI candidates:**
- `Screenshot 2569-08-01 at 15.05.26.png` — clearly displays “VolatilisOS v2.0,” `vfetch`, the editor and a V2.0 feature summary.
- `Screenshot 2569-08-05 at 15.15.51.png` — clearly displays “VolatilisOS v2.0,” command help, workspaces, directory listing and memory information.

These original image files have been **selected for inclusion but have not yet been uploaded** to this branch. The archive will embed exactly one August desktop candidate and up to two of the verified V2.0 text snapshots once binary asset upload is available. Do not use 2.1/2.2 screenshots as V2.0 proof. See [snapshot provenance](docs/SCREENSHOT_PROVENANCE.md).

## Running historical builds

For the correct ISO, the conservative first test is a **fresh BIOS-mode QEMU guest with no host disks attached**:

```sh
# Replace this placeholder with the filename of a *verified* V2.0 ISO.
qemu-system-i386 -m 512 -cdrom VERIFIED_VOLATILIS_2_0_BETA.iso -boot d
```

This is an example for a future verified file, **not** a link to a build already available. Do not boot or install to physical storage as part of testing this archive.

## Documentation

- [V2.0 evidence and version-identification notes](docs/RELEASE_EVIDENCE.md)
- [Snapshot selection and provenance](docs/SCREENSHOT_PROVENANCE.md)
- [Commands and safety](docs/COMMANDS_AND_SAFETY.md)

## Source and licensing

**No kernel source, VScript compiler source, private development tree, or V2.1 source archive is included in this release branch.** The source repository is separate and private. Copyright (C) 2025–2026 Chanatun Volatilis Poolcharuansin. All rights reserved, subject to applicable third-party licenses. This historical documentation is not a license grant to redistribute the OS source.
