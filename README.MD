<div align="center">

# ChickBeat

**A standalone Windows desktop tool for slicing full audio tracks into custom Counter-Strike 2 music kits.**

<br />

<a href="https://github.com/TYFALY/ChickBeat/releases/latest">
  <img src="https://img.shields.io/badge/Download_Latest_Release-ChickBeat.exe-E63946?style=for-the-badge&logo=windows&logoColor=white&labelColor=18181B" height="42" alt="Download Latest Release - ChickBeat.exe" />
</a>

<br />
<br />

[![Latest Release](https://img.shields.io/github/v/release/TYFALY/ChickBeat?style=flat-square&color=E63946&label=Latest%20Release)](https://github.com/TYFALY/ChickBeat/releases/latest)
[![Platform](https://img.shields.io/badge/Platform-Windows_x64-27272A?style=flat-square&logo=windows&logoColor=white)](https://github.com/TYFALY/ChickBeat/releases/latest)
[![Target](https://img.shields.io/badge/.NET-8.0_Single_File-512BD4?style=flat-square&logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/download)
[![Downloads](https://img.shields.io/github/downloads/TYFALY/ChickBeat/total?style=flat-square&color=2ea44f&label=Downloads)](https://github.com/TYFALY/ChickBeat/releases/latest)

</div>

---

## What it does

Instead of manually slicing and crossfading 10 separate audio cues in a DAW, you drop in a single `.mp3`, `.wav`, or `.flac` track. ChickBeat analyzes the track's audio profile, extracts the right sections for each game event, applies smooth fades, and exports a ready-to-use CS2 music kit folder.

---

## How it works

- **RMS Energy Profiling:** Scans the audio waveform to identify dynamic intensity across the whole track.
- **Dynamic Cue Selection:** Maps highest RMS energy peaks (drops, choruses) to high-impact events like MVP anthems and round starts, and lower energy sections (intros, verses, breakdowns) to deaths and menu ambience.
- **Raised-Cosine S-Curve Fades:** Applies S-curve fade-ins and fade-outs at stem boundaries to prevent audible clipping or pops during in-game state transitions.
- **Single Portable Binary:** Built with .NET 8 and Avalonia UI as a self-contained executable. No installation, runtimes, or loose DLLs required.
- **VAC Safe:** Operates strictly via CS2's official Game State Integration (GSI) and local files. It does not hook processes, inject code, or touch game memory.

---

## CS2 Stem Mapping

| Event Cue | Output File | Target Duration | Fade Setting | Selection Logic |
| :--- | :--- | :---: | :---: | :--- |
| **Main Menu** | `mainmenu.wav` |(Loopable) | 1.0s In / 1.0s Out | Mid-energy ambient verse or chorus |
| **Freeze Time** | `roundmvpanthem_01.wav` | 15s | 0.8s In / 0.5s Out | Intro or lower-energy build section |
| **Round Start** | `roundstart.wav` | 5s | Instant / 1.0s Out | Immediate impact transient or drop |
| **Round Action** | `roundaction.wav` | 30s | 1.0s In / 1.0s Out | Sustained rhythmic section |
| **Bomb Planted** | `bombplanted.wav` | 30s | 0.5s In / 0.8s Out | High-tension escalation section |
| **10-Sec Warning** | `round10sec.wav` | 10s | Instant / 0.3s Out | Fast tempo climax leading to defuse point |
| **MVP Anthem** | `roundmvpanthem.wav` | 7s | Instant / 1.2s Out | Highest RMS energy peak (main drop) |
| **Round Won** | `roundwon.wav` | 7s | 0.4s In / 1.0s Out | High-energy melodic resolution |
| **Round Lost** | `roundlost.wav` | 7s | 0.4s In / 1.0s Out | Breakdown or minor-key transition |
| **Player Death** | `deathcam.wav` | 5s | 0.2s In / 1.5s Out | Lowest RMS percentile section |

---

## How to use

1. **Download:** Get the latest `ChickBeat.exe` from the [Releases](https://github.com/TYFALY/ChickBeat/releases/latest) page.
2. **Import Track:** Drag and drop your audio file into the window (or click Browse). ChickBeat generates and previews each stem automatically.
3. **Export:** Click **Export Kit** to save the generated cues to your CS2 directory or custom kit folder.

> [!TIP]
> To mute default CS2 music kit audio in-game while keeping footsteps and team comms intact, open the game console (`~`) and enter:
> ```cfg
> snd_music_volume 0
> ```

---

## Star History

If this saved you time making custom kits, drop a star on the repo.

[![Star History Chart](https://api.star-history.com/svg?repos=TYFALY/ChickBeat&type=Date)](https://star-history.com/#TYFALY/ChickBeat&Date)

---

## License & Disclaimer

Counter-Strike, CS2, and Valve are registered trademarks of Valve Corporation. ChickBeat is an open-source project and is not affiliated with or endorsed by Valve Corporation.
