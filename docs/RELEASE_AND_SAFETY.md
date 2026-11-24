# Downloads, installer safety and release notes

**Public binary line:** VolatilisOS 2.2 Beta — “Navy Horizon”.  
**Published build:** private `VolatilisOS-source-code` at `549e6d454157675664eeb416975f50d8742b29f4` on 24 November 2026.

The binaries in this repository are **fixed uploaded artifacts**. They do not automatically pick up new drivers, kernel fixes or features when the source repository advances. The files were rebuilt, boot-tested and independently hashed for this documentation update; their checksums appear in [README.md](../README.md).

## Choose a download

| File | Recommended use |
| --- | --- |
| [`volatilis-gui.iso`](../volatilis-gui.iso) | Boot directly into the GUI edition |
| [`volatilis-cli.iso`](../volatilis-cli.iso) | Boot the CLI edition |
| [`volatilis-master.iso.zip`](../volatilis-master.iso.zip) | Unzip to `volatilis.iso`; choose GUI/CLI live boot or graphical/command-line installation |

For the least risky first experience, use a new virtual machine with no host disks attached. An ISO boot alone does not mean an installation has taken place.

## Verify what you downloaded

From the same directory as your ISO or ZIP:

```sh
sha256sum volatilis-gui.iso
sha256sum volatilis-cli.iso
sha256sum volatilis-master.iso.zip

# If using the master ISO:
unzip volatilis-master.iso.zip
sha256sum volatilis.iso
```

Compare those values with the checksums published in [README.md](../README.md). Checksums detect unexpected changes/corruption relative to the published values; they are not a digital signature or a guarantee of safety.

## Try it in QEMU

```sh
qemu-system-i386 -m 1024 -cdrom volatilis-gui.iso -boot d
qemu-system-i386 -m 512  -cdrom volatilis-cli.iso -boot d
```

The GUI and CLI are **separate kernels**. The master image selects between them at boot. A 32-bit-capable legacy-BIOS virtual-machine profile is the conservative starting point. Physical hardware support is selective and may differ from QEMU.

## About installation

The development tree has a BIOS-first installer with explicit target selection, confirmation, partition safety mechanisms and QEMU tests. That does **not** certify installation on real disks or the same behavior in every published ISO.

The master and standalone CLI boot menus include **Command-Line Installation**.
From an ordinary CLI boot, `vos-install --cli` opens the same frontend. It
reuses the established installer backend rather than implementing separate
sector-writing logic. See [Command-line installation](CLI_INSTALLER.md).

**Never test the installer on a disk containing important data.** If you experiment with installation, use a new blank disposable VM disk, confirm the displayed target and all planned writes, and keep original VM images or snapshots backed up. Do not point the OS at an entire host device such as `/dev/sda` or a host NVMe namespace.

- **BIOS installer:** development code has installed-disk/QEMU evidence; physical boot after installation remains under active verification.
- **UEFI live boot:** has OVMF/QEMU evidence in the development tree, but do not assume every public image carries that boot path.
- **UEFI installer:** gated off, not a supported way to install.
- **Secure Boot:** not supported with the unsigned UEFI loaders.
- **USB-stick installation:** not release-certified; using USB mass storage as a file device is not the same as installing to and booting from it.
- **Writable external filesystems:** ext2/3/4, exFAT and NTFS remain read-only in development implementation.

## Input compatibility

These images move firmware USB ownership to the native controller before a
second i8042 reset and then enable VM absolute-pointer and USB HID input. QEMU
checks proved PS/2-only and EHCI USB-mouse movement and clicks after booting an
installed disk with no ISO attached. Synaptics packet tests cover pressure,
motion, tapping and scrolling. This is stronger regression evidence, not a
guarantee for every laptop; keep the installation media and a USB keyboard
available for the first physical retest.

## Artwork provenance

The Vista and MOD7 selectable icon themes are derivatives of user-supplied
Windows icon archives. Those archives contained no licence or redistribution
notice. The project records their provenance and does not claim the artwork as
original VolatilisOS work or as open-source. Download availability does not
grant permission to redistribute individual artwork or extracted assets.

The source project's release gate uses **NO-GO**, **PRERELEASE (VM ONLY)** and **RELEASE CANDIDATE**. The documented QEMU checks for this upload passed, but a formal physical-hardware release-candidate decision was not generated; this page does not claim one.

## Reporting a problem

Please include the specific ISO filename and its checksum, VM software/version, BIOS vs UEFI firmware, amount of RAM, exact action, error/screenshot and whether a disposable virtual disk was attached. If building from source, add the source commit hash, compiler toolchain and actual test output. Never upload passwords, private data, or a disk image containing personal files.

More context: [Current feature status](CURRENT_STATUS.md), [Architecture](ARCHITECTURE.md), and [Build/test guide](BUILD_AND_TEST.md).
