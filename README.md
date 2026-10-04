# LineageOS local manifests for Amazon devices

Dependencies for building LineageOS 24.0 on the MT8188-based Amazon Fire tablets.

Currently supporting:
- Fire Max 11 2023 (13th Gen) - `sunstone`

## Usage

### 1. Initialize the LineageOS 24.0 source (optional)

> [!NOTE]
> Skip this step if you already have a LineageOS 24.0 tree synced.

> [!TIP]
> A shallow init (`--depth=1`) is recommended to save disk space and bandwidth, the full git history isn't needed to build.
> This matters most for the kernel, which carries the full Android Common Kernel history.

```bash
mkdir -p lineage-24.0 && cd lineage-24.0
repo init -u https://github.com/LineageOS/android.git -b lineage-24.0 --git-lfs --depth=1
```

### 2. Add these manifests and sync

```bash
git clone https://github.com/amazon-oss/local_manifests.git -b lineage-24.0 .repo/local_manifests
repo sync -c --no-clone-bundle --no-tags -j$(nproc --all)
```

Then build:

```bash
. build/envsetup.sh
breakfast sunstone
mka bacon
```
