# TECNO BG7n — GKI r3 + KernelSU v3.2.5 + SUSFS Build Kit

This kit is prepared for **TECNO BG7n / Spark 20C** and is pinned to the Google GKI release **android12-5.10-2025-06_r3**, Linux **5.10.237**, commit **d09ef2e980e0974a0d6dfe762e29fff118db7f46**. Google lists this exact tag/commit as the 5.10.237 GKI r3 build.

## Stock boot source

The workflow now downloads the stock boot image automatically from your public GitHub Release:

- Repository: `whmyjda97-lab/tecno20c`
- Release tag: `stock-boot`
- Release page: https://github.com/whmyjda97-lab/tecno20c/releases/tag/stock-boot

The workflow discovers the boot-related release asset, extracts `boot.img` from it, hashes it, and then uses that exact image for repacking. Your Release page currently shows the `stock-boot` tag and 3 assets; the workflow does not depend on a hard-coded asset filename. It does **not** require `boot.img` to be committed into the repository.

## Repository layout

Upload the contents of this directory to the root of your GitHub repository:

```text
.github/workflows/build-bg7n.yml
BG7n_stock_defconfig
.gitignore
README.md
```

`stock/` is created by the workflow automatically. You do not need to upload a boot image there.

## Build

1. Upload these files to your repository.
2. Open **Actions**.
3. Select **Build BG7n GKI r3 + KernelSU + SUSFS**.
4. Select **Run workflow**.
5. Leave `boot_release_tag` as `stock-boot`.
6. Start the workflow.

The workflow will:

1. Download the exact Google GKI r3 source.
2. Verify the exact `common` commit and kernel version.
3. Integrate KernelSU `v3.2.5`.
4. Apply the pinned SUSFS `gki-android12-5.10` ref (default `be08face`) and verify the module is v2.2.0.
5. Apply the pinned SUSFS patches for `gki-android12-5.10`.
6. Build ARM64 kernel/modules.
7. Download and verify the stock BG7n boot image from the Release above.
8. Repack the stock boot image with the new kernel using `magiskboot`, preserving the stock boot layout.
9. Produce kernel, SUSFS, boot image, config, manifest, ABI/KMI evidence and SHA256 hashes as Actions artifacts.

## Important

Do not flash the generated boot image until the first build logs and `kernel_verification.txt` have been checked. Keep the original stock boot image available as the recovery path.


**Stock boot source:** GitHub Release `whmyjda97-lab/tecno20c`, tag `stock-boot`, asset `boot.img.zip`. The workflow downloads this exact asset and requires it to contain `boot.img`.
