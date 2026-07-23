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
| **Stock `fvwm3` package** | Modules (`FvwmPager`, …), `share/fvwm3`, man pages, `FvwmCommand`, helpers |
| **`bvwm` package (planned)** | Primarily the **`bvwm` binary** — what we materially changed in the core WM |

We do **not** rename `Fvwm*` modules or man pages to `Bvwm*`. Configs keep
`Module FvwmButtons` and friends. The product name is BVWM; the module vocabulary
stays Fvwm.

### Why a thin binary package?

Decor and core WM patches live in the main executable, not in every module. Depending
on stock fvwm3 for the rest:

- lets `fvwm3` and `bvwm` both sit on disk (`bin/fvwm3` and `bin/bvwm`);
- avoids duplicating (and fighting) hundreds of Fvwm man pages and share files;
- keeps this fork easier to rebase when upstream moves.

Pin the `fvwm3` runtime dependency to a compatible version: module paths are
versioned (e.g. `libexec/fvwm3/1.1.5/`). Build BVWM so its compiled module/data
paths match that package.

If we later patch a module or share file, that artifact moves into the bvwm
package (or the thin-binary model is revisited).

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

For a FreeBSD port that only stages `bvwm`, build this tree, install/rename the
main executable, and discard the rest of the stage so stock `fvwm3` owns modules
and man pages.

## Upstream

- Project: https://github.com/fvwmorg/fvwm3
- We track release tags (e.g. `1.1.5`) that match FreeBSD’s `fvwm3` port when
  practical, then layer BVWM commits on top.

## License

Same as upstream fvwm3 — see `COPYING`.
