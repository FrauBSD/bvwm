# BCHANGELOG

BVWM-only release notes. Upstream fvwm3 history stays in [`CHANGELOG.md`](./CHANGELOG.md).

Format: newest first. Versions are labeled relative to the upstream tag we branched
from (e.g. `1.1.5`) plus BVWM notes.

---

## 1.1.5-bvwm.6

### Packaging

- **FvwmPrompt** honors `GO_CMD` and `GO_BUILDFLAGS` when a packager sets
  them. Meson writes a wrapper so quoted `-ldflags` are shell syntax and
  `-C` stays the first `go build` flag. Unset, the build is unchanged
  (`go build -mod=vendor`).

---

## 1.1.5-bvwm.5

### Added

- **Tiling** in `default-config/tiling`, read by the stock config.
  Super+arrows (halves, quarters, fill, restore), Super+Ctrl+Up/Down
  (insert and walk back), Super+T (auto-tile for the current monitor,
  desk, and pager page), Super+Tab, and Super+grave.
  `default-config/tiling` binds these chords.
- **Hotkey catalog** for those chords, installed into
  `share/bhotkeys/plugins.d`, plus `bhotkeys-bvwm-run` and
  `bhotkeys-bvwm-apply`. The x11-wm/bvwm port depends on x11/bhotkeys
  and x11/bosd.
- **`fvwm-tile`** and **`bvwm-same-class`**, PipeRead helpers for the
  tiling functions.
- **FvwmEventTile**, a second FvwmEvent alias: new windows join an
  auto-tile layout, and closed windows leave it. The stock desk event
  module is unchanged.
- **`taskbar_h`** defaults to 0 in the stock config (bottom strut for
  tiling). A later `InfoStoreAdd` replaces it.
- **Session bus** when `DBUS_SESSION_BUS_ADDRESS` is empty. bvwm
  re-execs through `dbus-launch --exit-with-session`, so the bus
  is in the environment of bvwm and everything it starts, and the
  bus exits with the session. An address already set is left alone.
- **Start menu** on a bare Super press and release (`super-menu-arm`,
  `super-menu-release`, `super-menu-open`), read from
  `default-config/super-menu`. `bvwm-super-menu-handler` marks a
  chord so release does not also open the menu. Enabled plugin
  chords are registered by bhotkeys; this file does not bind them.

---

## 1.1.5-bvwm.4

### Fixed

- **SetEnv / UnsetEnv** no longer corrupt `environ`. `flib_putenv()` passed
  `putenv(3)` strings it later freed, and `UnsetEnv` never called
  `unsetenv(3)` because the build left `HAVE_UNSETENV` undefined. A bad
  environ entry then made later `setenv(3)` fail for the life of the
  process, including across Restart. The code now uses `setenv(3)` and
  `unsetenv(3)`, which copy their arguments.

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
