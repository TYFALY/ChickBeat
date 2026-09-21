# Security Policy

## Supported Versions

Only the latest release of ChickBeat receives security updates and hotfixes.

| Version | Supported          |
| ------- | ------------------ |
| Latest   | :white_check_mark: |
| < 1.1.0 | :x:                |

## Anti-Cheat Compliance & Security Model

ChickBeat interacts with Counter-Strike 2 strictly through Valve's official **Game State Integration (GSI)** HTTP engine.

- **No Memory Hooking:** ChickBeat does not attach to `cs2.exe`, inject DLLs, or read/write game process memory.
- **No File Modification:** ChickBeat never alters game binaries, VPK archives, or protected game files.
- **VAC Safety:** GSI is a documented Valve feature where the game client sends local HTTP POST requests to an external listener port. It carries zero risk of triggering a VAC ban.

## Binary Verification & False Positives

Official release binaries published on GitHub Releases are single-file, self-contained `.NET 8` executables. Because ChickBeat is an unsigned community executable:

- **Windows SmartScreen:** Unsigned binaries without expensive EV Code Signing Certificates will trigger a default Windows SmartScreen warning until download reputation builds.
- **Antivirus Heuristics:** Single-file runtime extraction and automated tool fetches (`yt-dlp` / `ffmpeg`) into `%AppData%` may trigger behavioral false positives in some security software.

Always verify your local binary hash against the SHA-256 hash provided in the VirusTotal scan report attached to each release:

```powershell
Get-FileHash .\ChickBeat.exe -Algorithm SHA256
