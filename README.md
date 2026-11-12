# OpenSense TDP Preview

Experimental Windows x64 build of [OpenSense](https://github.com/archivesteak/opensense), based on commit `b5911c1712bb862bb13023bd3cc7b054b4461087`.

Adds manual Intel CPU PL1/PL2 wattage controls and NVIDIA GPU power-limit control under **System → CPU and GPU power limits**. Values are checked against reported limits, and writes are read back for verification.

## Download

[Download the complete Windows build](https://github.com/Laith1/opensense-tdp/actions/runs/43052783996/artifacts/13870442207) (GitHub sign-in may be required).

The ZIP contains:

- `OpenSense-0.3.6-TDP-Preview-Setup-x64.exe` — installer with the updated app, background service and official PawnIO setup.
- `OpenSense-0.3.6-TDP-Preview-Portable-x64.zip` — portable app; CPU control requires PawnIO installed separately.
- `OpenSense-0.3.6-TDP-Preview-Source.zip` — corresponding source.
- `SHA256SUMS.txt` — checksums.

The Actions artifact expires on November 25, 2026. Download it before then, or run the workflow again under Actions.

## Use

1. Close NitroSense/PredatorSense before using OpenSense.
2. Install the Setup build so both the app and service have the new methods. A portable copy can otherwise connect to an older installed service.
3. Open **System → CPU and GPU power limits**, press **Refresh**, record the original values, enter watts, and apply CPU or GPU independently.

This preview compiled successfully on Windows and passed all **645 tests**. The artifact and individual file checksums were verified. It has not been tested on real laptop hardware or through an interactive Windows installation.

BIOS, MMIO and GPU driver restrictions still apply. Some laptop GPUs reject power-limit changes. AMD CPU/GPU control is not implemented. Manual limits are not reapplied at startup, and closing the app does not restore them; re-enter the original values to restore them. Mode changes, sleep, reboot or driver resets can override the limits.

## Build

The workflow `.github/workflows/build-opensense-tdp.yml` checks out the pinned upstream source, applies the embedded patch, runs tests, and packages the installer, portable application and source on Windows. It publishes build artifacts, not a GitHub Release.

[Successful Windows build](https://github.com/Laith1/opensense-tdp/actions/runs/43052783996). Source is GPL-3.0-or-later; see the included upstream LICENSE.
