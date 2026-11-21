# V2.0 Beta shell and safety notes

These observations come from August 2026 screenshots, **not** from executing a verified V2.0 ISO in this review.

## Visible commands and concepts

The text interface labels itself `VolatilisOS v2.0`, running `vsh 2.0` in an 80×25 VGA text console. The screenshots show the `vfetch`, `version`, `ls` and `meminfo` commands, with a built-in line editor and multiple workspaces.

The on-screen help and feature overview mention ordinary utilities such as `df`, `du`, `mount`, `chmod`, `ln`, `ld`, `sort`, `uniq`, `cut`, `diff`, `more`, `head`, `tail`, `grep`, `tee`, `tr` and shell redirection/pipes. The complete list and functionality were not independently tested for V2.0.

The screenshots also discuss VLFS2 filesystems, a VFS that routes `/proc` and `/dev` paths, an i386 memory map, 4 KiB page frames and a prototype `install` command. A text or command existing in a screenshot is not proof that every edge case works or that it is safe for real disks.

## Do not test the installer on valuable media

V2.0 is an archived experimental build. No verified V2.0 release ISO, test logs or physical-installation acceptance results were supplied. **Do not install it onto a personal laptop, SSD, removable drive or disk containing files.** If a matching ISO is later verified, test first inside a fresh virtual machine without any host physical disks attached, and use a disposable VM disk for destructive tests.

## Boot example for a future verified ISO

```sh
qemu-system-i386 -m 512 -cdrom VERIFIED_VOLATILIS_2_0_BETA.iso -boot d
```

Do not mistake this placeholder for a downloadable file. See [release evidence](RELEASE_EVIDENCE.md) for the reasons the currently supplied ISO cannot be advertised as V2.0.
