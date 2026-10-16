# Skate3Web

A lightweight WebAssembly build of `skate-3-rust-engine`, with a simplified interface and a static-site layout for GitHub Pages.

**GitHub Pages target:** https://igu2012.github.io/skate3web/ (Pages must be enabled for `main` / `/docs` in the repository settings.)

## Repository layout

- `engine/` — engine source based on the [`cleanroom-web` branch](https://github.com/andrewnakas/skate-3-rust-engine/tree/cleanroom-web). Its web flow uses a park carousel, a progressive loading screen, and direct entry into the game. The fullscreen button and on-screen touchscreen pad have been removed.
- `docs/` — prebuilt WebAssembly application and static files for GitHub Pages, including the nine parks from the clean-pack release.
- `engine/web/map-art.js` and `docs/map-art.js` — linked, real-gameplay/map photos for Start Park, Black Box Park, Maloof Money Cup, and Mega Park; other parks use original illustrative SVG previews until an exact photo is verified.
- `ATTRIBUTION.md` — project and asset provenance.

The park selector uses the blue, translucent menu treatment shown in the supplied Skate 3 reference, while retaining the simplified carousel. Four cards show a real Skate 3 map/gameplay photo linked to its source; these are retail-game reference images, not screenshots of this clean-room web build. Five other parks use clearly identified illustrative previews because an exact, attributable photo was not verified. The selector shows each map's title and download size in MB. The loading screen reports downloaded MB out of the total and starts the game automatically when loading is complete. Gameplay requires a keyboard or a physical controller; no touchscreen pad is provided. If WebGPU is unavailable, the browser displays a native dialog with troubleshooting steps and links.

No ISO or retail Skate 3 files are included. Optional mod ZIPs are not part of this package.

## Large files and pack chunks

The current core pack is `docs/core.pack` (about 94.7 MB). The build script splits any asset that exceeds its configured chunk size into `.partN` files, and `loader.js` downloads and concatenates those parts automatically. The current WASM binary and each map are also below GitHub's 100 MB per-file limit; no manual joining is required.

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
