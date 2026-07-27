# BVWM

**B?** Virtual Window Manager — a fork of [fvwm3](https://github.com/fvwmorg/fvwm3).

Home: [FrauBSD/bvwm](https://github.com/FrauBSD/bvwm)

## What the B stands for

Same game as fvwm’s mysterious **F**: pick what fits.

Berkeley · BSD · Badass · … · or invent your own.

## BREADME (BREAD ME)

This file is the **BVWM** product readme. Upstream’s `README.md` is left alone on
purpose so merges from `fvwmorg/fvwm3` stay peaceful. Eat this one for FrauBSD /
packaging / divergence; use upstream’s for stock fvwm3 lore.

Companion: [`BCHANGELOG.md`](./BCHANGELOG.md) (BVWM-only notes). Upstream history
remains in `CHANGELOG.md`.

## Relationship to fvwm3

| Layer | Role |
|-------|------|
| **This git tree** | Full fvwm3-derived sources so we can build and merge upstream |
| **Stock `fvwm3` package** | Unrelated install; can sit beside BVWM |
| **`bvwm` package** | Self-contained: `bin/bvwm`, modules under `libexec/bvwm/`, `share/bvwm`, prefixed helpers/mans |

We do **not** rename `Module Fvwm*` command names. Configs keep
`Module FvwmButtons` and friends; those binaries live under BVWM’s private
moduledir. PATH tools and man pages use a `bvwm-` prefix so they coinstall with
stock fvwm3 (`bvwm-root`, `bvwm-FvwmAnimate.1`, …).

### Why a full, coinstallable package?

Decor and core WM patches live in the main executable, but modules are
versioned under `libexec/.../<ver>/`. Shipping BVWM’s own module/data tree
avoids pinning a specific `fvwm3` package version. Prefixed helpers and mans
avoid file conflicts so `fvwm3` and `bvwm` can both be installed.

`meson.project_name()` stays `fvwm3` for quieter rebases; install identity is
the separate `bvwm_name` (`bvwm`).

## Divergences (engine)

Behavioral changes in this tree (see `BCHANGELOG.md`), including:

- **ButtonStyle** hover states (pointer over titlebar buttons)
- **TitleStyle ButtonWidth** (rectangular titlebar hitboxes)

Default config filename may grow a BVWM-specific name later (e.g. `.bvwmrc`);
until then, expect fvwm3-compatible rc naming unless the port wraps it.

## Config paths (BVWM vs stock fvwm3)

BVWM defaults differ so Hover / ButtonWidth (and later extras) never land in a
file stock **fvwm3** tries to parse:

| | BVWM | stock fvwm3 |
|--|------|-------------|
| User dir | `~/.bvwm` (`FVWM_USERDIR`) | `~/.fvwm` |
| Compat rc | `.bvwmrc` | `.fvwm2rc` |

Search order still prefers `config` under the user dir / datadir, then `.bvwmrc`
locations, then packaged defaults. Keep a stock-safe `~/.fvwm2rc` (or none) for
`fvwm3`; put BVWM chrome in `~/.bvwmrc` or `~/.bvwm/config`.

## Building

Same as upstream fvwm3 (meson). See `INSTALL.md`.

A normal `meson setup && meson install` stages the full BVWM tree under the
`bvwm` install identity (binary, modules, share data, prefixed helpers/mans).

## Upstream

- Project: https://github.com/fvwmorg/fvwm3
- We track release tags (e.g. `1.1.5`) that match FreeBSD’s `fvwm3` port when
  practical, then layer BVWM commits on top.

## License

Same as upstream fvwm3 — see `COPYING`.
