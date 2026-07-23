# BCHANGELOG

BVWM-only release notes. Upstream fvwm3 history stays in [`CHANGELOG.md`](./CHANGELOG.md).

Format: newest first. Versions are labeled relative to the upstream tag we branched
from (e.g. `1.1.5`) plus BVWM notes.

---

## Based on upstream 1.1.5 (unreleased packaging)

Branch: `bvwm-1.1.5`

### Added

- **ButtonStyle hover** — `ActiveHover`, `InactiveHover`, and related
  toggled/down hover states; track decor-button enter/leave so chrome can
  highlight under the pointer without a press.
- **TitleStyle ButtonWidth** — along-title button length independent of title
  thickness (`0` keeps stock square buttons). Enables wider hitboxes without
  raising the whole titlebar.

### Packaging intent

- Product docs: `BREADME.md`, this file.
- Planned FreeBSD package ships primarily the **`bvwm`** core binary and
  **RUN_DEPENDS** on stock **fvwm3** for modules, man pages, and helpers (see
  `BREADME.md`).
