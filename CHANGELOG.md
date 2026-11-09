# Changelog

What changed in each version of Eidolon, the newest first.

## 2026.11.4 (2026-11-09)

- **Albums you didn't choose are easy to tell apart.** Everywhere an album shows (the list, the tiles, the item's album line, the viewer, the album picker and the Albums page), an album you chose yourself or that one of your folder rules gives is filled with its colour. Every other album is an empty outline with a small icon saying where its name came from: a folder, the date it was taken, a trip, an event, screenshots and documents, or the month. Before, only guessed albums had a thin dashed line, which was hard to see, and screenshots_and_documents looked as if you had chosen it.
- **Thumbnails are always kept.** The **Clear all previews** button in the window is gone. It deleted the thumbnails too, and a thumbnail can only be made again from the original picture, so pictures on a drive that wasn't connected showed nothing. **Clear larger previews** still frees the space the viewer's larger pictures take. Thumbnails are now removed only with their scan, or when you reset the database.
- **Previews no longer pile up.** Previews of pictures that no scan has any more (deleted or edited since) are removed as soon as a scan ends, not only the next time Eidolon starts. The turned copies of thumbnails, made when you turn a photo, now count toward the space you allow for previews.
- **Show only photos or only videos.** The Pictures filter now has **Photos** and **Videos** beside Photos & videos. Live Photos count as photos; an item that is a photo with a separate video is listed under both. They combine with every other filter.
- **Counting how many people use Eidolon, without tracking anyone.** The daily look for a new version now also lets us count how many copies are in use each day and each month. It is still the same single request, with no identifier and nothing about you, your computer or your photos. Turning off **Look for new versions daily** (More ▾) turns this off too.
- **Albums named after folders are marked as guesses.** An album that only comes from the name of the folder a photo is in now looks like the other guessed albums, with a dashed outline, so you can tell it from the albums you named yourself. Albums your folder rules give still count as yours.
  - The **Guessed albums** filter lists them too. **Y** says the album is right and makes it yours.
  - In the album picker (**P**) and on the Albums page, album names you didn't choose have a dashed outline, and hovering over one says it is a guess and not an album you named.
  - Confirm many guesses at once, each item keeping its own guessed album (**Z** undoes each of these in one step):
    - On the Albums page, **Make it mine** takes a whole album. Tick several guessed albums (or all of them at once) and press **Make them mine**.
    - Select several items in the list or grid and press **Y**, or **Right albums** at the bottom.
    - **Put the list in an album…** has a new choice, **Each keeps its guessed album**, for everything the list shows.
- **Enter presses the highlighted button in Eidolon's window**, in its dialogs too, as on the review screen, and ticks or unticks a highlighted box. Holding it down presses it only once.
- **Notices no longer cover a dialog.** A notice in the middle of the review screen, such as the one saying a new version is out, now goes away when a dialog opens.
- **See what a new version brings before updating.** When a new version is out, its Update window lists what changed in every version since yours, newest first, so you can decide whether to update now. This works from the review screen and from Eidolon's own window.
  - Eidolon's window shows a few of the latest changes: those of the new version when one is out, with an **Update to …** button, otherwise those of the version you have.
  - **Full change log…** opens every version's changes, newest first, and works without an internet connection. On the review screen, **More ▾ → What's new** shows the same.
- **Move to another computer, or bring scans over.** Eidolon's window has a new row:
  - **Export…** saves your scans and all you did in them, with their thumbnails, in one file to take to the other computer.
  - **Replace with an export…** makes this computer's Eidolon the same as the exported one. What is here now is deleted for good, so it lists what goes first and only works once you type REPLACE.
  - **Add scans from an export…** adds the scans you pick to the ones here, with their groups and your decisions, names and albums. Titles, captions, locations, rotations and people's names you already wrote here stay as they are.
  - Folders that are somewhere else on this computer show as not connected until you locate them on the Scans page.
- **See and free the space Eidolon uses, from its window.** The window now shows how much space the database, the previews and the saved lists take, with three buttons:
  - **Clear larger previews…** removes the bigger pictures the viewer kept; they are made again when viewed.
  - **Clear all previews…** removes the thumbnails too, after warning that pictures on a drive that isn't connected show no picture until it is.
  - **Reset database…** deletes every scan and all you did in them, for good, and starts again empty. It lists what goes and what stays first, and only works once you type RESET. Your photos and the albums you extracted are never touched.
- **Photos on a drive that isn't connected.** Opening a picture whose drive is unplugged (or a network drive away, or a folder moved) now says so instead of "Couldn't load this picture", and shows the picture as it was last seen. Its details, title, caption, keep or drop and album can still be seen and changed as usual.
  - **Try again** once the drive is back; **Browse without it** shrinks the note to one line while you go on without the drive.
  - **Locate folder…** finds a folder mounted somewhere else (another drive letter, a renamed volume) and checks that it holds the same files before using it. Nothing is read again or scanned again. The Scans page marks such folders **Not connected** and offers the same.
  - A picture deleted from a folder that is still there says so too.
  - Extract checks first: if some files to extract are on a drive that isn't connected, it says which and lets you try again or extract the rest.
- **Previews take less space.** The larger pictures the viewer keeps so they open at once next time now stay within a size you choose on the Scans page (2 GB at first), letting go of those viewed least recently. Thumbnails always stay, so browsing never needs the originals. Previews of files no scan has any more are removed too.
- **Updating with Homebrew works again.** Update now on a copy installed with Homebrew could start the same version again without updating: it now fetches the new version first, and says so if Homebrew still doesn't have it. To update by hand, run `brew update` before `brew upgrade eidolon`.

## 2026.11.3 (2026-11-06)

- **List and grid, switched right above the list.** A List | Grid switch now sits on top of the list, with the sort order beside it (and By day in the grid), so the grid view is easy to find.
- **Review opens with no filters.** The first time, the list shows everything (Any · All · All, as Clear filters does) instead of only items with copies that aren't reviewed yet. After that it opens on the filters you used last.
- **Clearer Homebrew install.** It is shown as two steps: `brew tap hiro5id/eidolon`, then `brew install eidolon`.

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
