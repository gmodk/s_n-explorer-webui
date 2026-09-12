# \(S_n\) Explorer — Web UI

A browser-based interactive application for exploring the **symmetric group**
\[
S_n,
\]
its permutations, algebraic operations, subgroups, quotient groups, conjugacy classes, Cayley tables, and related dihedral groups.

The project extends the original Python command-line explorer into a full web interface while preserving Python as the mathematical computation layer.

---

## Overview

The application is designed as an **interactive abstract-algebra workbench**.

Its interface combines:

- a Python group-theory engine;
- a local HTTP/JSON API;
- an HTML/CSS frontend;
- vanilla JavaScript for interaction;
- SVG-based mathematical visualizations.

The goal is to make the structure of finite permutation groups directly inspectable without moving the underlying algebraic logic into JavaScript.

---

## Architecture

The application follows the structure

\[
\text{Python algebra engine}
\longrightarrow
\text{HTTP / JSON API}
\longrightarrow
\text{JavaScript}
\longrightarrow
\text{HTML / CSS / SVG}.
\]

Python remains the source of truth for the mathematics.

The frontend is responsible for:

- navigation;
- state management;
- tables;
- form controls;
- selection behavior;
- visualizations;
- rendering API responses.

This separation keeps the mathematical implementation independent from the presentation layer.

---

## Features

The web interface contains several complementary exploration modes.

### Overview

The Overview page provides a compact structural summary of the selected symmetric group.

It displays:

- group order
  \[
  |S_n|=n!;
  \]

- number of even permutations;

- number of odd permutations;

- number of self-inverse permutations;

- number of conjugacy classes;

- an interactive permutation table;

- detailed information about the selected permutation;

- a directed cycle visualization;

- contextual information about the currently selected group.

Selecting a permutation updates its mathematical properties and visualization immediately.

---

## Elements explorer

The Elements view lets you browse the permutations of \(S_n\).

For each element, the interface can display:

- permutation index;
- one-line notation;
- disjoint-cycle notation;
- cycle type;
- order;
- sign;
- parity;
- inverse;
- identity status;
- self-inverse status.

The table supports interactive selection and browsing.

---

## Composition

The Composition view computes

\[
\sigma\circ\tau.
\]

The project uses the convention

\[
(\sigma\circ\tau)(i)=\sigma(\tau(i)).
\]

Therefore:

1. \(\tau\) acts first;
2. \(\sigma\) acts second.

The interface shows both input permutations and the resulting permutation together with their structural properties.

---

## Cayley table

The Cayley Table view constructs the multiplication table of \(S_n\) under permutation composition.

For a finite group \(G\), the Cayley table contains one row and one column for every element of \(G\).

For \(S_n\), the table therefore contains

\[
(n!)^2
\]

products.

Because factorial growth makes large Cayley tables impractical, the web application intentionally restricts this operation to small values of \(n\).

---

## Dihedral explorer

The Dihedral Explorer constructs the group

\[
D_m,
\]

the symmetry group of a regular \(m\)-gon.

The standard presentation is

\[
D_m
=
\langle r,s
\mid
r^m=e,\;
s^2=e,\;
srs=r^{-1}
\rangle.
\]

The application represents the rotations and reflections as permutations of the polygon vertices.

The interface includes:

- rotations;
- reflections;
- permutation representations;
- group order;
- an SVG visualization of the regular polygon.

Since

\[
|D_m|=2m,
\]

the group consists of

\[
e,r,r^2,\dots,r^{m-1},
s,sr,sr^2,\dots,sr^{m-1}.
\]

---

## Subgroups

The Subgroups view supports subgroup generation and, for sufficiently small groups, exhaustive subgroup enumeration.

Given elements

\[
g_1,\dots,g_k,
\]

the generated subgroup is

\[
\langle g_1,\dots,g_k\rangle.
\]

The application computes subgroup closure under the group operation.

For small symmetric groups, it can also enumerate all subgroups and determine whether each subgroup is normal.

---

## Normal subgroups

A subgroup

\[
H\le G
\]

is normal when

\[
gHg^{-1}=H
\qquad
\text{for every }g\in G.
\]

The web interface identifies normal subgroups and exposes them as candidates for quotient-group construction.

---

## Quotient groups

If

\[
H\trianglelefteq G,
\]

the application can construct

\[
G/H.
\]

Its elements are cosets

\[
gH.
\]

The quotient explorer can display:

- cosets;
- quotient-group order;
- identity coset;
- element orders in the quotient;
- quotient Cayley table.

For example,

\[
S_3/A_3\cong C_2.
\]

---

## Conjugacy classes

The web application includes a conjugacy-class explorer.

Two elements \(\sigma,\tau\in S_n\) are conjugate if there exists

\[
g\in S_n
\]

such that

\[
\tau=g\sigma g^{-1}.
\]

In the symmetric group, two permutations are conjugate **if and only if they have the same cycle type**.

Therefore the conjugacy classes of \(S_n\) correspond to the partitions of \(n\).

For example, the conjugacy classes of \(S_3\) correspond to the cycle types

\[
1+1+1,
\qquad
2+1,
\qquad
3.
\]

The interface displays:

- cycle type;
- class size;
- representative;
- representative order;
- parity.

---

## Cycle visualization

The application renders the selected permutation as a directed graph representing

\[
i\mapsto \sigma(i).
\]

Vertices correspond to the symbols

\[
1,\dots,n,
\]

and directed edges indicate their images under the permutation.

This visualization makes fixed points, transpositions, cycles, and more complicated cycle decompositions immediately visible.

---

## Theme and visual design

The interface uses a dark mathematical-workbench theme.

The design includes:

- dark navy / charcoal backgrounds;
- thin blue-gray borders;
- serif mathematical headings;
- compact high-contrast body text;
- monospace styling where appropriate;
- blue selection states;
- color-coded invariant cards;
- fixed left-side navigation;
- dense research-dashboard layouts;
- SVG mathematical visualizations.

The visual language is intended to resemble a small mathematical research tool rather than a generic consumer dashboard.

---

## Project structure

```text
s_n_explorer_web/
├── app.py
├── symmetric_group.py
│
├── static/
│   ├── index.html
│   ├── styles.css
│   └── app.js
│
├── tests/
│   └── test_engine.py
│
├── README.md
└── requirements.txt
```

### `app.py`

Implements the web server and API layer.

Responsibilities include:

- serving the frontend;
- routing API requests;
- validating parameters;
- calling the Python group-theory engine;
- serializing results as JSON.

### `symmetric_group.py`

Contains the mathematical engine.

It implements:

- generation of permutations;
- composition;
- inverses;
- cycle decomposition;
- permutation order;
- sign / parity;
- Cayley tables;
- dihedral groups;
- subgroup generation;
- subgroup enumeration;
- normality;
- cosets;
- quotient groups;
- conjugacy-class information.

### `static/index.html`

Defines the browser interface and major application panels.

### `static/styles.css`

Contains the dark mathematical-workbench theme and responsive layout.

### `static/app.js`

Handles:

- UI state;
- API requests;
- navigation;
- table rendering;
- permutation selection;
- cycle visualization;
- interactive controls.

### `tests/test_engine.py`

Contains mathematical regression tests for the algebra engine.

---

## Requirements

The application requires:

- Python 3;
- a modern web browser.

The current implementation does not require a JavaScript build system.

There is no Node.js bundling step and no frontend framework compilation step.

---

## Running the application

From the project directory, run:

```bash
python app.py
```

On Windows, depending on your Python configuration:

```bash
py app.py
```

Then open:

```text
http://127.0.0.1:8000
```

in your browser.

---

## Mathematical conventions

### Symmetric group

The symmetric group is

\[
S_n
=
\{\sigma:\{1,\dots,n\}\to\{1,\dots,n\}
\mid
\sigma\text{ is bijective}\}.
\]

Its order is

\[
|S_n|=n!.
\]

---

### Composition convention

The engine uses

\[
(\sigma\circ\tau)(i)=\sigma(\tau(i)).
\]

This is the standard right-to-left functional-composition convention.

---

### Internal representation

Internally, Python uses zero-based indices.

The user-facing interface displays the conventional mathematical labels

\[
1,\dots,n.
\]

Thus, internal storage follows Python indexing while the browser preserves standard algebraic notation.

---

## Computational safeguards

The size of \(S_n\) grows factorially:

| \(n\) | \(|S_n|=n!\) |
|---:|---:|
| 1 | 1 |
| 2 | 2 |
| 3 | 6 |
| 4 | 24 |
| 5 | 120 |
| 6 | 720 |
| 7 | 5,040 |
| 8 | 40,320 |

Different operations have very different computational costs.

The current application uses conservative limits so the browser remains responsive.

| Operation | Current limit |
|---|---:|
| Browse / inspect \(S_n\) | \(n\le 8\) |
| Composition | \(n\le 8\) |
| Conjugacy classes | \(n\le 8\) |
| Cayley table | \(n\le 4\) |
| Exhaustive subgroup enumeration | \(n\le 4\) |
| Generated subgroup exploration | \(n\le 7\) |
| Dihedral explorer | \(3\le m\le 24\) |

These limits are implementation safeguards rather than mathematical restrictions.

---

## Why some operations are expensive

### Permutation generation

The number of elements is

\[
n!.
\]

Thus the underlying set already grows factorially.

### Cayley tables

A complete Cayley table has

\[
(n!)^2
\]

entries.

For example,

\[
|S_6|=720,
\]

so its complete multiplication table would contain

\[
720^2=518{,}400
\]

products.

### Subgroup enumeration

Subgroup enumeration is substantially harder than listing elements because many candidate generating sets must be considered and their closures computed.

For this reason, exhaustive subgroup discovery is restricted to small groups.

---

## Tests

The project includes mathematical tests for the core engine.

Run them with:

```bash
python -m pytest
```

or, depending on the environment:

```bash
pytest
```

The test suite checks representative structural properties including:

- \(|S_3|=6\);
- permutation composition orientation;
- inverses;
- element orders;
- parity;
- subgroup structure of \(S_3\);
- normal subgroups;
- quotient structure;
- Cayley-table consistency;
- dihedral-group relations;
- conjugacy-class sizes.

---

## Example: \(S_3\)

The group

\[
S_3
\]

contains six permutations:

\[
e,
\quad
(1\ 2),
\quad
(1\ 3),
\quad
(2\ 3),
\quad
(1\ 2\ 3),
\quad
(1\ 3\ 2).
\]

Its structure includes:

\[
|S_3|=6;
\]

three transpositions;

two \(3\)-cycles;

three conjugacy classes;

alternating subgroup

\[
A_3
=
\{e,(1\ 2\ 3),(1\ 3\ 2)\};
\]

and quotient

\[
S_3/A_3\cong C_2.
\]

It is also isomorphic to the symmetry group of an equilateral triangle:

\[
S_3\cong D_3.
\]

For this reason, \(S_3\) is an especially useful group for demonstrating the main features of the application.

---

## Educational purpose

The project is intended for interactive exploration of:

- symmetric groups;
- finite groups;
- permutation notation;
- cycle decompositions;
- parity;
- alternating groups;
- element orders;
- group actions through permutation representations;
- Cayley tables;
- generators;
- subgroup closure;
- subgroup lattices;
- normality;
- cosets;
- quotient groups;
- conjugacy classes;
- dihedral groups.

The broader objective is to connect formal abstract algebra with direct computation and visualization.

---

## Relationship to the command-line explorer

The web application is an extension of the original command-line \(S_n\) Explorer.

The mathematical model remains in Python.

The web version adds:

- graphical navigation;
- interactive tables;
- immediate selection feedback;
- SVG cycle diagrams;
- visual subgroup and quotient exploration;
- conjugacy-class exploration;
- browser-based interaction.

The command-line application remains useful as a compact terminal-based algebra explorer, while the web version provides a richer exploratory environment.

---

## Repository

Source repository:

```text
https://github.com/danielsfrede/python_projects
```

The web application can be maintained as a separate project directory alongside the command-line implementation.
