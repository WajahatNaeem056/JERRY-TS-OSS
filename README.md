# Jerry TSOSS

Built-in TSOSS (Tricky Store OSS) files for [JerryManager](https://github.com/WajahatNaeem056/JerryManager), so no separate Tricky Store module is needed.

This repo holds only the files JerryManager adds, not the full project. The source is in the original [TrickyStoreOSS](https://github.com/beakthoven/TrickyStoreOSS) repo. The workflow here builds it and packs only what Jerry uses.

## Files

- `ts/daemon`, `ts/classes.dex`
- `ts/lib/<abi>/libTrickyStoreOSS.so` and `libinject.so` for arm64-v8a, armeabi-v7a, x86 and x86_64
- `ts/supervisor.sh`: starts and restarts the daemon (JerryManager's `service.sh` calls it)
- `sepolicy.rule`

Copy `ts/` and `sepolicy.rule` into the `Jerry/` folder of JerryManager.

## How the files are made

| File | Comes from (TrickyStoreOSS) |
| --- | --- |
| `ts/classes.dex` | `app/` Kotlin code. Gradle builds the release APK, R8 shrinks it, `classes.dex` is taken from it |
| `ts/lib/<abi>/libTrickyStoreOSS.so` | `app/src/main/cpp` (C++23, CMake, NDK 29), built per ABI |
| `ts/lib/<abi>/libinject.so` | `app/src/main/cpp/inject`, same build. Jerry installs it as `ts/inject` |
| `ts/daemon` | `module/daemon`, copied as is |
| `sepolicy.rule` | `module/sepolicy.rule`, copied as is |
| `ts/supervisor.sh` | `module/service.sh`, one change: the process check matches `supervisor.sh` instead of `service.sh` |

`module/keybox.xml`, `target.txt`, `customize.sh`, `post-fs-data.sh` and `module.prop` are not used. Jerry installs its own keybox and manages `target.txt`.

## Rebuild with GitHub Actions

1. Open the **Actions** tab, choose **Build Jerry ts/**, press **Run workflow**.
2. Leave `ref` as it is to build the pinned commit (`dda5277`), or enter another TrickyStoreOSS commit or tag.
3. Download the **JERRY-TS-OSS-ts** artifact (`ts/` and `sepolicy.rule`) and replace the files in this repo.

The workflow checks out TrickyStoreOSS with its PLTI submodule, so no source is copied here. It uses Java 26, Android SDK 37 and NDK 29, same as upstream.

## Config

Read from `/data/adb/tricky_store/`:

- `keybox.xml`
- `target.txt`
- `security_patch.txt`

Changes take effect immediately, no reboot needed.

## Credits

Sincere thanks to:

- [**beakthoven**](https://github.com/beakthoven/TrickyStoreOSS): author of **TSOSS (Tricky Store OSS)**.
- [**5ec1cff**](https://github.com/5ec1cff/TrickyStore): author of the original **TrickyStore**.

## License

GPL-3.0.
