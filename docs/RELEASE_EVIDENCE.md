# V2.0 Beta: evidence, version verification and scope

**Prepared:** 21 November 2026. **This is not a release announcement.**

## Evidence inspected

| Evidence | What it establishes | What it does not establish |
| --- | --- | --- |
| Gallery screenshot `Screenshot 2569-08-01 at 15.05.26.png` | The screenshot visibly names “VolatilisOS v2.0,” `vsh 2.0`, `vfetch`, VLFS2, a VFS layer, C interpreter, editor and prototype installer | Actual on-disk integrity, date of ISO compilation, successfully tested physical installation |
| Gallery screenshot `Screenshot 2569-08-05 at 15.15.51.png` | V2.0 text shell, workspaces, help output, `ls`, `meminfo` and memory-map reporting | Exact supported command count or hardware list |
| Gallery screenshot `Screenshot 2569-08-09 at 15.10.41.png` | An August desktop interface with Japanese launcher, file-manager, images and calculator | Conclusive proof this GUI image was produced by the same V2.0 ISO |
| Uploaded `volatilis-master.iso` | 43,612,160 bytes, SHA-256 `49843b7c441bf1ee20e2a2934f29c624b7d6f0d9ef8427a29485e236c63f2b63`; its GRUB menu and embedded kernel strings say `2.1` | **It is not verified to be V2.0**; therefore it has not been distributed in this branch |
| `VOS V2.1 Beta.zip` | Contains a `build/volatilis-master.iso` with the exact same SHA-256 as the uploaded ISO | A V2.0 release source tree (this is labeled 2.1) |
| Existing public `version-2.1` branch | Documents the subsequent 2.1 release as BIOS/live-first and says the older installer was not supported for production | Does not replace direct evidence for 2.0 or prove every older V2.0 command functioned correctly |

The screenshots use Thai Buddhist calendar year **2569** in their filenames, corresponding to **2026**. This is supported by their archive timestamps and not by an external release publication record.

## V2.0 claims supported by screenshots

**Observed screen content:** x86 32-bit kernel, VGA text, vsh shell, a VLFS2 root on `/dev/ata0p1`, filesystem/VFS summary, paging and memory reports, `vfetch`, built-in C interpreter, text editor and various shell utilities. Screenshot text discusses a custom disk installer; **no safe installation outcome was independently verified**.

**Unverified:** exact V2.0 kernel sources and commit, kernel binary hash, V2.0 GUI ISO identity, device compatibility, reproducible build, QA test results, networking capabilities and every feature claimed by later versions. Do not copy the V2.1 or 2.2 feature matrix onto this branch.

## Release completion checklist

- [ ] Receive **actual V2.0 ISO**.
- [ ] Inspect its GRUB menu, embedded version strings and boot modes; stop if it identifies as V2.1.
- [ ] Compute file size and SHA-256; compare with the file to be uploaded.
- [ ] Boot it in a no-host-disk BIOS QEMU VM and record V2.0 evidence where possible.
- [ ] Upload **only the verified ISO** plus the selected archival screenshots, never the source-code ZIP.
- [ ] Upload one August desktop-era screenshot and at most two V2.0 CLI screenshots, with accurate provenance captions.
- [ ] Update README links to files that actually exist and verify GitHub's branch tree contains no source directories or later-version ISOs.
- [ ] Verify the final ISO URL, checksum, README screenshots and branch tree after publication.

Until these are complete, the branch is **documentation-only / incomplete release**, not a published V2.0 binary archive.
