# Avatar Toolbox

**A small Windows dashboard for launching your tools and checking their status.**

[**▶ Project page on caseyshingledecker.com**](https://caseyshingledecker.com/desktop-tools.html#avatar-toolbox) · [**Source**](https://github.com/Beebopcat/avatar-toolbox)

![Desktop Tools page at the Avatar Toolbox card, with its feature list and View source and Source releases links.](docs/media/site-01.webp)

### Why it matters

IT-support tooling in PowerShell 5.1 and WPF: one small window that starts, stops and health-checks your tools (process and HTTP status checks), and that opens guided repair helpers (for example a graphics reset and the `sfc /scannow` and `DISM` repair steps). Risky actions ask first, only the deep scan asks for administrator permission, and nothing runs until you click.

**Stack:** PowerShell 5.1, WPF, Python (`build_toolbox.py` generator), JSON configuration (`tools.json`).

### Proof

- **Built-in self-test, run on Windows 11 with Windows PowerShell 5.1:** 2 PASS, 0 FAIL, plus 1 informational line. It checks that `tools.json` loads and that the configured tool file exists; it does not test the repair actions.
- All four PowerShell scripts I parsed (`Avatar-Toolbox.ps1`, both templates and `scripts/Backup-Settings.ps1`) have 0 parse errors, and a headless `-Snapshot` render of the repair panel completed.
- Screenshots: the project-page capture above and the public-edition preview below.

### Quick start

```powershell
git clone https://github.com/Beebopcat/avatar-toolbox.git
cd avatar-toolbox
powershell.exe -NoProfile -STA -File Avatar-Toolbox.ps1                       # open the toolbox
powershell.exe -NoProfile -STA -File Avatar-Toolbox.ps1 -SelfTest result.txt  # run the self-test
```

### Limitations

- Windows only (PowerShell 5.1 and WPF). The self-test's file check expects OCR Boxes at the path in `tools.json`; change that path if you installed it elsewhere, or the check reports a failure.
- No repair action was run as part of testing, and repairs can change Windows settings, so review each one before you use it.
- The public edition ships a neutral vector mascot and no avatar artwork. The self-test is a small smoke test, not a full test suite.
- Built with AI-assisted development.

---

## What it is

A small Windows PowerShell 5.1 / WPF dashboard for launching tools, checking their status and opening optional repair helpers. OCR Boxes is first in the tool list.

## Screenshots

![Desktop Tools page at the Avatar Toolbox card, with its feature list and View source and Source releases links.](docs/media/site-01.webp)

<sub>Desktop Tools page at the Avatar Toolbox card, with its feature list and View source and Source releases links.</sub>

![Preview of the public Avatar Toolbox: a neutral vector mascot between buttons for My tools and checks, Start all my tools, PC repair and fixes and Choose avatar.](preview.png)

<sub>Preview of the public edition (`preview.png`): the original neutral vector mascot.</sub>

## How to use

1. Run `powershell.exe -NoProfile -STA -File Avatar-Toolbox.ps1`. Nothing starts automatically in the supplied configuration.
2. Edit `tools.json` to list your own tools (fields: id, name, info, hotkeys, kind `ahk`/`python`/`service`, path or exe and args, healthUrl and stopUrl, log, autostart).
3. To change the generated script, edit the templates `source/hub.template.ps1` and `source/repair.template.ps1`, then rebuild with `python source/build_toolbox.py`.
4. Review each repair action and its confirmation before using it; repairs can change Windows settings.

## Features

- Start and stop controls plus read-only status checks for each tool
- Optional repair helpers
- An avatar picker; the public edition uses an original neutral vector mascot when no avatar artwork is installed
- Manual startup and portable per-user paths
- Charcoal panels with cream, warm text matching Kokoro Player

## The story behind it

The public edition is dated 2026-10-20. It derives from a personal always-on-top toolbox widget that combined the author's tools with automated checks, repairs and a companion picker; the public edition swaps in a neutral mascot. OCR Boxes is first in the tool list, and its path resolves to the copy bundled with Desktop Pixel Companions; change it if you installed OCR Boxes elsewhere.

## Built with

- PowerShell 5.1
- WPF
- Python (`build_toolbox.py` generator)
- `tools.json` configuration

## Run it locally

Requires Windows with PowerShell 5.1.

```powershell
git clone https://github.com/Beebopcat/avatar-toolbox.git
cd avatar-toolbox
powershell.exe -NoProfile -STA -File Avatar-Toolbox.ps1
```

## Validation and scope

The local edition passed PowerShell parsing and six file-presence checks, with five informational status results and no failures. These checks do not validate every repair action. No repair, service restart or audio playback was performed as part of release preparation.

## Credits & disclaimers

Original project source is published for inspection; no additional source license or third-party character-art rights are granted by this repository. Personal character art, settings, reports and voice models are excluded.

Built by Casey Shingledecker with AI-assisted development.

## More projects

- Portfolio and live demos: https://caseyshingledecker.com/
- All repositories: https://github.com/Beebopcat

## License

Copyright (c) 2026 Casey Shingledecker. All rights reserved. Source-available for viewing and for personal, non-commercial running only; this is not open source. See [LICENSE](LICENSE). Other people's material keeps its own license.
