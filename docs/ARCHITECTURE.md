# VolatilisOS architecture overview

This is a short, public-facing tour of the current source layout, reviewed against `VolatilisOS-source-code` `main` at `549e6d454157675664eeb416975f50d8742b29f4` (24 November 2026). Source access may be restricted. Paths refer to the **source repository**, not the prebuilt-binary repository you are reading.

## Two editions, two kernels

VolatilisOS builds separate **GUI** and **CLI** i686/ELF32 kernels. They share selected implementation code, a versioned user ABI and common subsystems, but have different entrypoints, private adapters and boot initialization. They are two boot personalities, **not** one kernel toggling the desktop on and off.

```text
boot/ (BIOS, GRUB/Multiboot, UEFI experiments)
    |
    +-- kernel/core/init/gui/ ---> GUI kernel
    |
    +-- kernel/core/init/cli/ ---> CLI kernel
                                    |
                     common ownership layers
             kernel/core/ + kernel/services/
                         /             \
                  drivers/       domain libraries
                           filesystem/
                           networking/
                           graphics/
                           libraries/
                                    |
                           userspace/ + vscript/
```

The arrows indicate source responsibilities, not an exact boot or memory-initialization sequence.

### Privilege model

`kernel/core/` owns privileged CPU, interrupts, memory, process and scheduler behavior. `kernel/services/` provides storage, console, device, networking, app and other coordination. **These services currently run in the privileged kernel address space**; the naming is an organizational refactor, not a microkernel or isolated userspace-service design.

Userspace programs use ELF loading, a shared/versioned system-call ABI and the supported libc/SDK. Not every GUI built-in app is a ring-3 userspace program.

## Where source files live now

| Source directory | Responsibility |
| --- | --- |
| `boot/` | BIOS/Multiboot, GRUB and experimental UEFI loaders |
| `kernel/core/` | CPU, interrupts, memory, tasks, processes, syscalls and IPC |
| `kernel/services/` | Service orchestration, console, storage, applications, device manager |
| `kernel/interfaces/`, `include/vos/` | Kernel contracts, headers and user-facing ABI |
| `drivers/` | Storage, display, input, audio, networking and other devices |
| `filesystem/` | VFS, VLFS2, FAT, partition handling and additional readers |
| `networking/` | IP, TCP/UDP, DHCP, DNS, sockets, TLS and wireless layers |
| `graphics/` | Rendering, compositor, fonts, widgets and desktop window manager |
| `libraries/` | Cryptography, codecs and shared helpers |
| `userspace/` | Programs and authoritative libc/runtime code |
| `vscript/` | VScript interpreter, compiler and runtime |
| `installer/` | Shared installer engine, disk layout and edition frontends |
| `config/`, `editions/cli/` | Build policy and edition graphs |
| `tools/`, `tests/`, `scripts/`, `ports/` | QA, SDK, utilities, external ports and packaging |

**Do not use the historical** `src/desktop.c`, `src/kernel.c`, `common/vfs.c` or `volatilis cli/src/install.c` paths for new source instructions. Earlier documentation described an older layout.

## Subsystem notes

**Boot:** A master ISO selects GUI/CLI live boot and graphical/command-line installation through GRUB. The supported installed-disk path is BIOS-first and has QEMU boot/persistence evidence. UEFI live boot can work under OVMF; UEFI installation and Secure Boot are not release-ready.

**Storage:** The block layer exposes disk capabilities and 512-byte compatibility sector operations; partition code validates MBR/GPT and filesystem code provides VFS mounts. Disk writes, cache barriers and installer planning are safety-critical. Larger disks and native 4 KiB media require explicit supported paths and bounds checks.

**Desktop:** The window manager, compositor, graphics/card layers and built-in applications are independently organized. The current desktop is not simply a fixed 640×480 16-colour framebuffer: supported modes and rendering formats vary with virtual graphics adapters and firmware framebuffers. One role-based icon manager serves the desktop and applications across the selectable themes.

**Input:** PS/2, Synaptics, VirtualBox/VMware absolute-pointer and USB HID paths feed the shared pointer state. Firmware USB handoff is followed by an i8042 resynchronization before VM and USB pointer protocols are enabled, preventing partial firmware-emulated packets from poisoning an installed boot.

**Network:** Ethernet/TCP/IP functionality and TLS are present; the request system can schedule compatible work concurrently. Wireless UI and security code do not imply a working radio driver. NetSurf is a third-party browser port packaged through the OS's application system.

**Toolchains:** C and freestanding kernel C++ coexist. VScript has an interpreter and an independent compiler path. The SDK and `ports/` support select third-party programs; they do not amount to binary compatibility with Linux or Windows.

## Boundaries worth preserving

- There is currently **one active CPU** in the supported VM profile, not an SMP kernel.
- Hardware implementations vary by edition and class. One working emulator is not universal hardware support.
- Read-only filesystem adapters should never be described as writable.
- User ABI compatibility requires care when changing shared interfaces.
- Never claim a working UEFI installer, signed Secure Boot, or physical-disk installation safety without matching tests.

For reproducible work and evidence, see [Build and test](BUILD_AND_TEST.md), [Current status](CURRENT_STATUS.md), and the private source's `docs/architecture/` references (for maintainers with access).
