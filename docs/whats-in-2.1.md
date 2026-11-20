# What is in VolatilisOS 2.1

VolatilisOS 2.1 is a from-scratch, 32-bit operating system with **two kernels**
on one disc: a **GUI kernel** for the desktop and a separate **CLI kernel** for
the text-only system. Both were written by one person.

> **No installer yet.** Everything below runs live from the disc.

## The kernel (the core of the OS)

What `vfetch` reports on 2.1:

| Item | Value in 2.1 |
| --- | --- |
| Kernel | VolatilisKernel, x86, 32-bit |
| CPU mode | i386 protected mode |
| CPU features used | 32-bit, FPU, MMX, SSE, SSE2 |
| Display | 960×540 at 32 bits per pixel (later builds of 2.1 also ran 1280×800) |
| Shell | `vsh`, with about 203 to 209 commands |
| File system | VLFS2, mounted at `/dev/rootfs` |
| Boot | Custom bootloader + GRUB |
| Built with | GCC and NASM |
| Extra | A built-in C interpreter |

**Memory, explained simply:** the kernel asks the firmware (BIOS) which parts of
memory are free (`meminfo` shows this "memory map"). It cuts free memory into
4 KiB pieces called *page frames*. On top of that it has a *heap*
(`kmalloc` / `kfree`): a pool the kernel borrows small chunks of memory from.
In 2.1 the heap can **grow on demand**, and `heaptest` proves it works.

## The desktop

- Windows with title bars, minimise, maximise and close buttons, that you can
  drag and resize.
- A taskbar with the **▲ Programs** button, **Search**, one button per open
  window, a power (AC) indicator and a clock.
- A desktop right-click menu: **New File**, **New Folder**, **In Terminal**,
  **Personalize** and **Clean**.
- A dotted navy-blue background and colour icons.

## The apps

| App | What it does |
| --- | --- |
| **Notes** | Text editor with line numbers, word wrap, Find, and Run for VScript files. Later 2.1 builds add bold, italic, underline, colours and a ruler. |
| **Code** | Write code |
| **Calc** | A calculator |
| **Terminal** | The `vsh` shell. Later builds add tabs and a **Split** menu. |
| **Clock** | Analogue clock with a date picker |
| **Calendar** | Month view |
| **Files** | Icon view and list view, a sidebar (Home, Desktop, Documents, Music, gallery, games) and a **USB DRIVE** |
| **Paint** | Draw pictures |
| **Settings** | Appearance, Graphics, Desktop, Taskbar, Text, Terminal, Display, Sound, Power. Language can be English or Japanese (kana and kanji input). |
| **System Monitor** | Memory, storage, CPU usage graph, tasks, running programs and frames per second |

The Programs menu sorts apps into **Accessories, Graphics, Sound, Internet,
Games and System**.

## VScript

VScript is VolatilisOS's own small programming language. In 2.1 you can write
`.vs` files in Notes and press **Run**. Examples in the screenshots include a
Pong game (`pong.vs`) and a settings window (`control-center.vs`). The full
language reference is in the file `vsdocs.txt` on the system.

Next: [Terminal guide](terminal-guide.md)
