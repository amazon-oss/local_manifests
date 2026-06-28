# LineageOS local manifests for Amazon devices

Dependencies for building LineageOS 18.1 on the MT8163-based Amazon Echo devices.

Currently supporting:
- Echo Spot 2017 - `rook`
- Echo Show 5 2021 (2nd Gen) - `cronos`
- Echo Show 5 2019 (1st Gen) - `checkers`
- Echo Show 8 2019 (1st Gen) - `crown`

## Usage

### 1. Initialize the LineageOS 18.1 source (optional)

> [!NOTE]
> Skip this step if you already have a LineageOS 18.1 tree synced.

> [!TIP]
> A shallow init (`--depth=1`) is recommended to save disk space and bandwidth the full git history isn't needed to build.

```bash
mkdir -p lineage-18.1 && cd lineage-18.1
repo init -u https://github.com/LineageOS/android.git -b lineage-18.1 --depth=1
```

### 2. Add these manifests and sync

```bash
git clone https://github.com/amazon-oss/local_manifests.git -b lineage-18.1 .repo/local_manifests
repo sync -c --no-clone-bundle --no-tags -j$(nproc --all)
```

Apply the required source patches (synced into `patches/` by this manifest):

```bash
./patches/apply.sh
```

> [!IMPORTANT]
> These patches are required for a working build. Run `./patches/apply.sh` after every fresh `repo sync`.
> Use `./patches/reset.sh` to roll them back to the upstream branch state.

Then pick a device and build, e.g.:

```bash
. build/envsetup.sh
breakfast lineage_cronos-userdebug   # or checkers / rook / crown
mka bacon
```
