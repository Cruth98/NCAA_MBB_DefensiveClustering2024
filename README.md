# NCAA MBB Defensive Clustering (2024)

This project performs **unsupervised clustering (K-Means)** on NCAA Division I teams to group programs with similar **defensive profile characteristics**, then layers in **KenPom roster size / height metrics** to enable more context-aware comparisons (e.g., identifying peer groups aligned with Bellarmine’s profile).

The core deliverable is an analysis workflow that:
1) engineers/selects defensive profile features,  
2) scales inputs,  
3) determines an appropriate cluster count using **Elbow Method + Silhouette Score**,  
4) assigns cluster labels, and  
5) analyzes the resulting clusters (including a focused deep-dive on Bellarmine’s cluster).

---

## Key Questions This Analysis Answers

- Which teams share similar defensive “shape” across core profile metrics?
- What cluster does Bellarmine fall into, and what are the characteristics of that cluster?
- Which peer teams can be used for **benchmarking, scouting, and strategic comparison**?
- How does roster size/height context (KenPom) relate to cluster membership?
- Of the team(s) with similar size profile to Bellarmine, which ones aligned with the most successful defensive cluster? 

---

## Data & Features

### Defensive Profile Features Used (Team-Level)
The clustering model is built from a selected subset of team profile metrics, including:

- `ORtg`
- `FTr`
- `3PAr`
- `TRB%`
- `AST%`
- `eFG%`
- `TOV%`
- `3 FG%`

> Note: Feature names reflect the column headers used in the notebook’s source dataset.

### Additional Context (Merged)
KenPom size/height context is merged into the clustered dataframe using:

- `Size`, `SizeRank`
- `Hgt5`, `Hgt4`, `Hgt3`, `Hgt2`, `Hgt1`

---

## Methodology

1. **Data loading + subsetting**
   - Loads team data and selects core defensive profile metrics.
   - Uses a team identifier mapping step (for consistent joining).

2. **Scaling**
   - Uses feature scaling before clustering to prevent high-variance metrics from dominating.

3. **K-Means clustering**
   - Evaluates candidate `k` values using:
     - **Elbow Method** (inertia)
     - **Silhouette Score**
   - Final model selection:
     - **k = 5 clusters** (chosen via elbow + silhouette evaluation)

4. **Cluster assignment + interpretation**
   - Appends cluster labels to the original dataframe.
   - Computes cluster distributions and summary statistics.

5. **Bellarmine cluster deep-dive**
   - Identifies Bellarmine’s assigned cluster and summarizes the peer group.

---

## Results (High Level)

- Teams are grouped into **5 clusters**, each representing a distinct defensive profile “type.”
- Cluster summary statistics are used to interpret what differentiates each cluster.
- A Bellarmine-specific analysis pulls all teams in the same cluster to identify:
  - peer comparisons
  - cluster ranges (min/max/mean by feature)
  - candidate benchmarks for further film + statistical evaluation

---

## Repository Contents

- `DefensiveTeamClustering.ipynb`  
  Main notebook containing the end-to-end workflow: feature prep → scaling → clustering → evaluation → interpretation.

---
