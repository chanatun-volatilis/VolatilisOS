# VolatilisOS V2.0 Beta archive — publication checklist

**Current state (21 November 2026):** The `version-2.0-beta` branch contains **27 historical August screenshots**, all embedded and captioned in the [README](../README.md). The **actual V2.0 ISO is still missing**; the only supplied ISO was positively identified as V2.1 and must not be renamed or redistributed as V2.0. **No source-code upload is authorized.**

## 1. Screenshot gallery — complete

- [x] The uploaded images are tracked under `screenshots/` on the historical branch.
- [x] All **27** PNGs are displayed in a two-column README gallery with descriptions.
- [x] V2.0 CLI captures are distinguished from older V1.5 GUI captures and GUI screenshots with no visible version identifier.
- [x] Images have repository identities and version evidence recorded in [SCREENSHOT_PROVENANCE.md](SCREENSHOT_PROVENANCE.md).
- [x] The GitHub/project-page screenshot is described as an archived webpage, not a successful OS boot.
- [ ] A human viewing GitHub while logged out should verify that all 27 images actually render at the README URLs.

The earlier four-image upload instructions are superseded: all 27 files are already in Git. Do **not** rerun an uploader that appends an old four-image fragment to the new README.

## 2. Verified V2.0 ISO — still pending

The previously supplied `volatilis-master.iso` is **not a V2.0 release**. Its SHA-256 is `49843b7c441bf1ee20e2a2934f29c624b7d6f0d9ef8427a29485e236c63f2b63`, matching `VOS V2.1 Beta.zip`'s master ISO. Its boot-menu and kernel version strings identify **2.1**.

Before publishing another ISO:

1. Obtain the actual V2.0 ISO binary.
2. Verify its GRUB menu and kernel version strings, not merely the filename.
3. Boot in a **disposable QEMU guest with no physical host disks**; record actual V2.0 boot output and any unsupported cases.
4. Compute SHA-256 and size of the exact file to publish.
5. Upload **only the verified ISO**, using an allowed GitHub release/large-file method if required by size limits, and update the README's download link and checksum.
6. Preserve the original source repository's privacy and third-party license notices.

No actual V2.0 image was booted or tested as part of the screenshot documentation update.

## 3. Source-code prohibition

Never add `kernel/`, `drivers/`, `filesystem/`, `include/`, `src/`, `userspace/`, `vscript/`, `tools/`, development-source archives, compiler sources, or private disk images to this public archival branch.

This branch holds only public Markdown documentation and historical PNG screenshots until a correct V2.0 ISO is verified. The source repository remains private.

## 4. Verify the branch after future changes

- The image links in the README point to files that exist in `version-2.0-beta`.
- Older screenshots with on-screen `v1.5` labels remain clearly identified as older historical builds.
- Only genuine V2.0 binaries are advertised as V2.0 downloads.
- No private sources or user data are committed.
- The `main` branch is not altered by this historical archive maintenance.

Until a matching ISO is verified, this branch remains a **documentation-and-screenshot historical archive**, not a downloadable V2.0 release.
