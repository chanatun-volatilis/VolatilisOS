# Publishing the recovered V2.0 Beta binaries (owner checklist)

**State:** The branch is currently documentation only; no ISO or screenshots have been pushed to GitHub. No source-code upload is authorized.

## First: supply a correctly identified V2.0 ISO

The provided `volatilis-master.iso` is **not** the desired archive. Its SHA-256 is `49843b7c441bf1ee20e2a2934f29c624b7d6f0d9ef8427a29485e236c63f2b63`, matching `VOS V2.1 Beta.zip/build/volatilis-master.iso`. The ISO itself says “VolatilisOS v2.1” in the GRUB menu and kernel. Do **not** upload or rename it as V2.0.

Before any binary publication, inspect the replacement ISO boot menu/kernel, boot in a disposable no-disk QEMU VM, compute its SHA-256 and record the size/version. Only then commit the actual ISO to this release branch (with Git LFS if it exceeds GitHub's allowed per-file size) and update README's download section with the verified filename and checksum. Do not upload the V2.1 source ZIP.

## August screenshots selected by the author

A prepared screenshot ZIP contains exactly these original assets:

```text
screenshots/august-desktop.png
screenshots/v2.0-cli-editor-vfetch.png
screenshots/v2.0-cli-shell-memory.png
```

The desktop image is **August-era**, not conclusively identified as the exact 2.0 kernel. The CLI photos show `VolatilisOS v2.0`. After uploading those exact PNGs, insert the following in the README's screenshots section:

```markdown
![August 2026 Volatilis desktop interface](screenshots/august-desktop.png)
*August 2026 desktop-era snapshot; exact V2.0 GUI build not independently confirmed.*

![VolatilisOS v2.0 CLI editor and vfetch](screenshots/v2.0-cli-editor-vfetch.png)
![VolatilisOS v2.0 CLI commands and memory map](screenshots/v2.0-cli-shell-memory.png)
```

## Verify the public branch

- The branch URL is `https://github.com/chanatun-volatilis/VolatilisOS/tree/version-2.0-beta`.
- There must be only one **verified V2.0 ISO**, README and Markdown docs, and those three screenshots.
- Check the asset SHA-256 values in [screenshot provenance](SCREENSHOT_PROVENANCE.md).
- **Never publish** `kernel/`, `drivers/`, `filesystem/`, `src/`, `include/`, `tools/`, private source ZIPs, code bundles, development disk images or user data.
- After committing, open the public branch link in a logged-out browser and verify the ISO link and screenshots display.
- Do not claim release-grade QA or safe physical installation without independent evidence.
