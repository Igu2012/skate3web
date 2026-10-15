# Skate3Web

A lightweight WebAssembly build of `skate-3-rust-engine`, with a simplified interface and a static-site layout for GitHub Pages.

**GitHub Pages target:** https://igu2012.github.io/skate3web/ (Pages must be enabled for `main` / `/docs` in the repository settings.)

## Repository layout

- `engine/` — engine source based on the [`cleanroom-web` branch](https://github.com/andrewnakas/skate-3-rust-engine/tree/cleanroom-web). The web page has been simplified to start directly in the game, without a fullscreen button.
- `docs/` — prebuilt WebAssembly application and static files for GitHub Pages, including the simple map selector and the nine parks from the clean-pack release.
- `ATTRIBUTION.md` — project and asset provenance.

No ISO or retail Skate 3 files are included. Optional mod ZIPs are not part of this package.

## Large files and pack chunks

The main pack is split into `docs/core.pack.part0` (95,000,000 bytes) and `docs/core.pack.part1`. `loader.js` downloads the parts and concatenates them automatically before starting the engine. The WASM binary and map files are also below GitHub's 100 MB per-file limit; no manual joining is required.

## Run the prebuilt site locally

Serve the files over HTTP; do not open `docs/index.html` directly as a `file://` URL:

```bash
python3 -m http.server 8000 --directory docs
```

Open `http://localhost:8000/` in Chromium or Edge 113+ with WebGPU support and an available graphics adapter.

## Rebuild from source

The current build is already available in `docs/`. To rebuild it, install Rust, add the `wasm32-unknown-unknown` target, install `wasm-bindgen-cli` version `0.2.127`, and obtain the [Clean pack 2026-10-11 release](https://github.com/andrewnakas/skate3-cleanroom/releases/tag/clean-pack-2026-10-11). Extract the clean data locally, then run this from `engine/` in PowerShell:

```powershell
powershell -File tools/build_web.ps1 -Pack <extracted-pack-directory> -Out ../docs -DefaultMap StartPark
```

See `engine/docs/web.md` for the full technical documentation.

## Credits and licensing

See [`ATTRIBUTION.md`](ATTRIBUTION.md). This is an unofficial project and is not affiliated with EA. Skate and Skate 3 are trademarks of their respective owners. Attribution does not grant any additional license.
