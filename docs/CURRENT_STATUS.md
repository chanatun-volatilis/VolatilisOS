# VolatilisOS development status

**Status snapshot:** 24 November 2026
**Release line:** VolatilisOS **2.2 Beta — “Navy Horizon”**
**Source reference:** `chanatun-volatilis/VolatilisOS-source-code` `main` at `549e6d454157675664eeb416975f50d8742b29f4`
**Scope:** Fresh source build plus host and QEMU verification for the uploaded images; **not** physical-hardware certification.

> **Published ISOs:** the GUI, CLI and master ISOs in this repository were rebuilt on 24 November 2026 from source commit `549e6d454157675664eeb416975f50d8742b29f4`. The exact master image booted its GUI, CLI and command-line installer menu entries in QEMU; both standalone editions also passed framebuffer smoke checks.

> **Important distinction:** This public repository distributes prebuilt ISO files and screenshots. The separately maintained source repository is currently private. Its development status can move ahead of the prebuilt ISOs here. A capability described below is **not automatically guaranteed** to be present in the binary downloads; rebuild or verify the particular artifact to establish that.

## What exists today

| Area | Source-tree status | Caveat |
| --- | --- | --- |
| Core architecture | Two independently bootable 32-bit x86 GUI/CLI kernels; core mechanisms, services, userspace, versioned syscall ABI | One CPU is used; this is not x86_64 or an SMP kernel. Services are still privileged/ring 0, **not** a microkernel |
| Desktop | Native GUI, window management, compositing, Settings, Files, Terminal, Text Editor, many built-in utilities | Feature coverage varies by boot edition and graphics device |
| CLI | Text-first shell, commands, storage and recovery tooling | Different kernel from the GUI edition; not merely a launch option within one shared kernel |
| Storage | VFS, VLFS2, FAT16/FAT32 read/write, partition discovery and block-device layer | VLFS2 newly installed volumes may lack a journal until enabled; use throwaway disks for testing |
| Filesystem readers | ext2/3/4, exFAT, NTFS and ISO 9660 (`.iso` images) read-only paths | Do **not** rely on write support; filesystem and file-size limits apply |
| Disk interfaces | IDE/ATA, AHCI, NVMe, USB xHCI Bulk-Only mass storage and removable-media compatibility | Device support and capacity limits are driver-specific |
| USB input | USB keyboards and mice on xHCI and EHCI (USB 2.0), PS/2 mice and Synaptics packet handling; post-USB i8042 resynchronization protects installed boots | Real-laptop coverage is limited; UHCI/OHCI and unusual receivers may still need firmware compatibility paths |
| Install and recovery | BIOS installed-disk flow, GUI Setup, `vos-install --cli`, MBR/GPT inspection, alongside/erase plans, checks and boot repair | **Not certified safe for real-user disks**; UEFI installation is gated off |
| UEFI | IA32 and x64 UEFI live-boot paths have OVMF/QEMU evidence | UEFI **installation** unavailable; Secure Boot not supported |
| Networking | IPv4/IPv6, ARP, DHCP, DNS, TCP/UDP, socket and TLS implementations; multiple Ethernet drivers | Networking features are incremental; no claim of support for arbitrary physical NICs |
| Wi-Fi | Network manager, UI, security groundwork and early chipset-driver work | **Cannot currently scan/join Wi-Fi networks with the implemented hardware support** |
| Applications | Built-in editor/system tools; package-supported NetSurf browser; DoomGeneric/Freedoom and other ports | Port packaging, device support and runtime completeness vary; Doom audio and saves remain open |
| Appearance | MOD7 default plus Vista, Modern VOS, Native and Android icon themes; shared desktop/application/file icon routing | Vista and MOD7 derive from user-supplied Windows artwork with no supplied open licence; see the release notice |
| Development tooling | VScript compiler/interpreter, C/C++ components, native SDK, VPK packages, third-party port recipes; Linux/macOS Make builds and a Windows WSL 2 bridge | Not full compatibility with desktop Linux apps or their dependencies; native MSVC builds are unsupported |
| Testing | Host core/package/icon/render checks; QEMU smoke, ISO-menu, installed-input and eight-scenario installed-disk verification run for this upload | QEMU evidence is not physical-hardware certification |

## Later development notes

Source main at `df2cc1110983fc69296b5ceb2afd68665d92dcdd` is ahead of
the published ISO baseline. This update describes source changes, not newly
built or revalidated public images.

| Area | Later source development | Limits |
| --- | --- | --- |
| VOSCast | Opt-in browser desktop viewing over HTTP; session token, pause/stop and bounded frame rate | View-only, one client, isolated network only; no TLS or remote input |
| Device diagnostics | Settings displays PCI driver binding/probe state; live firmware USB-mouse fallback | Physical input retest remains necessary |
| Third-party apps | Native DoomGeneric/Freedoom via ABI-3 surfaces, VPK and separate WAD; see [port notes](THIRD_PARTY_SOFTWARE.md) | No complete Doom audio, multiplayer or save/load |
| Build portability | Apt-based dependency setup, pinned i686-elf cross build, C++11 host bootstrap | Full new Kali ISO build not independently verified here |
| VM display integration | Existing virtual graphics drivers and manual mode changes | Automatic host-window resizing and guest additions are not claimed |

## Boot and release readiness

Source documentation distinguishes **working emulator paths** from **verified physical hardware**. It describes BIOS/GRUB boot and disk-only BIOS installation in QEMU, and both UEFI loader variants in OVMF. An installed UEFI disk is **not** a supported installation workflow. Secure Boot is **off/unsupported**.

The source release gate reports one of:

- **NO-GO:** required evidence is missing, blocked, failed, stale or skipped;
- **PRERELEASE (VM ONLY):** required checks pass but physical hardware certification is missing or gated hardware issues remain;
- **RELEASE CANDIDATE:** required checks and real-machine preflight evidence exist, with no remaining hardware-gated defects.

For this upload, the required core, package, dual-kernel and smoke targets passed; ISO verification passed four scenarios, and installed-disk verification passed eight scenarios including persistence, GPT-neighbour preservation, repair, backup-kernel boot and non-target disk protection. A formal physical-hardware release-candidate claim is still not made.

## Important known limitations from the source release ledger

- **RG-1:** Fresh installed VLFS2 volumes are created without journaling by default.
- **RG-3:** Installation to, and boot from, a USB stick have not been verified.
- **RG-5:** A GPT disk extending beyond driver reachability can be reported as invalid rather than partly inaccessible; the installer refuses unsafe use.
- **RG-6:** Read-only NVMe devices may be presented as writable before the write is rejected.
- **RG-12:** The GUI's removable-file size display can show a negative size for files of 2 GiB or more.
- **Physical retest still required:** QEMU now proves independent BIOS installed boot and post-install pointer movement/clicks, but the reported HP ProBook trackpad/mouse case still needs a new real-machine retest.

These are **documented source-development issues**, not a claim that each is reproducible in the public prebuilt ISO files. No defect is considered fixed just because a patch prompt exists.

## Links and status sources

- [Public release README](../README.md) and [download/safety guide](RELEASE_AND_SAFETY.md)
- [Architecture overview](ARCHITECTURE.md)
- [Build, testing and contributor entry points](BUILD_AND_TEST.md)
- [Source repository](https://github.com/chanatun-volatilis/VolatilisOS-source-code) (access currently restricted)
- Source references for maintainers: `docs/RELEASE_GATE.md`, `docs/STORAGE_RELEASE_NOTES.md`, `docs/WIFI.md`, `docs/UEFI_BOOT_MATRIX.md`, `docs/USB_STORAGE_MATRIX.md`, and `docs/DOOM_PORT.md`.

**Please treat these status descriptions as versioned documentation, not a live capability detector.**
