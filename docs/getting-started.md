# Getting started with VolatilisOS 2.1

> **No installer yet.** 2.1 runs live from the disc. Nothing is written to your
> disk, and when you turn the machine off, the system starts fresh next time.

## What you need

- The disc image [`volatilis-2.1-master.iso`](../volatilis-2.1-master.iso) (45 MB).
- A virtual machine program, such as **QEMU** or **VirtualBox**, or an older PC
  that can boot in **legacy BIOS** mode (not UEFI only).

## Check your download (optional)

On macOS or Linux, run:

```sh
shasum -a 256 volatilis-2.1-master.iso
```

It should print:

```
bddfacfc53209ca7f67b2588f27ca80783cc98a452b750a331d89a687ba6a881
```

If the numbers are different, the download is broken. Download it again.

## Boot it in QEMU

```sh
qemu-system-i386 -m 512 -cdrom volatilis-2.1-master.iso
```

`-m 512` gives the virtual machine 512 MB of memory. 2.1 runs well with 512 MB
to 1 GB (`-m 1024`).

## Boot it in VirtualBox

1. Make a new machine. Type: **Other**, version: **Other/Unknown** (32-bit).
2. Give it 512 MB to 1 GB of memory. You do not need a hard disk.
3. Put `volatilis-2.1-master.iso` in the optical (CD) drive and start it.

## The boot menu

When the disc starts, GRUB shows a menu for 10 seconds:

| Menu entry | What it does |
| --- | --- |
| **VolatilisOS v2.1 GUI Edition** | Starts the graphical desktop (the default). |
| **VolatilisOS v2.1 CLI Edition** | Starts the separate text-only kernel. |
| Backup installers | Left over from development. Not supported in 2.1, see [Known limits](known-limits.md). |

## After it starts

- The desktop has **home**, **Trash** and **README.txt** icons on the left.
- The **▲ button** at the bottom left opens the **Programs** menu.
- The **Search** box in the taskbar finds apps.
- Open **Terminal** and type `help` to see every command, or `vfetch` to see
  system information.

Next: [What is in 2.1](whats-in-2.1.md)
