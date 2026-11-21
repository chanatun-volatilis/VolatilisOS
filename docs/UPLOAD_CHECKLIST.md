# Publishing V2.0 Beta: remaining tasks

**Current state:** V2.0 documentation is on `version-2.0-beta`. **No V2.0 ISO or uploaded PNG assets are yet in the branch**. The independently verified previously provided ISO identifies itself as **V2.1**, not V2.0. **Never publish any source code or source-code ZIP**.

## Step 1 — Add the original screenshots

Unpack the prepared `VolatilisOS-V2.0-Beta-selected-screenshots.zip`. It includes these **four PNGs** under `screenshots/`:

- `august-desktop.png` — 27 August 2026, blue GUI / launcher / Welcome / browser; version **unconfirmed**.
- `v2.0-cli-editor-vfetch.png` — 1 August 2026, V2.0 editor and `vfetch`.
- `v2.0-cli-help-memory.png` — 1 August 2026, V2.0 shell navigation, memory and `id`.
- `v2.0-cli-memory-map.png` — 3 August 2026, V2.0 memory map and heap.

Upload **only these images** to the public repository's `version-2.0-beta` branch under `screenshots/` (e.g. by checking out the branch, copying the folder, `git add screenshots/`, committing and pushing). The originals are not currently present in GitHub. Verify their hashes against [SCREENSHOT_PROVENANCE.md](SCREENSHOT_PROVENANCE.md) after upload.

## Step 2 — Embed only after the paths exist

Insert the following under the README's August screenshots section **after** verifying the files exist. The downloadable screenshot ZIP includes this as a ready-to-paste fragment.

```md
### Desktop (August-era; build version not verified)

![August 27 VolatilisOS blue desktop, Welcome, browser and Programs launcher](screenshots/august-desktop.png)

*August 27, 2026 GUI screenshot. Exact OS version is not visible.*

### VolatilisOS v2.0 CLI

![V2.0 shell with built-in editor, VLFS2 introduction and vfetch](screenshots/v2.0-cli-editor-vfetch.png)

![V2.0 console navigation and physical memory report](screenshots/v2.0-cli-help-memory.png)

![V2.0 CLI kernel heap and physical memory map](screenshots/v2.0-cli-memory-map.png)
```

The uploaded August 9 and August 24 screenshots explicitly say V1.5 and must **not** be included as V2.0 snapshots.

## Step 3 — Publish only a genuinely identified 2.0 ISO

The previous file `volatilis-master.iso` is **not** V2.0. Its SHA-256 is `49843b7c441bf1ee20e2a2934f29c624b7d6f0d9ef8427a29485e236c63f2b63`, matching an ISO inside `VOS V2.1 Beta.zip`, and both GRUB menu and kernel strings identify **2.1**. **Do not rename or upload it as 2.0.**

When the actual V2.0 ISO is provided: inspect boot-menu/kernel version, boot read-only with a no-host-disk QEMU VM, compute SHA-256 and size, and publish **only that verified binary** (Git LFS if GitHub file-size policy requires). Update README with the real link and checksum.

**Do not publish** `kernel/`, `drivers/`, `filesystem/`, `src/`, `include/`, `tools/`, source ZIPs, compiler sources, development disk images or personal data.

## Step 4 — Final public check

In a logged-out browser, verify:

- The README's four Markdown images render.
- The ISO download actually identifies V2.0.
- No source files or wrong-version binaries are present.
- The desktop image is described only as August-era; CLI ones show V2.0.
- Checksums, QEMU instructions and all links match uploaded files.

Until that point, the branch is an **incomplete documentation-first historical archive**, not a verified V2.0 release.
