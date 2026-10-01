<div align="center">

# 🎮 PlayStation 1 Web Emulator

Emulador de PlayStation 1 (PSX) corriendo 100% en el navegador — core **mednafen_psx_hw** vía [EmulatorJS](https://emulatorjs.org/) (libretro/WASM). Sin instalación, sin backend: cargás tu ROM y tu BIOS y jugás.

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

**[▶️ Abrir demo en vivo](https://lautarosantiago.github.io/psx-web-emulator/)**

</div>

---

## ⚠️ Sobre el BIOS (importante)

Igual que la Nintendo DS, la PS1 **no tiene BIOS HLE**: el core necesita un dump real del BIOS de una PlayStation física (por ejemplo `scph5501.bin`, `scph1001.bin` o `scph7502.bin`, según región). Es propiedad de Sony, así que:

- Este repositorio **no lo incluye, no lo genera y no linkea de dónde bajarlo**.
- Tenés que dumpearlo vos mismo desde tu propia consola.
- Sin ese archivo el emulador no arranca — el botón "Cargar juego" queda deshabilitado hasta que subas la ROM y el BIOS.

## Características

- Corre 100% en el cliente, sin backend ni instalación.
- Carga manual de ROM (`.bin/.cue` multi-track, `.iso`, `.img`, `.chd`, `.pbp`, `.zip`) + BIOS desde el navegador; nunca se suben a ningún lado.
- **Multi-archivo**: podés seleccionar o arrastrar el `.cue` junto con todos sus `.bin` a la vez — se empaquetan solos en un zip en memoria.
- **Drag & drop**: arrastrá los archivos directo sobre la zona de carga en vez de usar el selector.
- **Validación de BIOS** por tamaño (512KB) con detección de región/versión por nombre de archivo, con checkbox para desactivarla si sabés que tu dump es válido igual.
- Controles por teclado (△ □ ○ ✕, D-pad, L1/R1/L2/R2, Start/Select), remapeables desde el menú del emulador.
- **Sticks analógicos virtuales** (arrastrables con mouse/touch), activables con un botón, además del D-pad digital.
- Pad digital transparente superpuesto a la pantalla (mouse/touch), visible también en fullscreen, con botones para agrandar/achicar.
- Botón x2 para activar/desactivar el avance rápido con un click.
- Barra de progreso mientras se prepara la carga.
- Guardado de partida (save states) persistente en el navegador, más botones para descargar/subir la memory card (.srm) desde el menú del emulador.

## Demo

👉 **https://lautarosantiago.github.io/psx-web-emulator/**

![Demo del emulador funcionando](assets/demo.gif)

> Para que este link funcione hay que activar GitHub Pages en el repo (Settings → Pages → Branch: `main` → carpeta `/root`). Ver instrucciones más abajo.

## Uso local

1. Cloná el repositorio:
   ```bash
   git clone https://github.com/LautaroSantiago/psx-web-emulator.git
   cd psx-web-emulator
   ```

2. Levantá un servidor local (no funciona abriendo el `index.html` directo por `file://`):
   ```bash
   python3 -m http.server 8000
   ```

3. Abrí `http://localhost:8000`, cargá tu ROM y tu BIOS, y tocá "Cargar juego".

## Controles por defecto

| Botón PS1 | Tecla |
|---|---|
| D-pad | Flechas ↑ ↓ ← → |
| Stick izquierdo | `F` `H` `T` `G` |
| Stick derecho | `J` `L` `I` `K` |
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
| Guardado rápido | `1` |
| Carga rápida | `2` |
| Cambiar slot | `3` |

Para remapear teclas: menú del emulador (ícono de engranaje) → **Control Settings**. También hay botón **"Mostrar controles en pantalla"**, **"Activar sticks analógicos"** y **"x2"** para avance rápido.

## Problemas comunes

- **Pantalla negra al cargar:** normalmente es un BIOS inválido o corrupto. Fijate el aviso de detección de BIOS debajo del selector de archivo, y probá con la validación de tamaño activada.
- **"Este archivo no parece un BIOS válido":** tu BIOS no pesa exactamente 512KB. Si estás seguro de que es un dump real de PS1 (algunos tienen padding distinto), destildá "Validar que el BIOS pese 512KB".
- **Audio cortado o con clicks:** común en emuladores web bajo carga alta de CPU — probá cerrar otras pestañas o bajar la resolución interna desde el menú del emulador (Video Settings).
- **El juego pide "modo analógico" y no reacciona:** activá los sticks virtuales con el botón correspondiente, o mapeá el modo analógico desde Control Settings si el juego lo requiere como botón explícito (el "ANALOG" físico del control no está mapeado por defecto).
- **Multi-track no carga bien:** confirmá que elegiste el `.cue` Y todos sus `.bin` juntos en la misma selección — si falta alguno, el `.cue` va a apuntar a un archivo que no está en el zip.

## Activar el demo con GitHub Pages

```bash
# en la raíz del repo, después de pushear a main
git checkout -b gh-pages
git push -u origin gh-pages
```

O desde GitHub: **Settings → Pages → Source: branch `main`, carpeta `/ (root)` → Save**. El link queda disponible en unos minutos en `https://lautarosantiago.github.io/psx-web-emulator/`.

## Nota sobre ROMs

Este repositorio **no incluye ni distribuye ROMs ni archivos de BIOS**. Solo funciona con archivos que el usuario ya posee legalmente. El `.gitignore` excluye las carpetas `roms/` y `bios/` y las extensiones típicas para evitar subirlas por error.

## Tecnología

- [EmulatorJS](https://emulatorjs.org/) — frontend web para RetroArch (core `mednafen_psx_hw`).
- [JSZip](https://stuk.github.io/jszip/) — empaqueta en memoria los archivos `.cue`+`.bin` multi-track antes de pasarlos al emulador.
- HTML / CSS / JavaScript vanilla, sin dependencias de build.

## Autor

<div align="left">

[![GitHub](https://img.shields.io/badge/GitHub-LautaroSantiago-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/LautaroSantiago)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Lautaro%20Subeldia-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/lautaro-subeldia/)

</div>

## Licencia

MIT — ver [LICENSE](LICENSE). No aplica a EmulatorJS ni a los cores de terceros que se cargan desde su CDN, ni a ninguna ROM o BIOS que el usuario utilice.
