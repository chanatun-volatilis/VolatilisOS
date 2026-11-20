# Known limits of VolatilisOS 2.1

## 1. No installer yet

VolatilisOS 2.1 **cannot be installed** to a hard disk. It only runs live from
the disc (or the ISO in a virtual machine).

- When you shut down, nothing is kept. The next boot starts fresh.
- The boot menu still shows a **Backup installers** entry, and the shell help
  text mentions an `install` command. These were early work in progress and are
  **not supported** in 2.1. Please do not use them on a real computer with data
  you care about.
- A working installer arrived in **VolatilisOS 2.2 Beta "Navy Horizon"**, on the
  [`main` branch](https://github.com/chanatun-volatilis/VolatilisOS/tree/main).

## 2. Older hardware only

- 32-bit x86 (i386/i686) and **legacy BIOS** boot. Computers that only boot in
  UEFI mode will not start it.
- It was mostly tested in **QEMU**. Mice and touchpads on real laptops were
  fixed later, in 2.2.

## 3. No more updates

2.1 is kept here for history. It does not get bug fixes. For the newest
features and fixes, use 2.2 "Navy Horizon".
