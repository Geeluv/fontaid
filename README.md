# Fontaid

A simple Windows desktop app that installs fonts straight from ZIP archives,
no more unzip → open folder → select fonts → install one-by-one.

## What it does

1. You add one or more `.zip` files (however they came from the font site — nested
   folders inside the zip are fine, Fontaid searches all of them).
2. You choose **OpenType (.otf)**, **TrueType (.ttf)**, or **Both**.
3. Click **Install Fonts**. Fontaid extracts the zips, filters to the type you
   picked, copies the matching font files into your personal Windows font
   folder, registers them, and refreshes the font cache, all without an
   admin/UAC prompt.
4. New fonts appear right away in apps like Word, Photoshop, Illustrator, etc.
   (some apps may need a restart to see them).

Fonts are installed **for your Windows user account only** (not system-wide for
all users on the PC). That's what lets it run without admin rights and without
interrupting your workflow. It's the same mechanism Windows itself uses when
you right-click a font file and choose "Install."

## Requirements

- Windows 10 or 11
- Python 3.9+ (from [python.org](https://python.org). Check "Add to PATH" during install)
- `tkinter` — included with the standard Python Windows installer by default

Optional but recommended, for accurate font names in the install list:

```
pip install fonttools
```

Without `fonttools`, Fontaid still installs fonts correctly. it just falls
back to naming them from the filename instead of reading the font's real name.

## Easiest setup: get a real fontaid.exe on your Desktop

1. Make sure `fontaid.py` and `Install Fontaid.bat` are in the **same folder**.
2. Double-click **`Install Fontaid.bat`**.
3. Click **Yes** on the Windows permission prompt (it needs this once, to install
   the build tools properly. Fontaid itself never needs admin rights to run).
4. If Python isn't on your PC yet, the installer will open the official
   python.org download page for you. Install Python (check **"Add python.exe
   to PATH"** on the install screen), then double-click `Install Fontaid.bat`
   again.
5. Wait about a minute while it builds. When it's done, you'll have a real
   **`fontaid.exe`** sitting on your Desktop. Double-click it any time to
   run Fontaid. No Python knowledge needed after this point.

You can delete `Install Fontaid.bat`, `fontaid.py`, and `requirements.txt`
afterward if you like — `fontaid.exe` on your Desktop is fully self-contained.

## Running it without building an .exe (alternative)

If you'd rather just run the Python script directly instead of building an
.exe, double-click `run_fontaid.bat`, or from a terminal:

```
python fontaid.py
```

## App icon

`fontaid.ico` (used as the .exe's icon and the app window icon) and
`fontaid_logo.png` (a high-res PNG for anywhere else you need the logo) are
included. The installer already embeds `fontaid.ico` into the .exe for you —
just make sure it stays in the same folder as `fontaid.py` when you run
`Install Fontaid.bat`.

## Getting your download page live

`fontaid_download_page.html` is a single, self-contained download page for
Fontaid, branded for Fortis G Studios / Chinenova Synergy LTD. Two things to
fill in before you publish it:

1. **The download link.** Right now the button points to `fontaid.exe` as a
   relative link. Upload `fontaid.exe` next to the HTML file on your host
   (or update the `href` in the `<a class="btn-download">` tag to wherever
   you end up hosting the file — GitHub Releases, itch.io, or your own site).
2. **The SHA-256 hash.** Every time you build a new `fontaid.exe`,
   `Install Fontaid.bat` now automatically prints the file's SHA-256 hash
   and saves it to `fontaid_hash.txt`. Copy that value into
   `fontaid_download_page.html`, replacing the placeholder text
   `PASTE-YOUR-FONTAID-EXE-SHA256-HASH-HERE` (search for it — it appears once).

Then upload `fontaid_download_page.html` and `fontaid.exe` to your host of
choice (GitHub Releases, itch.io, or a page on your own site) and share the
page's link.

## Notes

- If a font file with the same name is already installed, Fontaid skips it
  and tells you in the log rather than overwriting it.
- Corrupted or non-ZIP files are reported in the log rather than crashing
  the app.
- To uninstall a font Fontaid installed, use Windows Settings → Personalization →
  Fonts, find it, and remove it as usual — Fontaid doesn't touch anything
  outside the normal per-user font mechanism, so standard uninstall works fine.
