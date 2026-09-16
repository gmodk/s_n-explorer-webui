# Changelog — Sₙ Explorer Web UI

All notable changes to the browser-based **Sₙ Explorer Web UI** are documented here.

## [Unreleased]

### Documentation

- Keep README and implementation notes synchronized with current functionality.

---

## [1.2.0] — 2026-09-16

### Added

- Animated, element-by-element permutation composition.
- Explicit Python-side composition trace of the form `i -> tau(i) -> sigma(tau(i))`.
- Three-lane SVG composition diagram: **Input**, **After tau**, **After sigma**.
- Moving token and progressive path drawing for each stage of the composition.
- Play-all, previous, next, replay, direct trace selection, and animation-speed controls.
- Two-row Cauchy notation for `tau`, `sigma`, and `sigma o tau` in the Composition view.
- Built-in example button for `(231) o (132)` in `S3`.
- Reduced-motion support: automatic playback is suppressed when the browser requests reduced motion.
- Regression test for the exact `(231) o (132)` trace.

### Changed

- Composition API now returns a `trace` array in addition to the operands and result.
- Composition view now explains the intermediate mapping rather than only displaying three result cards.

### Validation

- Confirmed the example produces the traces `1 -> 1 -> 2`, `2 -> 3 -> 1`, `3 -> 2 -> 3`.
- Confirmed the resulting one-line permutation is `(213)`.
- Mathematical regression suite: 9 tests passing.
- JavaScript syntax and Python compilation checks passing.

---

## [1.1.0] — 2026-09-13

### Changed

- Rebuilt the frontend around the dark mathematical-workbench design.
- Added fixed navigation, invariant cards, interactive overview, permutation detail view, and cycle visualization.
- Propagated the same visual language to the composition, Cayley, dihedral, subgroup, quotient, and conjugacy views.

### Fixed

- Corrected the conversion between zero-based internal permutations and one-based SVG labels.

---

## [1.0.0] — 2026-09-07

### Added

- Initial Python HTTP/JSON backend and vanilla HTML/CSS/JavaScript frontend.
- Elements, composition, Cayley table, dihedral, subgroup, quotient, and conjugacy explorers.
- SVG visualization support and mathematical regression tests.
