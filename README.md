# Jerry TrickyStore-Oos

Built-in Tricky Store OSS files for [JerryManager](https://github.com/WajahatNaeem056/JerryManager), so no separate Tricky Store module is needed.

This repo holds only the files JerryManager adds, not the full project. They are taken unmodified from the official [TrickyStoreOSS](https://github.com/beakthoven/TrickyStoreOSS) v3.1.0 release (build 201-e817d72), except `ts/supervisor.sh`, which is adapted from its `service.sh`. The source is in the original repo.

## Files

- `ts/daemon`, `ts/classes.dex`
- `ts/lib/<abi>/libTrickyStoreOSS.so` and `libinject.so` for arm64-v8a, armeabi-v7a, x86 and x86_64
- `ts/supervisor.sh`: starts and restarts the daemon (JerryManager's `service.sh` calls it)
- `ts/defaults/keybox.xml`: default keybox, used only when none exists
- `sepolicy.rule`

Copy `ts/` and `sepolicy.rule` into the `Jerry/` folder of JerryManager.

## Config

Read from `/data/adb/tricky_store/`:

- `keybox.xml`
- `target.txt`
- `security_patch.txt`

Changes take effect immediately, no reboot needed.

## Credits

Sincere thanks to:

- [**beakthoven**](https://github.com/beakthoven/TrickyStoreOSS): author of **Tricky Store OSS**.
- [**5ec1cff**](https://github.com/5ec1cff/TrickyStore): author of the original **TrickyStore**.

## License

GPL-3.0.
