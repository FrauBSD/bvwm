# BCHANGELOG

BVWM-only release notes. Upstream fvwm3 history stays in [`CHANGELOG.md`](./CHANGELOG.md).

Format: newest first. Versions are labeled relative to the upstream tag we branched
from (e.g. `1.1.5`) plus BVWM notes.

---

## 1.1.5-bvwm.3

### Packaging / coinstall

- Install identity is **`bvwm`**: `bin/bvwm`, `share/bvwm`, `libexec/bvwm/<ver>/`,
  gettext domain `bvwm`, and `xsessions/bvwm.desktop`.
- PATH helpers are prefixed for coinstall with stock fvwm3:
  `bvwm-root`, `bvwm-menu-*`, `bvwm-FvwmCommand`, `bvwm-FvwmPrompt`, …
- Man pages install as `bvwm.1`, `bvwm-FvwmAnimate.1`, `bvwm-root.1`,
  `bvwmall.1`, … (stock `fvwm3.1` / `FvwmAnimate.1` names are not used).
- Module command names stay `FvwmButtons` and friends under the private moduledir.

### Notes

- `meson.project_name()` remains `fvwm3` for rebase peace; `bvwm_name` drives
  install paths, `PACKAGE`, and gettext.

---

## Based on upstream 1.1.5 (1.1.5-bvwm.2 and earlier)

Branch: `bvwm-1.1.5`

### Added

- **ButtonStyle hover** — `ActiveHover`, `InactiveHover`, and related
  toggled/down hover states; track decor-button enter/leave so chrome can
  highlight under the pointer without a press.
- **TitleStyle ButtonWidth** — along-title button length independent of title
  thickness (`0` keeps stock square buttons). Enables wider hitboxes without
  raising the whole titlebar.
- **Config paths** — default user dir `~/.bvwm` and compat rc `.bvwmrc` so
  BVWM-only directives are not loaded by stock fvwm3 via `.fvwm2rc`.
- **bvwm(1)** manual page.

### Packaging intent (superseded by 1.1.5-bvwm.3)

Earlier packaging explored a thin `bvwm` binary plus `RUN_DEPENDS` on stock
fvwm3. **1.1.5-bvwm.3** ships a self-contained, coinstallable tree instead.
