# Train Single-Routing Selection Problem (TSRSP) — Instance Repository

This repository contains the full benchmark dataset used in the work:

> **A Novel and Effective Formulation for the Train Single-Routing Selection Problem**  
> Anna Livia Croella, Fabio Furini, Ivana Ljubić, Bianca Pascariu, Paola Pellegrini, Pablo San Segundo  
> Submitted to _Transportation Research Part B_, July 2025  
<br>

## 🧩 Problem Overview

The **Train Single-Routing Selection Problem (TSRSP)** arises in the context of real-time railway traffic management. It consists in selecting exactly one feasible route per train from a predefined set of alternatives, in such a way that:

- The total cost — including route-specific delays and delay-induced penalties from route interactions — is minimized;
- All selected routes are pairwise compatible.

This problem can be modeled as the search for a minimum-weight **k-clique** in a **k-partite compatibility graph**, where each vertex represents a route and each layer corresponds to a train. Compatibility is encoded by edges between vertices of distinct layers, with associated pairwise (pairing) costs.

In the referenced article, we:
- Introduce a novel and effective MILP formulation based on a compact linearization of a Binary Quadratic Programming (BQP) model;
- Propose a strengthening of the LP relaxation tailored to the TSRSP structure;
- Perform a detailed theoretical and computational comparison against existing formulations;
- Present the first optimal solutions for large-scale real-world instances of the TSRSP.
<br>


## 🗂️ Repository Structure

The repository is organized into two main directories, corresponding to the two railway networks under study:

### 🛤️ `Rouen/`

This directory includes all instances derived from the **Rouen Railway Network**. Instances are grouped by the edge density of the compatibility graph:

- `Rouen/Rouen/` — Layer-wise complete graphs (ε = 1.0)
- `Rouen/Rouen_90/` — Graphs with 10% of compatibility edges randomly removed (ε = 0.9)
- `Rouen/Rouen_80/` — Graphs with 20% of compatibility edges removed (ε = 0.8)

Each of these contains two subfolders:
- `_Peak/` — Instances derived from peak-hour traffic scenarios
- `_OffPeak/` — Instances derived from off-peak-hour traffic scenarios

### 🛤️ `Lille/`

This directory contains instances built on the **Lille Railway Network**, characterized by higher congestion and denser route graphs:

- `Lille/Lille_Peak/` — Peak-time instances
- `Lille/Lille_OffPeak/` — Off-peak-time instances
<br>


### 🔍 Instance Format

Each subfolder (e.g., `Lille/Lille_Peak/`) contains several instance directories named: `scenario_1/`, `scenario_2/`, ..., `scenario_XXX/`.
Each `scenario_XXX/` folder contains **four files**, encoding the full input data for one TSRSP instance:

- `scenario_XXX.data`: encodes the **compatibility graph** in DIMACS-like format.  
  - The file begins with a `p edge n m` line indicating the number of vertices (n) and edges (m).  
  - Each subsequent line of the form `e u v` defines an undirected edge {u, v} representing a pair of compatible routes belonging to two distinct trains.

- `scenario_XXX.p`: provides the **assignment of each route (vertex) to its train** (layer).  
  - The file lists one integer per line, indicating the layer index for the corresponding vertex.

- `scenario_XXX.q`: contains the **route cost vector**.  
  - Each entry represents the cost associated with assigning a specific route to its corresponding train.

- `scenario_XXX.r`: lists the **pairing costs** associated with the edges in `scenario_XXX.data`.  
  - Each line corresponds to one edge in the order they appear in the `.data` file.

<br>


### 🧮 Reference Example
<p align="center">
  <img width="412" height="215" alt="image" src="https://github.com/user-attachments/assets/51ddc561-c733-4db3-842b-4937ca2567fd" />
</p>

*Figure 1* reports the compatibility graph for a TSRSP instance with:
- **k = 3** trains (layers),  
- **n = 9** total routes (vertices),  
- **m = 16** compatibility edges,  
- Edge density ε = 16⁄26 ≈ 0.615.  
- The optimal 3-clique consists of routes `{2, 5, 8}` with a total cost (clique weight) of **16**.

The corresponding files for this illustrative instance, contained in the `example/` folder, are:
- `example.data` — lists the 16 edges of the compatibility graph  
- `example.p` — route-to-train mapping  
- `example.q` — route costs  
- `example.r` — pairing costs.

These files are syntactically and semantically consistent with all other instances in the repository.

<br>

## 📚 Citation

If you use this dataset in academic work, please cite:

```
@article{Croella2025TSRSP,
  title={A novel and effective formulation for the Train Single-Routing Selection Problem},
  author={Croella, A.L. and Furini, F. and Ljubić, I. and Pascariu, B. and Pellegrini, P. and San Segundo, P.},
  year={2025}
}
```
<br>

## 📬 Contact

For questions, feedback, or collaboration inquiries, please contact:

- **Anna Livia Croella** – [annalivia.croella@unimercatorum.it](mailto:annalivia.croella@unimercatorum.it)

