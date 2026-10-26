# Changelog

All notable changes to the **Network Health Reporter** project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [2.3.1] - 2026-10-26

### Fixed
- **Live device command selection**: Detect SG/CBS command syntax before setting terminal paging, use supported assessment commands for Small Business switches and routers, include ISR/ASR neighbors in CDP traversal, and limit concurrent management sessions to four.
- **Assessment coverage accuracy**: Treat StackWise commands as optional on standalone switches and report a failed device visit once with its collection reason instead of listing every command as unavailable.

---

## [2.3.0] - 2026-10-26

### Added
- **Credential vault and presets**: Add a portable AES-256 vault protected by a master password, named SSH credential profiles, optional enable secrets, apply/delete actions, exact-host matching, and optional authentication fallback for live assessments. Existing Windows host credentials can be imported without deleting their source files.

### Fixed
- **SG/C1000 CDP discovery**: Parse Small Business detail and wrapped neighbor tables so attached APs count without WLC inventory and observed inter-switch links retain their actual port numbers. Hide port badges on inferred links when no port was captured.
- **Live CDP traversal depth**: Continue auditing switches discovered by downstream switches across multiple hops, visit each known device IP once, and retain observed switch links and the WLC's actual uplink switch for topology generation.
- **Router model recognition**: Support optional 'cisco ' prefix and whitespace in Cisco router model strings (e.g. 'cisco ISR4331/K9', 'CISCO 2921') to prevent router chassis from falling back to access switches.
- **Link speed analyzer status parsing**: Harden regex against port descriptions containing status keywords (e.g. 'Connected to AP', 'Monitoring server') which previously caused state, duplex, and speed columns to be misaligned.

---

## [2.2.1] - 2026-10-23

### Fixed
- **Router chassis identity and topology**: Read chassis PID and serial from inventory, preserve Router role in topology and Excel, count captured physical interfaces and avoid inferred router-to-core links without neighbor evidence.

---

### Changed
- **Explicit development-signed release path**: Publish v2.2.1 locally with the existing development identity, verified installer hash and uploaded package digests; disclose SmartScreen limitations. Trusted signing remains required by CI.
- **Public release asset retention**: Keep the newest stable build and preserve release records, tags, manifests and logs while pruning obsolete binary packages after successful releases.

---


## [2.2.0] - 2026-10-23

### Changed
- **Local beta: separate data-port speed review**: Keep slow data/access ports in a separate LOW review alert, exclude discovered IP-phone ports including phone/PC shared ports, and keep switch/AP degradation findings separate. Unknown endpoint capability is explicitly marked for review.
- **Local beta: inspection output**: Remove raw captured output and artifact notices from the inspector and copied inspection; retain verification commands and conditional remediation. Use command-output wording for assessment coverage.
- **Local beta: topology and inspection usability**: Layer toggles reset and fit the diagram. Add visible-node search, clickable link inspection, complete wrapped switch names, responsive dashboard gauges, multiline tables and a redesigned finding inspector. Public release remains v2.1.0.

---

### Fixed
- **Local beta: topology obstructions and overflow**: Replace single-obstacle detours with an indexed corridor search around all node cards, discourage shared wire segments and reserve space between leaf rows. Wrap and fit complete exported hostnames. Expand AP inventory height into available viewport space, improve compact AP columns and normalize topology toolbar gaps. User visual/performance validation pending.
- **Local beta: PDF port tags and responsive columns**: Honor reserved label dimensions and endpoint rotation in topology PDF/SVG/PNG exports; fit long port names and paint badges after all wires. Use proportional table column widths with readable minimums and restore topology/status controls on the right of wide dashboard headers. Add repeatable column-width policy script. User testing pending.
- **Local beta: dashboard layout and small-screen zoom**: Distribute centered gauges in equal-width rows of four, two or one, reflow summary cards and dashboard heading, isolate title-bar drag/double-click gestures from zoom buttons, fit initial window bounds to the display working area, and adapt navigation to scaled content width. Compiled only; user testing pending.
- **Local beta: degraded infrastructure link speeds**: Check observed switch and AP links for sub-gigabit negotiation against endpoint/media capability. Accept a 1 Gbps link to a multigigabit AP, skip unknown and disconnected interfaces, deduplicate reciprocal wires, and stop flagging all 100 Mbps clients. User testing pending.
- **Grouped finding evidence lookup**: Split comma-separated finding targets and resolve command output separately for each device, preserving per-device headings and missing-output notices. Empty explicit artifacts now fall back to retained command evidence. Testing deferred to the user.
- **Local beta: PDF inventory and topology page**: Populate switch serial and base MAC from device-specific captured show version/inventory output and retain identity in parsed switch data. Summarize coverage on the opening page, preserve full details in an appendix, and finish with one adaptively sized vector topology page instead of tiled pages. User will perform testing.
- **Local beta: remediation accuracy**: Replace guessed interfaces, native VLAN 1, broad STP priorities, blanket errdisable recovery, legacy QoS buffer settings and AP-reset fallbacks with read-only checks and conditional, scoped templates. Preserve actual evidence and clearly label missing output; include reviewed Cisco references.

---

### Security
- **Verified Windows signing**: Share signing across release and beta installer scripts, require configured trusted timestamped signatures for public builds, remove silent self-signed fallback and unchecked success messages, persist an explicit development-only identity for local beta signing, and recompute hashes after signing. Add CI signing-secret setup, separate beta installer identity, private-key ignore rules and accurate SmartScreen documentation.

---


## [2.1.0] - 2026-10-23

### Fixed
- **BUG-01: preserve observed CDP switch connections**: Retain every observed switch-to-switch wire independently of the inferred parent during discovery, offline merging, live collection and topology export. Reciprocal silo neighbors no longer erase the distribution path; redundant uplinks and parallel physical ports are preserved.

### Added
- **Release verification scripts**: Compact pipeline status and a single public verification command check published packages, installer SHA-256, version metadata, README and changelog consistency. The local beta build script remains available for isolated Windows testing.

---

## [2.0.8] - 2026-10-23

### Fixed
- **Topology routing and view-state integrity**: Match parallel links by layout ID, retain dragged positions across filters, expand rerouted bounds, and avoid invalid or ambiguous endpoint matches.
- **Live evidence retention and partial assessment coverage**: Retain successful live command outputs, publish coverage notes across dashboard and exports, remove incorrect WLC seed fallback, and honor core-only scope.
- **Assessment data integrity and cross-platform presentation**: Remove fabricated IPs, inventory and RF data; preserve real 10.22 addresses and unknown-device identity; fix duplicate auditing, upload collisions, stale topology, and bundled fonts.

### Added
- **Public test-build workflow and clearer handover guidance**: Manual branch builds can publish portable LazyAutomatar prereleases with checksums while keeping stable updates and documentation separate. Reports restores worksheet descriptions; About adds build and platform details, release links and accurate discovery scope.
- **Vector topology PDF export**: Export the current diagram to an auto-oriented A3 PDF alongside Visio, using background rendering and safe file replacement.

### Changed
- **Clearer reports and readable topology pages**: Simplified Reports exports, evidence context, expandable inventories, subtle interaction feedback and Fit diagram. Assessment PDFs use vector diagrams and automatic overlapping landscape detail pages for large topologies; export runs in the background and preserves existing files on rendering failure. Removed sample report substitution and fabricated fallback IPs and ports.

---


## [2.0.7] - 2026-10-23

### Fixed
- **BUG-01 topology neighbor identity**: Preserve distinct hyphenated and underscored hostnames, use shared CDP hostname normalization, and require a unique truncated-name match to prevent Visio links from being redirected to another node.

---

## [2.0.6] - 2026-10-21

### Changed
- **Solo Project Attribution & Branding Cleanse**: Removed all legacy company/corporate references across the entire codebase, EULA, release pipeline, and packaging to reflect solo project ownership by Yash Nalawde.
- **Dynamic Release Notes Synchronization**: `publish-all.ps1` now automatically extracts the exact release notes for each version from `CHANGELOG.md` into `update_manifest.json`. The desktop application dynamically prepends incoming version notes into the in-app Changelog History upon update check so newer release notes are immediately visible before updating.
- **High-Contrast Theme-Aware Version Tags**: Replaced hardcoded white foreground on version badges with theme-aware `TextFillColorPrimaryBrush` on a subtle pill with accent border, guaranteeing crisp WCAG AAA contrast in both Dark and Light themes.
- **Certificate Metadata**: Updated code-signing certificate identity to `Network Health Reporter / Yash Nalawde` and exported as `NetworkHealthReporter_CodeSigning.cer`.

---

## [2.0.5] - 2026-10-21

### Changed
- **Author Attribution**: Maintained developer branding as Yash Nalawde across title bar pill and About view, linking to the LazyAutomatar distribution channel and GitHub issues.

---

## [2.0.4] - 2026-10-21

### Added
- **Silent Background Auto-Updater**: Configured Inno Setup with `/VERYSILENT /SUPPRESSMSGBOXES /NORESTART /CLOSEAPPLICATIONS` and automatic silent relaunch, providing a true zero-interruption, one-click in-place update experience.
- **In-App Release Changelog Preview**: Added an expandable "Release Changelog & History" card and viewer directly to the **About** view, allowing users to browse version release notes and security highlights offline at any time.

### Changed
- **Developer Details**: Preserved author attribution as Yash Nalawde across the title bar pill and About view with direct links to the LazyAutomatar distribution channel and GitHub issues.
- **Title Bar Spacing Optimization**:
  - Windows: Adjusted caption gutter to 142px to eliminate excessive empty void next to window controls.
  - macOS: Added 78px left clearance to guarantee zero overlap with native Apple traffic light window controls (close/minimize/zoom), and natural 14px right margin.
  - Standardized all title bar controls (Zoom pill, Developer pill, Dark Mode button) to a uniform 28px height, 14px pill corner radius, and 8px inter-item spacing.

---

## [2.0.3] - 2026-10-21

### Added
- **Authenticode Digital Code Signing**: Integrated automated Authenticode code signing into the Windows compilation pipeline (`publish-all.ps1`). Signs both the standalone application executable (`NetworkHealthReporter.exe`) and the Inno Setup installer (`NetworkHealthReporter_Setup.exe`) with Authenticode signatures.
- **Enterprise Certificate Export**: Automatically exports the public code signing certificate (`NetworkHealthReporter_CodeSigning.cer`) alongside release artifacts for domain and local machine installation into Trusted Publishers / Trusted Root Certification Authorities to eliminate Windows SmartScreen prompts.
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
