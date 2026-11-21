# Downloads, installer safety and release notes

**Public binary line:** VolatilisOS 2.2 Beta — “Navy Horizon”.  
**Source reviewed:** private `VolatilisOS-source-code` at `9b69ff2ba24901ed98d040f205882a7d3fd5868c` on 21 November 2026.

The binaries in this repository are **fixed uploaded artifacts**. They do not automatically pick up new drivers, kernel fixes or features when the source repository advances. Their release label and original published checksums appear in [README.md](../README.md). No binary was rebuilt or independently rehashed during this documentation update.

## Choose a download

| File | Recommended use |
| --- | --- |
| [`volatilis-gui.iso`](../volatilis-gui.iso) | Boot directly into the GUI edition |
| [`volatilis-cli.iso`](../volatilis-cli.iso) | Boot the CLI edition |
| [`volatilis-master.iso.zip`](../volatilis-master.iso.zip) | Unzip to `volatilis.iso`; choose either edition from the GRUB menu |

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

**Never test the installer on a disk containing important data.** If you experiment with installation, use a new blank disposable VM disk, confirm the displayed target and all planned writes, and keep original VM images or snapshots backed up. Do not point the OS at an entire host device such as `/dev/sda` or a host NVMe namespace.

- **BIOS installer:** development code has installed-disk/QEMU evidence; physical boot after installation remains under active verification.
- **UEFI live boot:** has OVMF/QEMU evidence in the development tree, but do not assume every public image carries that boot path.
- **UEFI installer:** gated off, not a supported way to install.
- **Secure Boot:** not supported with the unsigned UEFI loaders.
- **USB-stick installation:** not release-certified; using USB mass storage as a file device is not the same as installing to and booting from it.
- **Writable external filesystems:** ext2/3/4, exFAT and NTFS remain read-only in development implementation.

The source project's release gate uses **NO-GO**, **PRERELEASE (VM ONLY)** and **RELEASE CANDIDATE**. The latest decision for these specific uploaded binaries was not independently checked during this documentation update, so this page does not claim a passing release candidate.

## Reporting a problem

Please include the specific ISO filename and its checksum, VM software/version, BIOS vs UEFI firmware, amount of RAM, exact action, error/screenshot and whether a disposable virtual disk was attached. If building from source, add the source commit hash, compiler toolchain and actual test output. Never upload passwords, private data, or a disk image containing personal files.

More context: [Current feature status](CURRENT_STATUS.md), [Architecture](ARCHITECTURE.md), and [Build/test guide](BUILD_AND_TEST.md).
