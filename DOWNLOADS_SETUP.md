# Repository Structure & Release Guide — Datrix Software

## Your repository layout

| Repository | Contains | URL |
|---|---|---|
| **Datrix-Software** | Company website only | github.com/Sudhanshuk782/Datrix-Software |
| **CANStudio** | CAN Studio source + all releases | github.com/Sudhanshuk782/CANStudio |
| *TarkaMo* (create later) | TarkaMo source + releases | github.com/Sudhanshuk782/TarkaMo |

**Why separate?** Each product owns its own release stream. When you have four
products live, one shared release list would be an unmanageable mix of
`v1.1.0`, `v2.7.0`, `tarkamo-v1.0`, `modbus-v0.9` with no clear ownership.

**Do NOT move your existing v1.1.0 release.** GitHub cannot transfer releases
between repos — you would have to re-upload manually, and the old URL would
break for anyone who saved it. Leave it where it is.

---

## Where the website points

The download button on your website links to:

```
https://github.com/Sudhanshuk782/Datrix-Software/releases/latest/download/CANStudio_v2.7.0_Setup.exe
```

The `releases/latest/download/` path is a **permanent redirect** to your newest
release. Publish v2.8.0, v3.0.0, anything — the website link never changes,
**provided the filename stays exactly `CANStudio_Setup.exe`**.

This is why you should drop the version number from the installer filename.

---

## Publishing CAN Studio v2.7.0

### Step 1 — Build

```powershell
cd C:\path\to\CANStudio
python build\build_release.py --version 2.7.0 --notes "BLF/TRC support, J1939 decoding"
```

### Step 2 — Rename the installer

```powershell
cd dist
ren CANStudio_v2.7.0_Setup.exe CANStudio_Setup.exe
```

Do this every release. The website link then works forever without edits.

### Step 3 — Generate the checksum

```powershell
Get-FileHash CANStudio_Setup.exe -Algorithm SHA256
```

Copy the hash — corporate IT teams use it to whitelist your installer.

### Step 4 — Create the release

Go to: **https://github.com/Sudhanshuk782/Datrix-Software/releases/new**

| Field | Value |
|---|---|
| Choose a tag | Type `v2.7.0` → click "Create new tag: v2.7.0" |
| Target | `main` |
| Release title | `CAN Studio v2.7.0` |
| Description | See template below |
| Attach binaries | Drag `CANStudio_Setup.exe` into the box |

Tick **Set as the latest release**, then click **Publish release**.

---

## Release notes template

```markdown
## CAN Studio v2.7.0

Professional CAN log analysis for Windows 10 / 11.

### What's new since v1.1.0
- BLF (Vector) and TRC (PEAK) file reading
- J1939 / PGN automatic decoding
- Signal value-at-cursor readout on the waveform plot
- Rebuilt merge engine — zero frame loss on multi-message logs
- Professional UI, responsive from 1024px to 4K displays

### Installation
1. Download `CANStudio_Setup.exe` below
2. Run it. If Windows SmartScreen appears: **More info → Run anyway**
3. Launch from the Desktop shortcut — 10-day free trial starts automatically

### Requirements
Windows 10 / 11 (64-bit) · 8 GB RAM minimum · No Python needed

### Documentation
The full User Guide is supplied on request to trial users and licence holders.
Email **Sudhanshuk782@gmail.com** with your name and company.

### Licence
Free 10-day trial. Monthly and annual subscriptions available — email your
BIOS UUID (Help → Activate Licence) to receive a key.

### SHA-256
```
PASTE_YOUR_HASH_HERE
```
```

---

## What to do with the old v1.1.0 release

Leave it published. Optionally edit it to add a pointer:

1. Go to https://github.com/Sudhanshuk782/CANStudio/releases/tag/v1.1.0
2. Click **Edit release** (pencil icon)
3. Add at the top of the description:

```markdown
> ⚠️ **Superseded.** The current version is
> [v2.7.0](https://github.com/Sudhanshuk782/Datrix-Software/releases/latest)
> with BLF/TRC support and J1939 decoding.
```

4. Untick **Set as the latest release** if it is still ticked
5. Update release

---

## Future releases

```powershell
python build\build_release.py --version 2.8.0 --notes "..."
cd dist
ren CANStudio_v2.8.0_Setup.exe CANStudio_Setup.exe
Get-FileHash CANStudio_Setup.exe -Algorithm SHA256
```

Then GitHub → CANStudio repo → Releases → New release → tag `v2.8.0` →
attach → publish. **No website changes needed.**

---

## When TarkaMo launches (August 2026)

1. Create a new repo: `github.com/Sudhanshuk782/TarkaMo`
2. Publish releases there with filename `TarkaMo_Setup.exe`
3. In `index.html`, add a download link:
   ```
   https://github.com/Sudhanshuk782/TarkaMo/releases/latest/download/TarkaMo_Setup.exe
   ```
4. Remove the "Launching Independence Day" badge and swap in a live badge

---

## The User Guide PDF — deliberately not hosted

The guide documents every tab, control, and workflow. Published openly it
functions as a build specification for a competitor. It is supplied by email
on request instead.

### Reply template for guide requests

> Hi [Name],
>
> Thanks for your interest in CAN Studio. The User Guide is attached.
>
> Download the installer here:
> https://github.com/Sudhanshuk782/Datrix-Software/releases/latest
>
> The 10-day trial starts automatically on first launch — no registration
> needed. Any questions during evaluation, just reply to this email.
>
> Regards,
> Sudhanshu Kumar
> Datrix Software

---

## Website deployment recap

Push these four files to **Datrix-Software** repo root:

```
index.html
.nojekyll
DEPLOY.md
DOWNLOADS_SETUP.md
```

Then Settings → Pages → Branch `main` / `(root)` → Save.

Live at: **https://sudhanshuk782.github.io/Datrix-Software/**
