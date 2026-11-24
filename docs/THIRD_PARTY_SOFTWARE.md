# Native and third-party software in VolatilisOS

Development-source reference: `df2cc1110983fc69296b5ceb2afd68665d92dcdd` (24 November 2026).
The public ISO baseline remains `549e6d45`. These notes describe the source
implementation, not a new binary verification.

## Native application architecture

The VOS cross-development SDK compiles C/C++ programs into i386 ELF
executables for the versioned userspace ABI. Its libc and graphics APIs
bridge applications to kernel services. VPK packages manage executables,
libraries and application data. Existing Linux or Windows binaries cannot
simply be assumed to work: ports need compatible APIs and dependencies.

## DoomGeneric and Freedoom

The pinned DoomGeneric engine builds into `doomgeneric.elf`, an ABI-3 i386
ELF running natively in userspace. Its C platform backend uses the native
application-surface API, event queues and monotonic clock. The game renders
320 × 200 indexed frames with its own palette; the compositor handles
presentation and fullscreen. Relative mouse capture is released when the
menu opens or focus is lost.

Freedoom 0.13.0 Phase 2 provides the separate IWAD at
`/share/freedoom2.wad`. The engine and data have distinct licenses (engine:
GPL-2.0-or-later; Freedoom: BSD-3-Clause). No proprietary Doom IWAD is
required. The release packaging is designed to include corresponding
DoomGeneric source and notices.

From the graphical terminal, where the two packages are installed:

```text
exec doomgeneric.elf -iwad /share/freedoom2.wad -nosound
exec doomgeneric.elf -iwad /share/freedoom2.wad -nosound -f
```

The source's acceptance ledger documents a 120-frame platform test and a
180-frame actual-engine QEMU test, including the packaged IWAD and mouse
input path. This documentation refresh did not rerun those tests. Audio,
multiplayer and reliable save/load remain incomplete.

For a persistent VM disk, use a disposable image of at least 128 MiB; older
16 MiB disks cannot hold the entire IWAD. Do not attach physical disks.

## Other applications

NetSurf provides a native browser port; Calculator demonstrates the C++
SDK. The desktop also includes built-in Files, Terminal, Text Editor,
System Monitor, Calendar, Clock and media utilities. Port compatibility
varies by build; full desktop Linux or Windows compatibility is not claimed.

## Development references

- [Doom port status](https://github.com/chanatun-volatilis/VolatilisOS-source-code/blob/df2cc1110983fc69296b5ceb2afd68665d92dcdd/docs/DOOM_PORT.md)
- [DoomGeneric backend](https://github.com/chanatun-volatilis/VolatilisOS-source-code/blob/df2cc1110983fc69296b5ceb2afd68665d92dcdd/ports/doomgeneric/doomgeneric_volatilis.c)
- [Build and test](BUILD_AND_TEST.md)

The development repository is private; its links require access.
