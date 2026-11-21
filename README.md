# VolatilisOS

**VolatilisOS** is an independently developed, experimental **32-bit x86 operating system** with two bootable editions: a graphical desktop (**GUI**) and a text-first command environment (**CLI**). The project began when I was 12, out of an interest in low-level programming, kernels and operating systems.

The current **published download line** is **VolatilisOS 2.2 Beta — “Navy Horizon”**. Development continues separately in the source repository. **The ISO files here are prebuilt snapshots; they do not update automatically when the source code changes.**

| | |
| --- | --- |
| **Published version** | 2.2 Beta — *Navy Horizon* |
| **Editions** | GUI, CLI, and a master ISO containing both |
| **CPU architecture** | 32-bit x86 / i686 |
| **Recommended first boot** | QEMU or a legacy-BIOS virtual machine |
| **Release readiness** | Experimental/beta; **not certified safe for installation on real-user disks** |
| **Development source** | [VolatilisOS-source-code](https://github.com/chanatun-volatilis/VolatilisOS-source-code) (currently private) |

**Current technical status:** [What works and what's unfinished](docs/CURRENT_STATUS.md) · [Architecture](docs/ARCHITECTURE.md) · [Build and test](docs/BUILD_AND_TEST.md) · [Download & installation safety](docs/RELEASE_AND_SAFETY.md)

Development-source status on these pages was reviewed **21 November 2026**, against commit `9b69ff2ba24901ed98d040f205882a7d3fd5868c`. It describes the source tree, **not guaranteed features of every uploaded binary**.

![A full workspace: Text Editor, Terminal, System Monitor and the desktop folder menu all open at once](screenshots/system-monitor-and-terminal.png)
*A graphical VolatilisOS desktop with Text Editor, Terminal, System Monitor and the folder menu.*

## Download — 2.2 Beta “Navy Horizon”

These files are present in this public repository. Choose the edition you want:

| Download | Description | Approximate size |
| --- | --- | --- |
| [`volatilis-gui.iso`](volatilis-gui.iso) | Standalone graphical desktop | 44 MB |
| [`volatilis-cli.iso`](volatilis-cli.iso) | Standalone text-first edition | 10 MB |
| [`volatilis-master.iso.zip`](volatilis-master.iso.zip) | Both editions with a GRUB selection menu and installer paths; **unzip before booting** | 66 MB ZIP, about 128 MB uncompressed |

**Published SHA-256 checksums** (copied from the existing release README; **not independently rehashed during this documentation update**):

```text
9aa0dc8badd7a3eb209b762fe23a4f183d8bda6010aba0c7f12da6f3b71612b5  volatilis-gui.iso
61c319ccdfc1813f437bc995e2c0cff74955ac1ea092c14778d8f4680d41817a  volatilis-cli.iso
71a2f3a9aaa3c88b476715db220e969fda5efc7e9c12e5b61d1d62698cb351d5  volatilis-master.iso.zip
b08f9500ae44a19022802d6476edf847b3bd8566fbeb527e233598543bd7ae94  volatilis.iso (inside ZIP)
```

To calculate a downloaded file's checksum, use `sha256sum <filename>` on Linux or `shasum -a 256 <filename>` on macOS and compare it with the corresponding published value. A checksum is **not** a digital signature.

**Older release:** VolatilisOS 2.1 (without the newer installer flow) is archived on the [`version-2.1` branch](https://github.com/chanatun-volatilis/VolatilisOS/tree/version-2.1).

## Run it safely

The simplest test is an **isolated QEMU virtual machine**:

```sh
# In the directory containing the downloaded images:
qemu-system-i386 -m 1024 -cdrom volatilis-gui.iso -boot d
qemu-system-i386 -m 512  -cdrom volatilis-cli.iso -boot d

# Master edition selection menu:
unzip volatilis-master.iso.zip
qemu-system-i386 -m 1024 -cdrom volatilis.iso -boot d
```

The commands above do not attach a host hard drive. In VirtualBox, start with an “Other / Unknown” 32-bit guest, **BIOS firmware**, one CPU, and 1 GB RAM. If you want to explore the installer, use a **new disposable virtual disk**, never a drive holding important data. Please read [installation and release-safety guidance](docs/RELEASE_AND_SAFETY.md) first.

## What's in VolatilisOS 2.2 Beta

The 2.2 *Navy Horizon* release description includes a GRUB edition-selection menu, redesigned boot splash, windowed installer, Settings app, sign-in/lock screens, system tools, updated file manager and graphical applications.

The **current source tree** also contains a substantially expanded architecture:

- **Two separate kernels:** GUI and CLI build/boot independently, sharing selected components and versioned userspace interfaces.
- **System software:** scheduling, ELF programs, file descriptors, VScript, C/C++ toolchain/SDK work, VPK packages and a selection of third-party ports.
- **Storage:** VFS, VLFS2, FAT read/write, read-only ext-family/exFAT/NTFS adapters, BIOS installer workflows and QEMU storage safety tests.
- **Graphics and applications:** desktop compositor, text editor, system utilities, media/image viewers, scalable rendering/font work, package-supported NetSurf browser and DoomGeneric/Freedoom.
- **Networking and devices:** IPv4/IPv6, TCP/UDP, DNS, TLS, Ethernet and several virtual hardware drivers.

**Not finished / not certified:** Wi-Fi cannot currently scan or join networks using the implemented radio driver; UEFI installation and Secure Boot are unsupported; broad real-GPU acceleration and SMP are not implemented; installer safety on physical drives has not been certified. Some library/port features are partial, and hardware-specific behavior varies. See the [status matrix](docs/CURRENT_STATUS.md) for evidence and limits.

## Screenshots

These pictures show the **published GUI build** and its desktop applications. They are not proof that a newer source change is present in the downloadable ISO.

### Desktop and menus

| | |
| --- | --- |
| ![Right-click folder menu on the desktop](screenshots/desktop-folder-menu.png) Right-click a desktop folder menu | ![Start menu with Applications](screenshots/start-menu-applications.png) Applications in the launcher |

### Settings and file management

| | |
| --- | --- |
| ![Settings overview](screenshots/settings-overview.png) Settings overview | ![Storage settings and folder menu](screenshots/storage-settings-and-folder-menu.png) Storage settings and the folder menu |

### Files and system monitor

| | |
| --- | --- |
| ![Files and System Monitor](screenshots/files-and-system-monitor.png) Files and System Monitor | ![System Monitor and terminal](screenshots/text-editor-terminal-and-start-menu.png) Launcher, Text Editor and Terminal |

### Text editor and terminal

| | |
| --- | --- |
| ![Text Editor](screenshots/text-editor.png) Tabbed Text Editor with syntax highlighting | ![Terminal running vfetch](screenshots/terminal-vfetch-and-folder-menu.png) Terminal with `vfetch` and `meminfo` |

## Source code and documentation

The authoritative development source is maintained in [`VolatilisOS-source-code`](https://github.com/chanatun-volatilis/VolatilisOS-source-code). It is **currently private**: a GitHub 404 is possible if you do not have access. This public repository is for distributable images, screenshots and user-facing documentation.

The old single-file `src/desktop.c`-style source layout is outdated. Current code has `kernel/core/`, `kernel/services/`, `drivers/`, `graphics/`, `filesystem/`, `networking/`, `userspace/` and `vscript/`. Read the [architecture overview](docs/ARCHITECTURE.md) before following historical build instructions.

## Project links

- [Volatilis on TikTok](https://www.tiktok.com/@alpha300332)
- [Volatilis on itch.io](https://volatilis-2033.itch.io/)

## Copyright and licensing

The source repository states **Copyright (C) 2025–2026 Chanatun Volatilis Poolcharuansin. All rights reserved.** This public repository has no root `LICENSE` file as of this documentation update. **Do not assume the VolatilisOS source is MIT-licensed or freely redistributable.** Third-party ports, fonts, tools and packaged assets have their own license terms; consult their notices. Being able to download an ISO is not a blanket license to redistribute its constituent code.
