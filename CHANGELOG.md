# Changelog

All notable changes to the **Network Health Reporter** project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [2.0.4] - 2026-10-21

### Added
- **Silent Background Auto-Updater**: Configured Inno Setup with `/VERYSILENT /SUPPRESSMSGBOXES /NORESTART /CLOSEAPPLICATIONS` and automatic silent relaunch, providing a true zero-interruption, one-click in-place update experience.
- **In-App Release Changelog Preview**: Added an expandable "Release Changelog & History" card and viewer directly to the **About** view, allowing users to browse version release notes and security highlights offline at any time.

### Changed
- **Developer Details to LazyAutomatar**: Standardized branding, author attribution, and links to `LazyAutomatar` across the title bar pill, assembly metadata, installer properties, and About view.
- **Title Bar Spacing Optimization**:
  - Windows: Adjusted caption gutter to 142px to eliminate excessive empty void next to window controls.
  - macOS: Added 78px left clearance to guarantee zero overlap with native Apple traffic light window controls (close/minimize/zoom), and natural 14px right margin.
  - Standardized all title bar controls (Zoom pill, Developer pill, Dark Mode button) to a uniform 28px height, 14px pill corner radius, and 8px inter-item spacing.

---

## [2.0.3] - 2026-10-21

### Added
- **Authenticode Digital Code Signing**: Integrated automated Authenticode code signing into the Windows compilation pipeline (`publish-all.ps1`). Signs both the standalone application executable (`NetworkHealthReporter.exe`) and the Inno Setup installer (`NetworkHealthReporter_Setup.exe`) with Conventus Technologies publisher identity.
- **Enterprise Certificate Export**: Automatically exports the public code signing certificate (`ConventusTechnologies_CodeSigning.cer`) alongside release artifacts for domain and local machine installation into Trusted Publishers / Trusted Root Certification Authorities to eliminate Windows SmartScreen prompts.
- **Official End-User License Agreement (EULA)**: Added formal `EULA.txt` defining terms for closed-source enterprise freeware use, commercial/personal deployment rights, non-invasive read-only safety guarantees, and reverse engineering restrictions.
- **Inno Setup EULA Integration**: Embedded `EULA.txt` directly into the Windows setup wizard via Inno Setup `LicenseFile` directive, requiring user agreement before installation.
- **Automated Public Repo Documentation Sync**: Release pipeline now automatically synchronizes `README.md`, `EULA.txt`, `LICENSE.md`, `CHANGELOG.md`, and visual assets directly to the public release repository (`LazyAutomatar/Network-Health-Reporter`).

### Changed
- Updated README.md test badge and architecture documentation to reflect 262 passing unit tests (up from 226).
- Streamlined Windows download links and quick-start instructions to reference canonical installer filenames.

---

## [2.0.2] - 2026-10-21

### Fixed
- **Auto-Updater HTTP Timeout**: Increased manifest check timeout from 15 seconds to 60 seconds and binary download timeout to 10 minutes to support high-latency, filtered, or metered enterprise WAN connections.
- **Corporate Proxy & Compression**: Added system default WebProxy resolution (`UseProxy = true`) and automated GZip/Deflate decompression to `UpdateService` HTTP client pipeline.
- **CI Test Suite Stability**: Fixed `DeviceSessionTests.Connect_WhenHostUnreachable_ThrowsDescriptiveException` on GitHub Actions Windows runners where an OpenSSH server listening on `127.0.0.1:22` caused unexpected authentication prompts.

### Security
- Hardened update package staging with strict SHA-256 hash checks and PE header verification.

---

## [2.0.1] - 2026-10-21

### Added
- **In-App Auto-Update Checker**: Added update notification and one-click upgrade installation directly from the **About** view.
- **Cryptographic Release Verification**: Verified binary payload integrity against GitHub release manifest SHA-256 hashes before staging.
- **PE Header Magic Byte Validation**: Inspected executable headers (`MZ` signature) before executing setup processes to guard against corrupt or intercepted payload downloads.
- **SemVer Comparison Engine**: Full Semantic Versioning comparison support including pre-release tags (`-beta`, `-rc`).

---

## [2.0.0] - 2026-10-20

### Added
- **Avalonia UI 11.2 Desktop Architecture**: Completely re-architected cross-platform native UI featuring dark slate fluent aesthetic, vector iconography, and high-DPI scaling.
- **Multi-Tier Campus Topology Engine**: Automated hierarchical classification for Tier 1 (Core), Tier 2 (Distribution), and Tier 3 (Access) devices with WLC and endpoint layers.
- **Orthogonal Manhattan Bus Routing**: Collision-free orthogonal routing with 80px channel separation, preventing overlapping lines across dense switch networks.
- **Multi-Token 25G/40G/100G Port Parser**: Advanced interface pairing for modern high-speed uplinks (`Twe`, `Ten`, `Fo`, `Hu`, `Gig`) across wrapped CDP and LLDP neighbor tables.
- **0–100 Weighted Site Health Scoring**: Composite metric auditing Switching, Wireless RF, Topology redundancy, and Network Safety.
- **Microsoft Visio VSDX Exporter**: Direct generation of native Microsoft Visio XML diagrams with official network master stencils.
- **Handover Excel Exporter (`.xlsx`)**: 6 comprehensive executive worksheets covering Executive Summary, Topology Matrix, Hardware Inventory, and Prioritized Findings.
- **Executive PDF Report Generator**: Publication-grade PDF report generation powered by QuestPDF with embedded vector diagrams.
- **Cross-Platform Compilation Matrix**: Zero-dependency self-contained builds for Windows x64, macOS Apple Silicon (ARM64), macOS Intel (x64), Linux x64, and Linux ARM64.
