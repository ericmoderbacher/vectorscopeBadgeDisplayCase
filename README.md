# vectorScopeBadgeDisplayCase

A 3D-printable display case/stand for the Vectorscope 2023 Supercon conference badge.

## Files

- [`vectorScopeBadgeDisplayCase.scad`](vectorScopeBadgeDisplayCase.scad) — the OpenSCAD model.
  It takes a flat 2D cut through the badge mesh (`projection(cut = true) import(...)`) to recover
  the badge outline as a basis for the case body.
- [`superconvectorscopebadge.stl`](superconvectorscopebadge.stl) — the badge geometry, produced by
  importing *Supercon 2023 Badge - Tinabel's Best Guesses.step*
  ([hackaday.io source](https://cdn.hackaday.io/files/1933128270660608/Supercon%202023%20Badge%20-%20Tinabel's%20Best%20Guesses.step)).
  The same geometry traces back to the
  [`supercon-2023-badge-enclosure`](supercon-2023-badge-enclosure) submodule.

## Build / render

OpenSCAD is installed as a macOS app, not on `PATH`:

```sh
# open interactively
open -a OpenSCAD vectorScopeBadgeDisplayCase.scad

# headless render to STL via the app bundle binary
/Applications/OpenSCAD.app/Contents/MacOS/OpenSCAD \
  -o vectorScopeBadgeDisplayCase.stl vectorScopeBadgeDisplayCase.scad
```

## Submodule

[`supercon-2023-badge-enclosure`](supercon-2023-badge-enclosure) is a git submodule
(fork: `github.com/ericmoderbacher/supercon-2023-badge-enclosure`), the origin of the badge geometry:

```sh
git submodule update --init --recursive
```
