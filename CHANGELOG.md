# Changelog — Sₙ Explorer Web UI

All notable changes to the browser-based **Sₙ Explorer Web UI** are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

---

## [Unreleased]

### Documentation

- Added a dedicated `README.md` for the Web UI project.
- Documented architecture, setup, mathematical conventions, computational safeguards, tests, and project structure.
- Added a project-specific `.gitignore` suitable for the Python backend and vanilla HTML/CSS/JavaScript frontend.

---

## [1.1.0] — 2026-09-13

### Changed

- Rebuilt the frontend to match the generated dark mathematical-workbench reference design.
- Introduced a fixed left-side navigation structure.
- Added a large \(S_n\) group header and selector.
- Added a row of invariant/statistic cards to the Overview.
- Reorganized the Overview into a three-part exploration workspace:
  - permutation table;
  - selected-permutation detail panel;
  - directed cycle visualization.
- Added an explanatory **About \(S_n\)** section and contextual insight panel.
- Propagated the redesigned visual language across:
  - Overview;
  - Composition;
  - Cayley Table;
  - Dihedral Explorer;
  - Subgroups / Quotients;
  - Conjugacy Classes.

### UI / UX

- Adopted a dark navy / charcoal visual theme.
- Added thin blue-gray borders and blue selection states.
- Added serif mathematical headings.
- Added monospace styling for permutation-oriented output.
- Improved layout density for research-style exploration.
- Kept the interface responsive rather than reproducing the reference as a static mockup.

### Fixed

- Corrected cycle-graph mapping between the engine's zero-based internal permutation representation and the user-facing labels \(1,\dots,n\).

### Validation

- Re-ran the mathematical regression suite after the UI rebuild.
- Confirmed all 8 existing tests pass.
- Verified JavaScript syntax.
- Verified Python compilation.

---

## [1.0.0] — 2026-09-07

### Added

- Initial browser-based implementation of the \(S_n\) Explorer.
- Python HTTP/JSON backend.
- HTML/CSS/vanilla JavaScript frontend.
- Browser-based Overview for symmetric groups.
- Interactive permutation browsing.
- Selected-permutation inspection.
- Permutation composition interface.
- Cayley-table explorer.
- Dihedral-group explorer.
- SVG regular-polygon visualization.
- Subgroup-generation interface.
- Exhaustive subgroup exploration for small groups.
- Normal-subgroup detection.
- Quotient-group exploration.
- Conjugacy-class explorer based on cycle type.
- Directed permutation-cycle visualization.

### Architecture

- Preserved Python as the mathematical source of truth.
- Added a browser layer on top of the existing algebra engine.
- Used:
  \[
  \text{Python engine}
  \longrightarrow
  \text{HTTP/JSON API}
  \longrightarrow
  \text{JavaScript}
  \longrightarrow
  \text{HTML/CSS/SVG}.
  \]
- Avoided moving the group-theory implementation into JavaScript.
- Avoided a frontend build system or JavaScript framework.

### Computational safeguards

Introduced explicit limits to prevent computationally expensive operations from freezing the browser:

- browse / inspect \(S_n\): \(n\le 8\);
- composition: \(n\le 8\);
- conjugacy classes: \(n\le 8\);
- Cayley tables: \(n\le 4\);
- exhaustive subgroup enumeration: \(n\le 4\);
- generated-subgroup exploration: \(n\le 7\);
- dihedral explorer: \(3\le m\le 24\).

### Tests

Added regression tests covering representative algebraic properties, including:

- \(|S_3|=6\);
- permutation composition orientation;
- inverse identities;
- permutation order and sign;
- subgroup count for \(S_3\);
- normal subgroups of \(S_3\);
- quotient \(S_3/A_3\);
- Cayley-table Latin-square behavior;
- \(D_5\) size and defining relation;
- conjugacy-class sizes in \(S_3\).

### Validation

- Confirmed all 8 mathematical tests pass.
- Verified representative API endpoints.
- Verified server startup.
- Verified JavaScript syntax.

---

## Notes

Future changes should first be added under **Unreleased**, then moved into a numbered release when published.
