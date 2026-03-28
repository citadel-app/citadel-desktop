<p align="center">
  <img src="resources/icon.png" width="120" alt="Citadel Logo" />
</p>

<h1 align="center">Citadel Desktop</h1>

<p align="center">
  <strong>A hackable second brain for software developers.</strong><br/>
  Knowledge management, AI-powered writing, and deep code integration — all in one workspace.
</p>

<p align="center">
  <a href="https://github.com/citadel-app/citadel-desktop/releases/latest"><img src="https://img.shields.io/github/v/release/citadel-app/citadel-desktop?style=flat-square&color=5C6BC0" alt="Latest Release" /></a>
  <a href="https://github.com/citadel-app/citadel-desktop/releases"><img src="https://img.shields.io/github/downloads/citadel-app/citadel-desktop/total?style=flat-square&color=26A69A" alt="Total Downloads" /></a>
  <a href="https://github.com/citadel-app/citadel-desktop/blob/main/LICENSE"><img src="https://img.shields.io/github/license/citadel-app/citadel-desktop?style=flat-square" alt="License" /></a>
</p>

---

## Download

Choose the installer for your platform. All binaries are unsigned — you may need to allow the app through your OS gatekeeper on first launch.

<!-- INSTALLERS:START -->
### Latest Release: v1.1.5

| Platform | Architecture | Download | Size |
|:---------|:-------------|:---------|-----:|
| 🪟 **Windows** | ARM64 | [citadel-1.1.5-arm64-portable.exe](https://github.com/citadel-app/citadel-desktop/releases/download/v1.1.5/citadel-1.1.5-arm64-portable.exe) | 127 MB |
| 🪟 **Windows** | x64 | [citadel-1.1.5-portable.exe](https://github.com/citadel-app/citadel-desktop/releases/download/v1.1.5/citadel-1.1.5-portable.exe) | 248 MB |
| 🪟 **Windows** | x64 | [citadel-1.1.5-x64-portable.exe](https://github.com/citadel-app/citadel-desktop/releases/download/v1.1.5/citadel-1.1.5-x64-portable.exe) | 121 MB |
| 🍎 **macOS** | Apple Silicon | [citadel-1.1.5-arm64.dmg](https://github.com/citadel-app/citadel-desktop/releases/download/v1.1.5/citadel-1.1.5-arm64.dmg) | 158 MB |
| 🍎 **macOS** | Universal | [citadel-1.1.5-universal.dmg](https://github.com/citadel-app/citadel-desktop/releases/download/v1.1.5/citadel-1.1.5-universal.dmg) | 235 MB |
| 🍎 **macOS** | Intel | [citadel-1.1.5-x64.dmg](https://github.com/citadel-app/citadel-desktop/releases/download/v1.1.5/citadel-1.1.5-x64.dmg) | 162 MB |
| 🐧 **Linux** | x86_64 (deb) | [citadel-1.1.5-amd64.deb](https://github.com/citadel-app/citadel-desktop/releases/download/v1.1.5/citadel-1.1.5-amd64.deb) | 122 MB |
| 🐧 **Linux** | ARM64 (AppImage) | [citadel-1.1.5-arm64.AppImage](https://github.com/citadel-app/citadel-desktop/releases/download/v1.1.5/citadel-1.1.5-arm64.AppImage) | 163 MB |
| 🐧 **Linux** | ARM64 (deb) | [citadel-1.1.5-arm64.deb](https://github.com/citadel-app/citadel-desktop/releases/download/v1.1.5/citadel-1.1.5-arm64.deb) | 118 MB |
| 🐧 **Linux** | x86_64 (AppImage) | [citadel-1.1.5-x86_64.AppImage](https://github.com/citadel-app/citadel-desktop/releases/download/v1.1.5/citadel-1.1.5-x86_64.AppImage) | 162 MB |
<!-- INSTALLERS:END -->

<details>
<summary><strong>Which file should I download?</strong></summary>

| Platform | Recommended | Notes |
|:---------|:------------|:------|
| **Windows** | `portable.exe` | No installation required, just download and run |
| **Windows** | `setup.exe` | NSIS based installer |
| **macOS (Apple Silicon)** | `arm64.dmg` | For M1/M2/M3/M4 Macs |
| **macOS (Intel)** | `x64.dmg` | For older Intel-based Macs |
| **macOS (Universal)** | `universal.dmg` | Works on both Apple Silicon and Intel |
| **Linux** | `.AppImage` | Portable, works on most distributions |
| **Linux (Debian/Ubuntu)** | `.deb` | Native package manager integration |

</details>

---

## Architecture

This repository is the **packaging and distribution shell** for [Citadel](https://github.com/citadel-app/citadel). It does not contain application source code — it consumes the pre-built `citadel-payload.zip` from the monorepo and wraps it with Electron Builder for each platform.

```
citadel (monorepo)          →  builds app code, publishes @citadel-app/app
  ↓ triggers
citadel-desktop (this repo) →  packages into platform installers, publishes releases
```

### Build Pipeline

1. A new release in `citadel-app/citadel` triggers the `Build Desktop App` workflow
2. The workflow downloads the latest `citadel-payload.zip` (containing the pre-built `out/` directory)
3. Electron Builder packages the payload into platform-specific installers across 3 OS runners
4. All artifacts are uploaded to a draft GitHub Release for review

### Auto-Updates

Production builds support auto-updates via `electron-updater`. The updater checks this repository's releases for new versions and downloads full binary replacements.

---

## Development

```bash
# Install dependencies
npm install --legacy-peer-deps

# Build for your platform
npm run build:win    # Windows
npm run build:mac    # macOS (universal)
npm run build:linux  # Linux
```

> **Note:** You need the `citadel-payload.zip` extracted into `./out/` before building. See the [monorepo](https://github.com/citadel-app/citadel) for build instructions.

---

## License

[MIT](LICENSE) © Citadel
