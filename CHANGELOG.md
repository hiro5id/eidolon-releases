# Changelog

What changed in each version of Eidolon, the newest first.

## 2026.11.2 (2026-11-06)

- **Updating stays on its "starting again" message until the new version is ready.** Every open tab is covered until it reloads by itself on the new version, even one opened at the last moment, so nothing can be changed or clicked in the meantime. Quitting covers every tab the same way.
- **Eidolon opens in a window of its own.** Started on a computer with a screen, it shows what it is doing from the first moment, its log as a terminal would, and buttons to open the review screen, copy its link and open its data folder. Started from a terminal, it hands the terminal back at once.
  - **Open Eidolon** shows the review screen in an app window of Chrome, Edge, Brave or Chromium when one is installed (no tabs, no address bar), else in your default browser; **Open in browser** opens it in a tab.
  - It can open the review screen by itself once it is ready (on at first), shows a running scan, extraction or check with its progress and a Stop button, says when a new version is out, and can record a diagnostic log (it starts again to do so).
  - Starting Eidolon again while it runs on the same library brings up the one already running instead of starting a second.
  - Without a screen (a server, SSH, Docker), or with `eidolon --no-window`, it runs in the terminal as before.
- **Quit** stops Eidolon cleanly, from its window or from the review screen (**More ▾ → Quit Eidolon**, not in Docker). A scan or other job running is stopped first, after asking; every open review page then says Eidolon has stopped.
- **Eidolon starts in about a second** instead of several: the download is now a folder (`eidolon/`, the program with its libraries) rather than a single file that unpacked itself at every start. Keep the folder's files together. On Windows, a copy downloaded by hand is updated by downloading the new version (Scoop, Homebrew and npm still update in one click).
- Scoop adds Eidolon to the Start menu.

## 2026.11.1 (2026-11-06)

No changes are listed for this version.

## 2026.11.0 (2026-11-05)

No changes are listed for this version.
