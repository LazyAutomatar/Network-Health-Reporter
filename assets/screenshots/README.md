# Screenshots Guide for Network Health Reporter

This folder is configured for application screenshots featured in the GitHub `README.md` and the GitHub Pages website (`docs/index.html`).

### Recommended Screenshots & Dimensions

1. **`topology.png`** (1920x1080 or 1600x900)
   - **View:** Canvas Topology View
   - **Tips:** Show a multi-tier network (Core, Distribution, Access, WLC) with clean orthogonal lines, port labels, and marquee selection active.

2. **`dashboard.png`** (1920x1080 or 1600x900)
   - **View:** Executive Dashboard View
   - **Tips:** Show the circular health gauge (e.g. 94/100), domain sub-scores, active findings summary, and telemetry feed.

3. **`inventory.png`** (1920x1080 or 1600x900)
   - **View:** Hardware & PoE Inventory View
   - **Tips:** Show switch stacks, dual power supplies (1100W/715W), fan modules, and PoE capacity breakdown.

4. **`findings.png`** (1920x1080 or 1600x900)
   - **View:** Audit & Remediation View
   - **Tips:** Show prioritized findings (Critical, High, Medium, Info) with rule categories (STP, VLAN, Power, Hardware).

5. **`visio_export.png`** (1920x1080)
   - **View:** Microsoft Visio (`.vsdx`) open with the generated campus diagram and Cisco stencil shapes.

### How to Enable in `README.md`

In `README.md`, insert:
```markdown
<div align="center">
  <img src="assets/screenshots/topology.png" alt="Network Health Reporter Topology" width="90%">
</div>
```
