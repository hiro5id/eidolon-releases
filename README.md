Eidolon 2026.11.2
===

Eidolon finds the copies and Live Photo pairs (a still and its short video) in a photo and video library by how they look, not by their names. You review them in your browser, keep the best copy of each, and extract a tidy, well-named library. Your originals are never changed, and your photos never leave your computer.

## Install

| | Install | Update |
|---|---|---|
| **macOS, Linux** (Homebrew) | `brew install hiro5id/eidolon/eidolon` | `brew upgrade eidolon` |
| **Windows** (Scoop) | `scoop bucket add eidolon https://github.com/hiro5id/scoop-eidolon` then `scoop install eidolon` | `scoop update eidolon` |
| **macOS, Linux, Windows** (npm, Node 18 or newer) | `npm install -g @sebestyen/eidolon` (or try it with `npx @sebestyen/eidolon`) | `npm install -g @sebestyen/eidolon@latest` |
| **Docker** | `docker run` or Docker Compose, see [sebestyen/eidolon](https://hub.docker.com/r/sebestyen/eidolon) (compose example in [`docker/`](https://github.com/hiro5id/eidolon-releases/tree/main/docker)) | `docker compose pull && docker compose up -d` |
| **Download** | the file for your computer from [the latest release](https://github.com/hiro5id/eidolon-releases/releases/latest) | from the review screen (Windows: download it again) |

Then run `eidolon`: its window opens, says what it is doing and shows its log, and **Open** shows the review screen in a window of its own. **Quit** (there or in the review screen's **More ▾**) stops it. On a computer without a screen, or with `eidolon --no-window`, it runs in the terminal: open the address it prints (http://127.0.0.1:8765). The npm version downloads the program (about 370 MB) the first time it runs.

What changed in each version: [CHANGELOG.md](https://github.com/hiro5id/eidolon-releases/blob/main/CHANGELOG.md).

When a new version is out, the review screen says so and updates in one click (Docker: it shows the command). It looks once a day, with one request to GitHub that says nothing about your photos; **More ▾** turns it off, or `UPDATE_CHECK=0`.

### A downloaded file
Unpack `eidolon-<system>-<processor>.tar.gz` (Windows: `eidolon-windows-x86_64.zip`): a folder, `eidolon/`, with the program (`eidolon`, Windows `eidolon.exe`) and its libraries; keep them together. The programs aren't signed:
- **macOS** blocks it at first: run `xattr -dr com.apple.quarantine eidolon` once in the folder you unpacked it in, then `./eidolon/eidolon`.
- **Windows** SmartScreen warns: **More info → Run anyway**.

Homebrew, Scoop and npm don't need either. `SHA256SUMS` in each release lists every file's checksum.

## Credits
Place names: [GeoNames](https://www.geonames.org), [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Face detector: YuNet (OpenCV Zoo, MIT License). Text detector and recognizer: PP-OCRv3 and CRNN (OpenCV Zoo, Apache License 2.0). Same subject search: CLIP ViT-B/32 image encoder (OpenAI, MIT License).
