# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A 3D-printable display case/stand (OpenSCAD/CAD) for Eric's Vectorscope 2023 Supercon
conference badge. The badge geometry comes from [`superconvectorscopebadge.stl`](superconvectorscopebadge.stl)
(traced back to the forked submodule — see [`README.md`](README.md)), and
[`vectorScopeBadgeDisplayCase.scad`](vectorScopeBadgeDisplayCase.scad) takes a flat 2D cut through it
to recover the badge outline as a basis for the case body.

## Build / render

OpenSCAD is installed as a macOS app, not on `PATH`. The single model is
[`vectorScopeBadgeDisplayCase.scad`](vectorScopeBadgeDisplayCase.scad).

```sh
# open interactively
open -a OpenSCAD vectorScopeBadgeDisplayCase.scad

# headless render to STL via the app bundle binary
/Applications/OpenSCAD.app/Contents/MacOS/OpenSCAD \
  -o vectorScopeBadgeDisplayCase.stl vectorScopeBadgeDisplayCase.scad
```

The `.scad` does `projection(cut = true) import("superconvectorscopebadge.stl", convexity=3)` —
this slices the badge mesh into a 2D profile (intended to be `linear_extrude`d into the case body).

Dependency: [`supercon-2023-badge-enclosure`](supercon-2023-badge-enclosure) is a **git submodule**
(fork: `github.com/ericmoderbacher/supercon-2023-badge-enclosure`), the origin of the badge geometry.
Init it with:

```sh
git submodule update --init --recursive
```

## Current state & next step

- The model so far is a single line: `projection(cut = true) import(...)` recovers the badge outline
  from `superconvectorscopebadge.stl` instead of importing the raw solid.
- Open design decision: **stand vs. enclosing case** — decide the goal, then build the case body in
  OpenSCAD from the badge outline (e.g. `linear_extrude` of the projected profile).

## Fleet context

Part of Eric Moderbacher's MOSS fleet. Conventions:

- **R1** — deps are git submodules of personal forks, **never** package managers
  (`supercon-2023-badge-enclosure` follows this).
- **R5** — each repo self-describes via a `capabilities.toml`; this repo does **not** have one yet.
- Fleet spine: `modersModel` / `modersOperandi` / `moss`.
