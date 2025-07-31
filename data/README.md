# Train Single-Routing Selection Problem (TSRSP) — Instance Repository

## 🗂️ Repository Structure

The repository is organized into two main (.zip) directories, corresponding to the two railway networks under study:

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


## 📊 Instance Statistics

Complete statistics for the **Rouen** and **Lille** railway networks are available in the following files:
- [`Rouen.pdf`](./tables/Rouen.pdf);
- [`Lille.pdf`](./tables/Lille.pdf).

The tables in these two PDF files report the following key statistics for each instance:

- Number of trains ($k$);
- Number of routes ($|\mathcal{V}|$);
- Number of compatibility edges ($|\mathcal{E}|$);
- Information on the objective function values ($Obj$).

For the **Rouen** instances, all instances were solved to optimality. The corresponding table reports the **minimum and maximum optimal objective values** for each group of instances.  
The complete list of optimal values for all Rouen instances is available in the Excel file [`/data/Computational_Results.xlsx`](../data/Computational_Results.xlsx), in the spreadsheet associated with formulation $G$.

For the **Lille** instances, only three instances—$L_1$, $L_2$, and $L_3$—were solved to optimality. Their respective rows report the optimal solution values.  
For all remaining instances, the column reports the **best known upper bound** obtained within the time limit (300-seconds).
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
<br>