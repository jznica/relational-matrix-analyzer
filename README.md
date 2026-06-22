# Relational Matrix Analyzer

**Discrete-mathematics analysis of social-network interactions — relations, properties, and graph structure.**

A single-file web application that models a social network as a *relation* on a set of users, represents it as a binary matrix **R**, and automatically derives its mathematical properties and network structure. It visualizes the same data two ways — as an adjacency matrix/heatmap and as a live force-directed graph.

> Built for **UBA0401 – Discrete Mathematics for Intelligent Data and Artificial Intelligence** as a B.Tech (AIML) capstone project.

---

## The idea

A social network is just a relation: a finite set of users **U** and a rule **R ⊆ U × U** describing who is connected to whom. Any such relation can be written as a binary matrix where

```
R[i][j] = 1  →  user i is connected to user j
R[i][j] = 0  →  no connection
```

Once the network is a matrix, the abstract properties of relations from discrete mathematics — reflexivity, symmetry, transitivity — become concrete, computable facts about the social structure (self-ties, mutual friendships, friend-of-a-friend reachability, communities). This tool computes all of them automatically and keeps the matrix and graph views in sync.

---

## Features

- **Editable relation matrix.** Click any cell to toggle a connection, rename users inline, resize from 2 to 12 users, and switch between **undirected** (mutual ties) and **directed** (one-way follows) modes.
- **Automatic property analysis.** Reflexive, irreflexive, symmetric, antisymmetric, and transitive checks — each with its formula and the exact users/pairs that violate it. Detects **equivalence relations** and **partial orders**.
- **Two visualizations.** An adjacency **heatmap** graded by tie strength, and a **force-directed network graph** where node size = degree and colour = community.
- **Transitive closure (Warshall's algorithm).** Overlays the indirect "friend-of-a-friend" links the relation implies.
- **Shortest-path tracer (BFS).** Finds and highlights the shortest chain of connections — the degrees of separation — between any two users.
- **Network metrics.** Density, mutual ties, isolated users, self-loops, hub (most connected user), and **communities via connected components**.
- **Cross-highlighting.** Hover a matrix cell to light up its edge in the graph; hover a graph node to highlight its row and column in the matrix.
- **Sample datasets and a random-network generator** for quick demos.
- **Save and load.** Export the project as `.json`, the matrix as `.csv`, or the graph as a `.png`; import a saved `.json`. Work auto-saves to the browser.
- **Responsive** and **reduced-motion** friendly.

---

## The mathematics

| Concept | Definition | In the tool |
|---|---|---|
| Reflexive | ∀i, R[i][i] = 1 | Whole diagonal is a connection |
| Irreflexive | ∀i, R[i][i] = 0 | No user relates to themselves |
| Symmetric | R[i][j] = R[j][i] | Every tie is mutual |
| Antisymmetric | ¬(R[i][j] ∧ R[j][i]) for i ≠ j | No two-way ties between distinct users |
| Transitive | R[i][j] ∧ R[j][k] ⟹ R[i][k] | Indirect links are already direct |
| Equivalence relation | Reflexive ∧ Symmetric ∧ Transitive | Partitions users into communities |
| Transitive closure | Smallest transitive relation containing R | Computed with Warshall's algorithm |

**Complexity:** property checks run in O(n²), transitivity and the transitive closure in O(n³), and BFS path-finding and connected-component detection in O(n²) on the adjacency matrix.

---

## Tech stack

- **Vanilla JavaScript** — no frameworks, no build step
- **HTML5 Canvas** for the force-directed graph and its physics simulation
- **CSS Grid / Flexbox** for layout, custom properties for theming
- **localStorage** for persistence
- Zero runtime dependencies; the only external request is web fonts (the app works offline once cached)

---

## Getting started

### Run locally

Clone the repository and open the file — that's it.

```bash
git clone https://github.com/<your-username>/relational-matrix-analyzer.git
cd relational-matrix-analyzer
# then just open the HTML file in any modern browser
```

No installation, server, or build is required.

### Deploy to Vercel

Rename the file to `index.html`, push to GitHub, and import the repo in Vercel — it deploys as a static site with no configuration.

```bash
mv relational-matrix-analyzer.html index.html
```

---

## How to use it

1. **Load a sample** from the sidebar, or build a network from scratch by clicking matrix cells.
2. **Choose the edge type** — *undirected* for mutual friendships, *directed* for one-way follows.
3. **Read the properties panel** to see which relation properties hold and why.
4. **Toggle Heatmap** to view tie strength, or **R\*** to overlay the transitive closure.
5. **Trace a path** between two users with the BFS path finder.
6. **Export** your project as JSON/CSV or save the graph as a PNG.

### Sample datasets

| Dataset | Type | Demonstrates |
|---|---|---|
| Friend circle | Undirected | Symmetric, mutual ties |
| Follower graph | Directed | One-way (asymmetric) relations |
| Study group | Directed | A transitive / total-order structure |
| Equivalence (3 cliques) | Undirected | An equivalence relation and its partition |
| Two communities + loner | Undirected | Multiple components and an isolated user |

---

## Project structure

```
relational-matrix-analyzer/
├── index.html        # the entire application (markup, styles, and logic)
└── README.md
```

The whole tool lives in one self-contained HTML file for portability and easy submission.

---

## Roadmap

- Weighted relations (interaction strength rather than binary 0/1)
- Real-time updates from live social-graph data
- Support for larger networks with zoom, pan, and filtering
- Additional metrics: betweenness centrality, clustering coefficient

---

## Team

**Team 1 — B.Tech, Artificial Intelligence and Machine Learning**

- Pavesh R — 192425010
- Kaviya Kumara K — 19245055
- Niranjan D — 192424028

**Supervisors:** Dr. T. Lawanya · Dr. A. Kanchana

**Course:** UBA0401 – Discrete Mathematics for Intelligent Data and Artificial Intelligence

---

## License

Released under the MIT License. See `LICENSE` for details.
