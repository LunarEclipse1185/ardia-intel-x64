# Ardia 0.2.47 — experimental Intel build 1

An unofficial x86_64 build from this fork, based on upstream commit `23c750f87` (one commit after Ardia
0.2.47-nightly.5), with this fork's Intel changes. Built from fork commit `3452457cf96bfdb42a7ae226efc670f89cb9720e`.
The app reports version 0.2.47-nightly.5, build 122. The engine is Chromium 157.0.8103.50 with Helium 0.21.2,
helium-macos 0.21.2.1 and Ardia's patches. This is not an official upstream stable or nightly release.

## Downloads

- **Ardia-0.2.47-intel.1.zip** — the app. Extract it and move Ardia.app to Applications if desired.
- **ArdiaCore-157.0.8103.50-x86_64.tar.gz** — the matching engine framework for developers; app users do not need it separately.
- **Ardia-0.2.47-intel.1-source.tar.gz** — the exact fork source, pinned Helium sources, bundled uBlock Origin source, build settings and provenance.
- **SHA256SUMS** — checksums for the downloads.

## Before installing

- **Ad-hoc signed, not notarized.** Apple has not verified the developer's identity. If Gatekeeper blocks the app,
  verify the download, attempt to open it, then use System Settings > Privacy & Security > Open Anyway.
- **Hardened runtime is disabled.** This allows the ad-hoc app to load its embedded frameworks without a shared Apple
  signing Team ID, but provides fewer runtime protections than upstream's official release.
- **Restricted passkey/payment keychain groups are omitted.** Features requiring upstream's provisioning profile are not supported.
- **Updates are manual.** The packaged app disables upstream's automatic update configuration so it cannot install an Apple Silicon release.
- This build passed a hidden smoke test on an Intel Mac running macOS 15.7.9: launch, page loading, JavaScript,
  DOM interaction and quit. Other machines, macOS versions and all individual features have not been exhaustively tested.

## Source

The source bundle includes the fork's licenses and notices, dependency source archives and `PROVENANCE.json`.
It also identifies the exact upstream Chromium source and the engine tree. Keep the corresponding sources available
alongside the binaries.

## Build

With a matching Intel ArdiaCore framework available:

```bash
TARGET_CPU=x64 ARDIACORE_FRAMEWORK="/path/to/Chromium Framework.framework" \
  scripts/agent/build-app --as intel-x64 --config Release --adhoc
```

The normal build without `--adhoc` retains its original signing settings. The prebuilt engine must match this
checkout's engine sources; an unmodified Chromium framework is not compatible.
