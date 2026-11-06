Eidolon 2026.11.2
===

**Your photo library, without the duplicates, and back in order.**

Ten years of photos end up in many places: the old phone's backup, the new phone's, a Google Takeout download, a laptop's Pictures folder copied to a USB drive "just in case", and photos sent back and forth over messaging apps. Merge them and you get the same picture five times under five names, as HEIC, JPEG and a blurry WhatsApp copy, with iPhone Live Photos split from their videos, and folders called `DCIM`, `Camera Roll` and `New folder (3)`. Finding duplicates by name doesn't work, because the names are all different.

Eidolon looks at the pictures themselves. It finds every copy of a picture, whatever its name, format or size, lets you review them in your browser, and extracts one clean, well-named library with the best copy of each.

## Sound familiar?

- **"I have the same photo three times, and I don't know which one to keep."** Eidolon groups the copies of a picture: other formats, resized, re-compressed, renamed, sent through a messaging app, cropped or straightened. It marks the best one (the original over a crop, then the most pixels, the camera's own file, the sharpest), and **Keep best** drops the rest in one go.
- **"My Live Photos came out of my iPhone as loose photos and short videos."** Eidolon pairs each still with its video again, exactly when they still carry Apple's Live Photo ID, by look when they don't, and exports them side by side under one name so photo apps can show them as one again.
- **"My backups overlap, and I've merged them so many times I've lost track."** Scan each one, combine the scans, and copies found across all of them group together. A scan done earlier isn't read again, and scanning again later only reads new or changed files.
- **"Half my library is junk."** Blank and black frames, accidental one-second videos and bursts of twelve nearly identical shots are suggested for you to drop. Nothing is dropped unless you say so.
- **"My folders are a mess."** Each picture goes into an album folder: the one you chose, else a folder name that means something (never `DCIM` or `100APPLE`), else the event or the trip it was taken on (`2019-06 Lisbon, Portugal`), else its month. Screenshots and documents get a folder of their own.
- **"I don't want to lose the captions, places and dates I added over the years."** What any copy of a picture knows (titles, captions, keywords, a Google Takeout file's details, where it was taken) goes with the copy you keep, in an `.xmp` file that photo apps read. Photos are turned upright for every app.
- **"Some of my old files might be damaged."** **Check files** reads each file again and finds the ones damaged since they were scanned (a failing drive, a copy cut short). **Repair** puts back the exact bytes scanned from another copy, from a backup or from the scan's own recovery data, and only when you ask.

## How it works

1. **Scan** the folders you want to clean up: drives, backups, exports. It works with hundreds of thousands of files.
2. **Review** the groups in your browser: keep or drop copies, move a photo to another group, choose albums, write titles and captions. Every change happens at once and can be undone. Search by name, place, caption or text in the picture, or search with a photo to find the same subject. It works with a keyboard, a mouse or a tablet's touch screen, even with the drive holding your originals unplugged.
3. **Extract** the files you kept into a new folder: one exact copy of each, in its album, with a clear name.

**Your originals are never changed, moved or deleted**: Eidolon only reads them and writes the clean library somewhere else. **Your photos never leave your computer**: places are looked up offline, and faces and text in pictures are found on your computer too. It runs on macOS, Windows and Linux, or in Docker on a server or NAS.

## Install

| | Install | Update |
|---|---|---|
| **macOS, Linux** (Homebrew) | `brew tap hiro5id/eidolon` then `brew install eidolon` | `brew upgrade eidolon` |
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
