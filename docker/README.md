# Eidolon

**Your photo library, without the duplicates, and back in order.**

Ten years of photos end up in many places: the old phone's backup, the new phone's, a Google Takeout download, a laptop's Pictures folder copied to a USB drive "just in case", and photos sent back and forth over messaging apps. Merge them and you get the same picture five times under five names, as HEIC, JPEG and a blurry WhatsApp copy, with iPhone Live Photos split from their videos, and folders called `DCIM`, `Camera Roll` and `New folder (3)`. Finding duplicates by name doesn't work, because the names are all different.

Eidolon looks at the pictures themselves. It finds every copy of a picture, whatever its name, format or size, lets you review them in your browser, and extracts one clean, well-named library with the best copy of each.

## Sound familiar?

- **"I have the same photo three times, and I don't know which one to keep."** Eidolon groups the copies of a picture: other formats, resized, re-compressed, renamed, sent through a messaging app, cropped or straightened. It marks the best one (the original over a crop, then the most pixels, the camera's own file, the sharpest), and **Keep best** drops the rest in one go.
- **"My Live Photos came out of my iPhone as loose photos and short videos."** Eidolon pairs each still with its video again, exactly when they still carry Apple's Live Photo ID, by look when they don't, and exports them side by side under one name so photo apps can show them as one again.
- **"My phone filmed it sideways."** Turn a video upright, all of it or only the part filmed sideways, and it plays upright once exported. Photos lying on their side are found by the faces in them and turned upright for you, and you can turn any photo yourself.
- **"My backups overlap, and I've merged them so many times I've lost track."** Scan each one, combine the scans, and copies found across all of them group together. A scan done earlier isn't read again, and scanning again later only reads new or changed files.
- **"Half my library is junk."** Blank and black frames and accidental one-second videos are suggested for you to drop, and bursts of nearly identical shots are shown together with the sharpest marked. Nothing is dropped unless you say so.
- **"My folders are a mess."** Each picture goes into an album folder: the one you chose, else a folder name that means something (never `DCIM` or `100APPLE`), else the event or the trip it was taken on (`2019-06 Lisbon, Portugal`), else its month. When you choose an album, Eidolon suggests the likely ones first: those with photos taken the same day, at the same place, or looking like this one, each saying why. Screenshots and documents get a folder of their own and stay out of your photo groups.
- **"I can't find the photo I'm thinking of."** Search by name, place or caption, by what a picture shows ("dog", "beach"), by the words in it (a sign, a menu, a receipt), by who is in it, or by the weather that day ("snow"). Or search with a photo: show Eidolon one and it finds the same picture, or the same subject, with a slider for how alike they must be.
- **"I want to find everyone's photos by their name."** Eidolon gathers the faces in your photos by person. Name a person, and their photos are found by that name, which goes with the photos you export. If someone's faces end up in two places (sunglasses can do that), give both the same name and they become one person.
- **"I don't want to lose the captions, places and dates I added over the years."** What any copy of a picture knows (titles, captions, keywords, a Google Takeout file's details, where it was taken) goes with the copy you keep, in an `.xmp` file that photo apps read, with the place in words, the words read in the picture and the names of the people in it as keywords.
- **"Some of my old files might be damaged."** **Check files** reads each file again and finds the ones damaged since they were scanned (a failing drive, a copy cut short). **Repair** puts back the exact bytes scanned from another copy, from a backup or from the scan's own recovery data, and only when you ask.

## How it works

1. **Scan** the folders you want to clean up: drives, backups, exports. It works with hundreds of thousands of files.
2. **Review** the groups in your browser: keep or drop copies, move a photo to another group, choose albums, turn photos and videos, write titles and captions. Nothing happens to any file yet: Eidolon only remembers what you decided, and every change can be undone. It works with a keyboard, a mouse or a tablet's touch screen, even with the drive holding your originals unplugged.
3. **Extract** the files you kept into a new folder. Only now are files copied: one copy of each, in its album, with a clear name, turned and captioned as you left it.

**Your originals are never changed, moved or deleted**: Eidolon only reads them and writes the clean library somewhere else. The one exception is **Repair**, when you ask it to fix a damaged file. **Your photos never leave your computer**: places, faces, the text in pictures and what they show are all worked out on your computer. Only the weather, if you turn it on, asks a weather service (Open-Meteo) about the town and the day, never about a photo or where exactly it was taken. It runs on macOS, Windows and Linux, or in Docker on a server or NAS.

**Why a container?** If you'd rather not run a downloaded program directly on your computer, run it here. It sees only the folders you give it (your photos read-only), it can't change anything in itself, it runs as your user with no extra rights, and only your own computer can open its page.

Images: `linux/amd64` (Intel/AMD) and `linux/arm64` (Apple Silicon Macs, Raspberry Pi 4/5 with a 64-bit OS, ARM servers and NAS). Docker picks the right one.

---

## Quick start

### Linux and macOS

```bash
mkdir -p ~/eidolon/data ~/eidolon/export

docker run -d --name eidolon \
  --user "$(id -u):$(id -g)" \
  --read-only --tmpfs /tmp --cap-drop ALL --security-opt no-new-privileges \
  -p 127.0.0.1:8765:8765 \
  -v ~/eidolon/data:/data \
  -v ~/eidolon/export:/export \
  -v ~/Pictures:/photos:ro \
  sebestyen/eidolon

docker logs eidolon
```

The log ends with a link like `http://localhost:8765/?key=Xy3…`. **Open that link** (with its key) in your browser. Then choose **New scan**, pick a folder under `/photos`, and start.

> Create the `data` and `export` folders yourself first, as above. A folder that doesn't exist yet is created by Docker and owned by root, and then Eidolon can't write to it.

### Windows (PowerShell)

```powershell
docker run -d --name eidolon `
  --read-only --tmpfs /tmp --cap-drop ALL --security-opt no-new-privileges `
  -p 127.0.0.1:8765:8765 `
  -v eidolon-data:/data `
  -v "$env:USERPROFILE\eidolon-export:/export" `
  -v "$env:USERPROFILE\Pictures:/photos:ro" `
  sebestyen/eidolon

docker logs eidolon
```

Your database lives in the Docker volume `eidolon-data`, and extracted files appear in `eidolon-export` in your user folder.

### Stop, start, update

```bash
docker stop eidolon                 # stop it (your scans and decisions are kept in /data)
docker start eidolon                # start again; `docker logs eidolon` shows the new link
docker pull sebestyen/eidolon       # update: pull, then remove and re-create with the same command
docker rm -f eidolon
```

When a new version is out, the review screen says so (it looks once a day: one request to GitHub, nothing about your photos) and shows the command. A container can't update itself: with Docker Compose, `docker compose pull && docker compose up -d` in the folder of your `docker-compose.yml`; else the three commands above. Each version is also tagged by its number (`sebestyen/eidolon:2026.11.0`) to stay on one. To update by itself, a tool such as [Watchtower](https://github.com/containrrr/watchtower) can pull and re-create it.

---

## What each part of the command does

| Option | Why |
|---|---|
| `-v …:/photos:ro` | The folders to scan. **`:ro` = read-only**: Eidolon can't change, move or delete your originals. |
| `-v …:/export` | Where **Extract** copies the files you kept. Choose `/export` (or a folder in it) as the destination. |
| `-v …:/data` | The database: scans, groups, your decisions, captions, rotations. Keep it. Previews, scan logs and (if you ask for it) recovery data are stored next to it. |
| `-p 127.0.0.1:8765:8765` | The page is reachable only from **this computer**. |
| `--user "$(id -u):$(id -g)"` | Runs as you, so the files it writes are yours (Linux/macOS). |
| `--read-only --tmpfs /tmp` | Nothing in the image can be changed while it runs. |
| `--cap-drop ALL --security-opt no-new-privileges` | No special rights, and no way to gain any. |

The image itself contains only the program and the C libraries it needs: no shell, no package manager.

**The access key.** The page only answers a browser that opened its link with the key. The key is then kept in a cookie, so other web pages you have open can't use Eidolon behind your back. A new key is made at each start. To keep one (for bookmarks), set your own:

```bash
openssl rand -base64 24 | tr '+/' '-_'           # make a key once
docker run … -e ACCESS_KEY=the-key-you-made …    # then open http://localhost:8765/?key=the-key-you-made
```

The key must be at least 16 letters, digits, `-`, `_` or `.`.

---

## Choosing what to scan

Mount each folder you want under `/photos`, read-only:

```bash
  -v ~/Pictures:/photos/pictures:ro \
  -v /media/usb/camera-backup:/photos/camera:ro \
  -v /mnt/nas/photos:/photos/nas:ro \
```

The scan dialog's folder browser opens at `/photos`. A scan can cover several folders, and **Scan again** later finds what changed.

**Keep the mounts the same between runs.** Eidolon remembers files by their path inside the container (`/photos/camera/IMG_0001.JPG`). If you mount a folder somewhere else next time, it looks like a new folder and is read again.

**Tip:** if you also use the Eidolon desktop program, you can mount folders at the **same path** as on your computer (`-v /home/me/Pictures:/home/me/Pictures:ro -e HOME=/home/me/Pictures`). Paths then look the same in both.

---

## Scanning a network share (NAS, Windows share, NFS)

Eidolon doesn't connect to the share itself: that would need rights that undo the sandbox. **Docker mounts the share and Eidolon sees an ordinary read-only folder.** You can do this in three ways.

If the network drops during a scan, Eidolon retries and waits. Files on a share that isn't reachable show as "not available", never as missing or damaged.

### 1. SMB / CIFS: Windows shares, Synology, QNAP, TrueNAS, Samba

Create a Docker volume that mounts the share, then mount the volume into Eidolon:

```bash
docker volume create --driver local \
  --opt type=cifs \
  --opt device=//192.168.1.20/photos \
  --opt o=addr=192.168.1.20,username=me,password=secret,vers=3.0,ro,uid=$(id -u),gid=$(id -g) \
  nas-photos

docker run … -v nas-photos:/photos/nas:ro … sebestyen/eidolon
```

- Use the NAS's **IP address** (in both `device` and `addr`). The Docker host's kernel mounts the share, and it may not resolve names like `nas.local`.
- A password containing a comma doesn't work in `o=`. Give Eidolon its own **read-only account** on the NAS with a simple password: safer anyway.
- Older NAS: try `vers=2.1` or `vers=1.0`.
- The share is mounted when the container starts. If the password changes: `docker rm -f eidolon`, `docker volume rm nas-photos`, then create both again.

### 2. NFS

```bash
docker volume create --driver local \
  --opt type=nfs \
  --opt o=addr=192.168.1.20,nfsvers=4,ro \
  --opt device=:/volume1/photos \
  nas-photos

docker run … -v nas-photos:/photos/nas:ro … sebestyen/eidolon
```

The NAS must allow NFS access from the Docker host's address.

### 3. A share your computer already has open

If the share is already mounted on your computer, mount that folder like any other:

```bash
-v /mnt/nas/photos:/photos/nas:ro                # Linux: fstab, autofs
-v /Volumes/photos:/photos/nas:ro                # macOS: connected in Finder
```

- **macOS (Docker Desktop):** Docker can see `/Volumes/…` only if it's allowed under *Settings → Resources → File sharing*. Otherwise use route 1.
- **Windows:** Docker Desktop can't see mapped drive letters (`Z:`). Use route 1 with the share's address.

### Troubleshooting

| Message | What to check |
|---|---|
| `mount error(13): Permission denied` | User name and password; try another `vers=`. |
| `mount error(2)` / `No such file or directory` | The share's name in `device=` (`//IP/share`, or `:/exported/path` for NFS). |
| `mount error(112)` / host is down | The Docker host must reach the NAS. With Docker Desktop, that's the Docker VM. |
| Folder is empty | The account can't read the share, or the wrong share or path was given. |

---

## Docker Compose

A ready-to-edit setup, with SMB and NFS blocks to uncomment: [`docker/docker-compose.yml`](https://github.com/hiro5id/eidolon-releases/blob/main/docker/docker-compose.yml) and [`docker/.env.example`](https://github.com/hiro5id/eidolon-releases/blob/main/docker/.env.example).

```bash
# in a folder with docker-compose.yml and .env (from .env.example, filled in)
mkdir -p data export
docker compose up -d
docker compose logs          # the link
```

The SMB/NFS settings (address, share, user, password) go in `.env`, not in the compose file or your shell history.

---

## Other settings

| Setting | Default | |
|---|---|---|
| `-p 127.0.0.1:9000:8765 -e PUBLIC_URL=http://localhost:9000` | port 8765 | Another port on your computer. `PUBLIC_URL` is the address the printed link uses. |
| `-e ACCESS_KEY=…` | new each start | A fixed key (see above). |
| `-e HOME=/photos/camera` | `/photos` | Where the folder browser opens. |
| `-e UPDATE_CHECK=0` | on | Never look for new versions (also **More ▾ → Look for new versions daily**). |
| `-e DIAGNOSTICS=1` | off | Record a diagnostic log, to send when something is slow or goes wrong: in `/data/diagnostics/` (and each scan's in `/data/scan-logs/`), or in one zip from the page's **More ▾ → Download diagnostics**. It names your files and folders, never what's in your photos. |

### Using it from other computers

```bash
docker run … -p 8765:8765 -e PUBLIC_URL=http://my-computer.local:8765 … sebestyen/eidolon
```

Anyone with the link and its key can see your photos. The connection isn't encrypted (plain HTTP). Do this only on a network you trust, or put Eidolon behind a reverse proxy with HTTPS. To reach it from a laptop, an SSH tunnel also works: `ssh -L 8765:localhost:8765 my-computer`.

---

## Good to know

- **Your originals are never changed.** A scan only reads them. Extraction copies to `/export`. The only exception is **Repair**, which restores a file that got damaged on disk, and only when you ask. It can't write into a `:ro` folder: to repair, mount that folder without `:ro` for that run.
- **Open** and **Show in folder** do nothing in a container: there's no desktop to open files on. Use **Download**, or open the files on your computer.
- Scanning is heavy work: it reads several files at once on all processor cores. To keep your computer responsive, cap the container with `--cpus 4 --memory 8g`. Eidolon fits its work into the memory limit you set.
- Keep `/data` on a different drive than your photos. If you turn on **recovery data** for a scan, it can then repair photos even after their drive fails.

---

## Versions

Tags: `latest`, and each release's version (`2026.11.0`, `2026.11.1`…) if you want to pin one. What each release brings and the other ways to install: [hiro5id/eidolon-releases](https://github.com/hiro5id/eidolon-releases).

---

## Credits

Place names: [GeoNames](https://www.geonames.org), [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Weather (if you turn it on): [Open-Meteo](https://open-meteo.com), [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Face detector (finds sideways photos): YuNet, OpenCV Zoo, MIT License. Face recognizer (People): SFace, OpenCV Zoo, Apache License 2.0. Text detector and recognizer: PP-OCRv3 and CRNN, OpenCV Zoo, Apache License 2.0. Search with a photo (same subject) and what pictures show: CLIP ViT-B/32 image encoder, OpenAI, MIT License. The model licenses are in the image under `/opt/eidolon/licenses/`.
