# Command-line installation

The 24 November 2026 VolatilisOS 2.2 Beta images provide two installation
front ends over the same checked installer backend:

- **Graphical Installation** opens the desktop Setup window.
- **Command-Line Installation** starts the text edition and opens a
  keyboard-only guided/advanced installer after input, storage and filesystems
  are initialized.

Choose the command-line option in the master or standalone CLI boot menu, or
run this from an ordinary VolatilisOS CLI session:

```text
vos-install --cli
```

Arguments after `--cli` go to the established installer. For example,
`vos-install --cli --dual ata0` enters the same alongside-install path as
`install --dual ata0`; it is not an independent disk-writing implementation.

## Guided and advanced operation

Guided mode lists detected whole disks with their model, bus, size, serial,
partition summary and any refusal reason. It offers explicit policies to:

- preserve existing partitions and use a verified Volatilis partition or
  safe free gap;
- install only when the selected disk is empty;
- erase the selected disk after the backend's exact destructive confirmation.

Advanced mode provides read-only MBR/GPT inspection, alongside installation,
whole-disk replacement, installed-system checking, boot-file repair, GPT
repair through the established tool, and confirmed VLFS2/FAT32 formatting
commands. VolatilisOS does not resize foreign filesystems: shrink or rearrange
another operating system's files with that system's own tools first.

## Safety and firmware boundary

The text interface does not write sectors directly. Before the first write,
the shared installer validates its payload and the exact selected target,
rejects installation media, mounted/ambiguous/read-only disks and unsafe
partition metadata, and displays the reviewed extents. Writes are fenced to
those extents. An incomplete marker remains until boot files, filesystem data,
flushes and read-back checks finish; success is reported only after the
complete marker is verified.

BIOS installation is supported. UEFI-booted sessions are detected, but UEFI
disk installation is refused before any write while that path remains gated.
Secure Boot is not supported. Always begin with a disposable virtual disk;
physical-disk installation is not release-certified.
