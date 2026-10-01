<div align="center">

# 🎮 PlayStation 1 Web Emulator

PlayStation 1 (PSX) emulator running 100% in the browser — **mednafen_psx_hw** core via [EmulatorJS](https://emulatorjs.org/) (libretro/WASM). No installation or backend: load your ROM and BIOS and play.

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

**[▶️ Open live demo](https://lautarosantiago.github.io/psx-web-emulator/)**

</div>

---

## ⚠️ About the BIOS (important)

Like the Nintendo DS, the PS1 **does not have an HLE BIOS**: the core needs a real BIOS dump from a physical PlayStation (for example `scph5501.bin`, `scph1001.bin`, or `scph7502.bin`, depending on region). It is owned by Sony, so:

- This repository **does not include it, generate it, or link to where to download it**.
- You must dump it yourself from your own console.
- Without that file the emulator will not start — the "Load Game" button remains disabled until you provide the ROM and BIOS.

## Features

- Runs 100% on the client, with no backend or installation.
- Manually loads ROMs (`.bin/.cue` multi-track, `.iso`, `.img`, `.chd`, `.pbp`, `.zip`) + BIOS from the browser; they are never uploaded anywhere.
- **Multi-file**: you can select or drag the `.cue` together with all of its `.bin` files at once — they are automatically packed into an in-memory zip.
- **Drag & drop**: drag files directly onto the loading area instead of using the file picker.
- **BIOS validation** by size (512KB), with region/version detection by file name and a checkbox to disable validation if you know your dump is valid anyway.
- Keyboard controls (△ □ ○ ✕, D-pad, L1/R1/L2/R2, Start/Select), remappable from the emulator menu.
- **Virtual analog sticks** (draggable with mouse/touch), enabled with a button, in addition to the digital D-pad.
- Transparent digital pad overlaid on the screen (mouse/touch), also visible in fullscreen, with buttons to enlarge/shrink it.
- x2 button to toggle fast-forward with one click.
- Progress bar while the files are being prepared.
- Persistent save states in the browser, plus buttons to download/upload the memory card (.srm) from the emulator menu.

## Demo

👉 **https://lautarosantiago.github.io/psx-web-emulator/**

![Emulator demo](assets/demo.gif)

> For this link to work, enable GitHub Pages in the repository (Settings → Pages → Branch: `main` → `/root` folder). See the instructions below.

## Local Usage

1. Clone the repository:
   ```bash
   git clone https://github.com/LautaroSantiago/psx-web-emulator.git
   cd psx-web-emulator
   ```

2. Start a local server (opening `index.html` directly via `file://` will not work):
   ```bash
   python3 -m http.server 8000
   ```

3. Open `http://localhost:8000`, load your ROM and BIOS, and click "Load Game".

## Default Controls

| PS1 Button | Key |
|---|---|
| D-pad | Flechas ↑ ↓ ← → |
| Left Stick | `F` `H` `T` `G` |
| Right Stick | `J` `L` `I` `K` |
| ✕ (Cross) | `X` |
| ○ (Circle) | `Z` |
| □ (Square) | `S` |
| △ (Triangle) | `A` |
| L1 | `Q` |
| R1 | `E` |
| L2 | `Tab` |
| R2 | `R` |
| Start | `Enter` |
| Select | `V` |
| Quick Save | `1` |
| Quick Load | `2` |
| Change Slot | `3` |

To remap keys: emulator menu (gear icon) → **Control Settings**. There are also **"Show On-Screen Controls"**, **"Enable Analog Sticks"**, and **"x2"** buttons for fast-forward.

## Common Problems

- **Black screen when loading:** this is usually caused by an invalid or corrupted BIOS. Check the BIOS detection message below the file selector and try with size validation enabled.
- **"This file does not appear to be a valid BIOS":** your BIOS is not exactly 512KB. If you are sure it is a real PS1 dump (some have different padding), disable "Validate that the BIOS is 512KB".
- **Choppy audio or clicks:** common in web emulators under high CPU load — try closing other tabs or lowering the internal resolution from the emulator menu (Video Settings).
- **The game asks for "analog mode" and does not respond:** enable the virtual sticks with the corresponding button, or map analog mode from Control Settings if the game requires it as an explicit button (the physical "ANALOG" controller button is not mapped by default).
- **Multi-track does not load correctly:** make sure you selected the `.cue` AND all of its `.bin` files together in the same selection — if any are missing, the `.cue` will point to a file that is not in the zip.

## Enable the Demo with GitHub Pages

```bash
# from the repository root, after pushing to main
git checkout -b gh-pages
git push -u origin gh-pages
```

Or from GitHub: **Settings → Pages → Source: branch `main`, folder `/ (root)` → Save**. The link will become available within a few minutes at `https://lautarosantiago.github.io/psx-web-emulator/`.

## ROM Note

This repository **does not include or distribute ROMs or BIOS files**. It only works with files the user already legally owns. The `.gitignore` excludes the `roms/` and `bios/` folders and common file extensions to prevent accidental uploads.

## Technology

- [EmulatorJS](https://emulatorjs.org/) — frontend web para RetroArch (core `mednafen_psx_hw`).
- [JSZip](https://stuk.github.io/jszip/) — packs multi-track `.cue`+`.bin` files in memory before passing them to the emulator.
- Vanilla HTML / CSS / JavaScript, with no build dependencies.

## Author

<div align="left">

[![GitHub](https://img.shields.io/badge/GitHub-LautaroSantiago-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/LautaroSantiago)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Lautaro%20Subeldia-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/lautaro-subeldia/)

</div>

## License

MIT — see [LICENSE](LICENSE). It does not apply to EmulatorJS or third-party cores loaded from its CDN, nor to any ROM or BIOS used by the user.
