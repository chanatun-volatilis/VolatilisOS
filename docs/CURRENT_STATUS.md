# VolatilisOS development status

**Status snapshot:** 21 November 2026  
**Release line:** VolatilisOS **2.2 Beta — “Navy Horizon”**  
**Source reference:** `chanatun-volatilis/VolatilisOS-source-code` `main` at `9b69ff2ba24901ed98d040f205882a7d3fd5868c`  
**Scope:** A documentation review of the source and its test/release notes, **not** a fresh build, VM run, or physical-hardware certification.

> **Published ISOs:** the GUI, CLI and master ISOs in this repository were rebuilt on 22 November 2026 from source commit `34ee203abceef20a25a5e45f52ed1ae16f2500e1` and boot to the desktop / shell in QEMU. The table below was written against the slightly older `9b69ff2` review, plus the additions listed in the [README](../README.md#whats-new-in-the-22-november-2026-build).

> **Important distinction:** This public repository distributes prebuilt ISO files and screenshots. The separately maintained source repository is currently private. Its development status can move ahead of the prebuilt ISOs here. A capability described below is **not automatically guaranteed** to be present in the binary downloads; rebuild or verify the particular artifact to establish that.

## What exists today

| Area | Source-tree status | Caveat |
| --- | --- | --- |
| Core architecture | Two independently bootable 32-bit x86 GUI/CLI kernels; core mechanisms, services, userspace, versioned syscall ABI | One CPU is used; this is not x86_64 or an SMP kernel. Services are still privileged/ring 0, **not** a microkernel |
| Desktop | Native GUI, window management, compositing, Settings, Files, Terminal, Text Editor, many built-in utilities | Feature coverage varies by boot edition and graphics device |
| CLI | Text-first shell, commands, storage and recovery tooling | Different kernel from the GUI edition; not merely a launch option within one shared kernel |
| Storage | VFS, VLFS2, FAT16/FAT32 read/write, partition discovery and block-device layer | VLFS2 newly installed volumes may lack a journal until enabled; use throwaway disks for testing |
| Filesystem readers | ext2/3/4, exFAT, NTFS and ISO 9660 (`.iso` images) read-only paths | Do **not** rely on write support; filesystem and file-size limits apply |
| Disk interfaces | IDE/ATA, AHCI, NVMe, USB xHCI Bulk-Only mass storage and removable-media compatibility |
| USB input | USB keyboards and mice on xHCI and EHCI (USB 2.0) controllers, including devices behind USB hubs and combined keyboard-and-mouse receivers | Real-laptop coverage is limited; some controllers and receivers may still not work | Coverage is hardware-specific; QEMU verification does not certify real controllers |
| Install and recovery | BIOS installed-disk flow, GUI Setup and CLI installer, disk checks, two-edition boot, file persistence in QEMU | **Not certified safe for real-user disks**; UEFI installation is gated off |
| UEFI | IA32 and x64 UEFI live-boot paths have OVMF/QEMU evidence | UEFI **installation** unavailable; Secure Boot not supported |
| Networking | IPv4/IPv6, ARP, DHCP, DNS, TCP/UDP, socket and TLS implementations; multiple Ethernet drivers | Networking features are incremental; no claim of support for arbitrary physical NICs |
| Wi-Fi | Network manager, UI, security groundwork and early chipset-driver work | **Cannot currently scan/join Wi-Fi networks with the implemented hardware support** |
| Applications | Built-in editor/system tools; package-supported NetSurf browser; DoomGeneric/Freedoom and other ports | Port packaging, device support and runtime completeness vary; Doom audio and saves remain open |
| Development tooling | VScript compiler/interpreter, C/C++ components, native SDK, VPK packages, third-party port recipes | Not full compatibility with desktop Linux apps or their dependencies |
| Testing | Host check matrix, QEMU boot/installed-media checks, failure injection, release evidence tools | Tests are not re-run by this page; current checkout must produce its own results |

## Boot and release readiness

Source documentation distinguishes **working emulator paths** from **verified physical hardware**. It describes BIOS/GRUB boot and disk-only BIOS installation in QEMU, and both UEFI loader variants in OVMF. An installed UEFI disk is **not** a supported installation workflow. Secure Boot is **off/unsupported**.

The source release gate reports one of:

- **NO-GO:** required evidence is missing, blocked, failed, stale or skipped;
- **PRERELEASE (VM ONLY):** required checks pass but physical hardware certification is missing or gated hardware issues remain;
- **RELEASE CANDIDATE:** required checks and real-machine preflight evidence exist, with no remaining hardware-gated defects.

This document does **not** state that the current public ISO has passed all those checks. No fresh release-gate report was generated during this update.

## Important known limitations from the source release ledger

- **RG-1:** Fresh installed VLFS2 volumes are created without journaling by default.
- **RG-3:** Installation to, and boot from, a USB stick have not been verified.
- **RG-5:** A GPT disk extending beyond driver reachability can be reported as invalid rather than partly inaccessible; the installer refuses unsafe use.
- **RG-6:** Read-only NVMe devices may be presented as writable before the write is rejected.
- **RG-12:** The GUI's removable-file size display can show a negative size for files of 2 GiB or more.
- **RG-17:** A real-machine BIOS installed-boot reset remained under investigation after stage-2 loader fixes, pending a new physical retest.

These are **documented source-development issues**, not a claim that each is reproducible in the public prebuilt ISO files. No defect is considered fixed just because a patch prompt exists.

## Links and status sources

- [Public release README](../README.md) and [download/safety guide](RELEASE_AND_SAFETY.md)
- [Architecture overview](ARCHITECTURE.md)
- [Build, testing and contributor entry points](BUILD_AND_TEST.md)
- [Source repository](https://github.com/chanatun-volatilis/VolatilisOS-source-code) (access currently restricted)
- Source references for maintainers: `docs/RELEASE_GATE.md`, `docs/STORAGE_RELEASE_NOTES.md`, `docs/WIFI.md`, `docs/UEFI_BOOT_MATRIX.md`, `docs/USB_STORAGE_MATRIX.md`, and `docs/DOOM_PORT.md`.

**Please treat these status descriptions as versioned documentation, not a live capability detector.**
