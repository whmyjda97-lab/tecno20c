# TECNO BG7n - Android common 5.10 + KernelSU-Next + SUSFS v2.2.0

This package is designed for the GitHub Actions build flow used for the TECNO BG7n kernel.

Source selections:
- Android common kernel: `d09ef2e980e0974a0d6dfe762e29fff118db7f46`
- KernelSU-Next: `26fded805206ae4542f4745e09cc465412994492`
- SUSFS: `gki-android12-5.10`, v2.2.0

Important integration change:
- The workflow applies the official SUSFS `50_add_susfs_in_gki-android12-5.10.patch`.
- The old combined `patches-susfs-bg7n.patch` is retained for reference only and is NOT applied, because comparison showed that its kernel-side changes overlap the official SUSFS 50 patch.
- The workflow does NOT apply `10_enable_susfs_for_ksu.patch` because the selected KernelSU-Next source already contains the SUSFS Kconfig integration.

The build fails early if:
- the exact KernelSU commit cannot be checked out;
- SUSFS v2.2.0 sources are missing;
- required SUSFS Kconfig symbols are not enabled after `olddefconfig`;
- `out/fs/susfs.o` is not produced;
- `vmlinux` contains no SUSFS symbols;
- the final boot image is missing.

The stock boot image is intentionally not stored in this repository. Upload `boot.img.zip` to the GitHub Release with tag `stock-boot`; the archive must contain a file named `boot.img`.

The main output is:
- `boot-BG7n-SUSFS-KSU.img`

Do not flash the output until the resulting image has been independently inspected and compared with the stock boot image.
