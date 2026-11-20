# VolatilisOS 2.1 (older version)

> **No installer yet.** VolatilisOS 2.1 runs *live* from the disc only. It cannot
> be installed to a hard disk. If you want the installer, use the current version,
> **VolatilisOS 2.2 Beta "Navy Horizon"**, on the
> [`main` branch](https://github.com/chanatun-volatilis/VolatilisOS/tree/main).

This branch keeps VolatilisOS **2.1** exactly as it was, so you can try it and see
how the OS looked before 2.2. It holds the 2.1 disc image, its own small
documentation set, and screenshots taken on 2.1.

![VolatilisOS 2.1 desktop with Terminal, Files, Clock, Calendar and the Programs menu](screenshots/11-desktop-clock-calendar-programs.png)
*The VolatilisOS 2.1 desktop: Terminal, Files, Clock, Calendar and the Programs menu.*

## Download

| File | What it is | Size |
| --- | --- | --- |
| [`volatilis-2.1-master.iso`](volatilis-2.1-master.iso) | The 2.1 master disc. One GRUB menu boots the **GUI edition** or the **CLI edition**. | 45 MB |

SHA-256 checksum, so you can check your download is not broken:

```
bddfacfc53209ca7f67b2588f27ca80783cc98a452b750a331d89a687ba6a881  volatilis-2.1-master.iso
```

## Try it in 1 minute

VolatilisOS 2.1 is a 32-bit x86 system for legacy BIOS PCs and virtual machines.
The easiest way is QEMU:

```sh
qemu-system-i386 -m 512 -cdrom volatilis-2.1-master.iso
```

Then pick **VolatilisOS v2.1 GUI Edition** (the desktop) or
**VolatilisOS v2.1 CLI Edition** (text only) from the menu.

## Documentation for 2.1

| Page | What you learn |
| --- | --- |
| [Getting started](docs/getting-started.md) | How to boot 2.1 in QEMU or VirtualBox, and what the boot menu means |
| [What is in 2.1](docs/whats-in-2.1.md) | The desktop, the apps and the kernel features of 2.1 |
| [Terminal guide](docs/terminal-guide.md) | Useful shell commands such as `vfetch`, `meminfo` and `heaptest` |
| [Known limits](docs/known-limits.md) | What 2.1 cannot do yet, starting with: no installer |
| [Screenshots](docs/screenshots.md) | All 12 screenshots of 2.1, with a short note on each |

## Versions at a glance

| Version | Nickname | Installer | Where |
| --- | --- | --- | --- |
| 2.2 Beta | **Navy Horizon** | Yes | [`main` branch](https://github.com/chanatun-volatilis/VolatilisOS/tree/main) |
| 2.1 | none | **No installer yet** | this branch (`version-2.1`) |

Website and full docs: https://chanatun-volatilis.github.io/VolatilisOSDocs/
· Downloads on itch.io: https://volatilis-2033.itch.io/
