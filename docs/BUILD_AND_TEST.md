# Building and testing VolatilisOS

This public repository contains **prebuilt images and screenshots**, not the authoritative current kernel source. The build commands on this page apply to the separate [VolatilisOS source repository](https://github.com/chanatun-volatilis/VolatilisOS-source-code), which is currently private; a GitHub 404 or failed clone may simply mean you do not have access.

**Published source baseline:** `549e6d454157675664eeb416975f50d8742b29f4` (24 November 2026). Recheck build targets if working from a later commit.

## Quick start without source access

Download the images from [README.md](../README.md) and boot them in a VM. For example:

```sh
qemu-system-i386 -m 1024 -cdrom volatilis-gui.iso -boot d
qemu-system-i386 -m 512  -cdrom volatilis-cli.iso -boot d

# Or unpack the master ISO ZIP and choose an edition in GRUB:
unzip volatilis-master.iso.zip
qemu-system-i386 -m 1024 -cdrom volatilis.iso -boot d
```

These examples start an optical-image guest with no host physical disk attached. QEMU must already be installed; commands assume they are run from the directory containing the downloaded images.

For installed-disk experiments, create a **new disposable QEMU image** and explicitly confirm the target inside the guest; never attach a host disk or a valuable disk image. See [Release and safety](RELEASE_AND_SAFETY.md).

## Developer prerequisites

If you have source access, use Linux or macOS with GNU Make, Python 3, NASM, QEMU i386, GRUB tools and xorriso. Windows is supported through WSL 2, which runs that same Linux build pipeline; native MSVC compilation is not supported. The preferred compiler is `i686-elf-gcc`; Linux GCC with working `-m32`/multilib may be used for existing supported targets. Installed-disk QEMU tests additionally need `qemu-img`. Extra checks may need mtools, sgdisk, exfat tools and related utilities. Missing dependencies are **blocked or not tested**, not successful checks.

## Building from the source checkout

```sh
git clone https://github.com/chanatun-volatilis/VolatilisOS-source-code.git
cd VolatilisOS-source-code

make toolchain          # inspect the selected tools
make kernels            # build both independently booting kernels
make iso                # master ISO + standalone rescue ISOs
make run                # GUI development guest
make run-iso            # master ISO guest
make run-img            # raw image guest
```

On Windows PowerShell with WSL 2 installed:

```powershell
.\scripts\development\build-windows.ps1 -Target toolchain
.\scripts\development\build-windows.ps1 -Target rebuild-all
```

Generated files include `build/kernel-gui`, `build/kernel-cli`, `build/volatilis-master.iso`, `build/backups/volatilis-gui.iso`, `build/backups/volatilis-cli.iso`, and `build/os.img`. The source checkout may also have persistent VM images; **do not run two writable VMs against the same image**.

For a clean release reconstruction, source documentation also describes `make rebuild-all`. Consult the source's `docs/build/BUILDING.md` and `Makefile` for the exact current targets.

## Testing and release evidence

```sh
python3 tools/qa/host_check.py       # host test matrix; status can be pass/fail/blocked
make smoke-iso                       # standalone GUI/CLI rescue ISO boots
make check-iso QA_TIMEOUT=90         # master ISO selects both editions
make check-installed QA_TIMEOUT=90   # BIOS disk-only install/persistence checks
make mouseinstalledguest             # pointer movement/clicks after installed boot
make touchpadcheck                    # Synaptics pressure/motion/tap/scroll packets
make check-two-disk                  # nontarget disk safety fixtures
make qa-report                       # summarize provenance and results
make release-gate                    # decide NO-GO / PRERELEASE / RELEASE CANDIDATE
```

The 24 November public artifacts were built from the baseline above. Their release run passed `run-core`, `vpkcheck`, both kernels, smoke, standalone ISO smoke, the four-scenario ISO suite, the eight-scenario installed suite, installed pointer checks, icon/theme checks and rendering checks. Availability still varies with the host toolchain. A linked kernel is not proof of a successful boot; an emulator pass is not proof of safe physical-hardware installation. `make release-gate` does not publish a build.

Useful source references (if you have permission): `docs/QA_REPORT.md`, `docs/RELEASE_GATE.md`, `docs/HARDWARE_PREFLIGHT.md`, `docs/INSTALLER_STATE_MACHINE.md`, and `docs/development/CONTRIBUTING.md`.

## Development contributions

The source is not automatically open-source just because it is browsable to some accounts. The source's `COPYRIGHT` and third-party licenses control redistribution; do not assume MIT licensing. Ask the repository owner for access and applicable permission before redistributing or publishing source changes.

## Keep release artifacts honest

The public ISOs are **uploaded snapshots**, not synchronized to every source commit. Before replacing downloads, build and test the intended source commit, compute the new SHA-256 hashes for every artifact, verify the ZIP's inner ISO name and hash, and then update [README.md](../README.md), [Current status](CURRENT_STATUS.md), and any release notes together.
