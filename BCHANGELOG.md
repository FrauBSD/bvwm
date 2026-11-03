# BCHANGELOG

BVWM-only release notes. Upstream fvwm3 history stays in [`CHANGELOG.md`](./CHANGELOG.md).

Format: newest first. Versions are labeled relative to the upstream tag we branched
from (e.g. `1.1.5`) plus BVWM notes.

---

## 1.1.5-bvwm.10

### Added

- **Super+Shift+comma** and **Super+Shift+period** in `default-config/tiling`
  send the focused window to the previous or next output (dwm
  `tagmon`). Order is top to bottom, then left to right, and it
  wraps. A fullscreen window is resized to fill that output. The
  cell it left reflows when it was auto-tiled; an auto-tiled cell
  on the destination takes the window. One output does nothing.

---

## 1.1.5-bvwm.9

### Fixed

- **The .8 fullscreen size guard is reverted.** Ignoring a resize
  or maximize smaller than the monitor did not keep an EWMH
  fullscreen client from leaving fullscreen. Those sizes are no
  longer ignored, and `Maximize False` is no longer special-cased
  on that path.
- **Fullscreen keeps the keyboard.** `DeleteFocus` and the
  stolen-focus path park input on `NoFocusWin`, then focus the
  client again. The FocusOut made the client leave fullscreen
  and iconify. Both parks are skipped while the focused window
  is EWMH fullscreen.

---

## 1.1.5-bvwm.8

### Added

- **Super+W** in `default-config/tiling` closes the focused window,
  the same action as Alt+F4. A tile has no title-bar close button,
  and F4 is behind Fn when Fn-lock is on. The chord is marked so
  Super release does not open the start menu. CirculateSkip windows
  (pager, taskbar) are left alone.
- **Super-arrow tile chords** show a bosd glyph for the direction
  the window is moving: halves, quarters, the working-area fill,
  float-drop, insert, and rotate. `fvwm-tile` emits
  `bosd tile-<place> 2` for that chord. A window mapped into an
  auto-tile does not. Super+T still uses `tile-on` and `tile-float`.
  Super+W has no glyph.

### Fixed

- **Start menu on the first Super tap.** A bare `R` binding was
  modifier none and ran on the press, before a chord could mark
  itself. The next bare Super found that mark and did not open.
  `R` is a release binding. Super release is `4R` because Mod4 is
  still set. `SuperMenuArm` is `PipeRead`, so the chord file is
  clear before the next event.
- **Fullscreen stays fullscreen.** A resize or maximize smaller
  than the monitor was applied to an EWMH fullscreen window, and
  the client left fullscreen. Those sizes are ignored.
  `Maximize False` still exits.

---

## 1.1.5-bvwm.7

### Fixed

- **New tiles meet the strut.** `ResizeHintOverride` replaced the font
  increment only when size hints were read. The first
  `ResizeMoveMaximize` still snapped to that increment, so the frame
  stopped short of the taskbar. `constrain_size()` now applies the
  style before the snap.
- **Super chords** call `SuperChord` before they return, so releasing
  Super after Super+T does not also open the start menu.
- **Auto-tile on map** calls `TileAutoMappedDo` directly. `Schedule`
  stamps its deadline from the last key or button, so the 200ms and
  800ms delays both ran at map time.
- **Super+T** reports through `bosd` (`tile-on` and `tile-float`).

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
