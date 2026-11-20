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

## Screenshots

A closer look at the VolatilisOS 2.1 desktop and its built-in apps. All of these were taken on 2.1 running in QEMU.

### The desktop and Programs menu

| | |
| --- | --- |
| ![Desktop with menus](screenshots/11-desktop-clock-calendar-programs.png) Right-click the desktop for **New File**, **New Folder**, **In Terminal**, **Personalize** and **Clean** | ![Programs menu](screenshots/18-programs-menu-clean-desktop.png) The **Programs** menu, with search, places and app categories |
| ![Programs menu over terminals](screenshots/05-programs-menu.png) The Programs menu opened over two terminals | ![Early 2.1 Programs menu](screenshots/13-programs-menu-and-vfetch-early.png) An early 2.1 build with a pixel font, running `vfetch` |

### Settings and System Monitor

| | |
| --- | --- |
| ![Desktop settings](screenshots/02-settings-and-system-monitor.png) **Settings**, Desktop page: background, pattern, clock, accent, language, corners, shadow and opacity | ![Graphics settings](screenshots/17-graphics-settings-and-system-monitor.png) **Settings**, Graphics page: quality presets, anti-aliasing, smoothing, shadows, rounded corners and transparency |
| ![System Monitor](screenshots/14-system-monitor-over-terminals.png) **System Monitor** shows memory, storage, CPU use, tasks and frames per second | ![Display settings](screenshots/15-display-settings-over-terminals.png) Display settings: brightness, pixel size and terminal options |

### Files

| | |
| --- | --- |
| ![Files icon and list views](screenshots/03-files-icon-and-list-views.png) **Files** in icon view and list view, with a sidebar and a **USB DRIVE** | ![Files and vfetch](screenshots/06-files-and-vfetch.png) Files next to Terminal running `vfetch` and `meminfo` |
| ![Programs menu over Files](screenshots/07-programs-menu-over-files.png) The Programs menu opened over Files | ![Lock screen](screenshots/19-lock-screen.png) The **lock screen**: click or press a key to unlock |

### Terminal and the kernel

| | |
| --- | --- |
| ![Clock and memory terminals](screenshots/01-clock-and-memory-terminals.png) **Clock** next to `vfetch`, `meminfo`, `mem` and `heaptest` | ![Heap test](screenshots/04-terminal-help-and-heap-test.png) `heaptest` checks the kernel heap and shows it growing |
| ![Command list](screenshots/08-command-list-and-heap-test.png) Part of the `help` command list, and `vfetch` with the V-shaped logo | ![Four terminals](screenshots/10-four-terminals-1280x800.png) Four **Terminal** windows with tabs and a Split menu, at 1280×800 |

### Notes, VScript and games

| | |
| --- | --- |
| ![VScript in Notes](screenshots/09-notes-vscript-editor.png) **Notes** editing two VScript programs, `control-center.vs` and `pong.vs` | ![Notes with formatting](screenshots/12-notes-terminal-clock-calendar.png) Notes with bold, colours and a ruler, reading `vsdocs.txt`, next to Clock and Calendar |
| ![3D Chess](screenshots/16-3d-chess-japanese.png) **3D Chess** with the Japanese interface and the navy Volatilis wallpaper | |

## Documentation for 2.1

| Page | What you learn |
| --- | --- |
| [Getting started](docs/getting-started.md) | How to boot 2.1 in QEMU or VirtualBox, and what the boot menu means |
| [What is in 2.1](docs/whats-in-2.1.md) | The desktop, the apps and the kernel features of 2.1 |
| [Terminal guide](docs/terminal-guide.md) | Useful shell commands such as `vfetch`, `meminfo` and `heaptest` |
| [Known limits](docs/known-limits.md) | What 2.1 cannot do yet, starting with: no installer |
| [Screenshots](docs/screenshots.md) | All 19 screenshots of 2.1 on one page, in the order they were taken |

## Versions at a glance

| Version | Nickname | Installer | Where |
| --- | --- | --- | --- |
| 2.2 Beta | **Navy Horizon** | Yes | [`main` branch](https://github.com/chanatun-volatilis/VolatilisOS/tree/main) |
| 2.1 | none | **No installer yet** | this branch (`version-2.1`) |

Website and full docs: https://chanatun-volatilis.github.io/VolatilisOSDocs/
· Downloads on itch.io: https://volatilis-2033.itch.io/
