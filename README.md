# Experiment 19 — Real-World and Interactive Visualizations

**Name:** Lakshya Sonawane &nbsp;|&nbsp; **PRN:** 25070123068

---

## 📌 Introduction

Complex real-world data requires visualizations that are interactive, multi-dimensional, and capable of representing hierarchical or flow-based structures. This experiment covers **Treemap, Dendrogram, Venn Diagram, Sankey Diagram, 3D Scatter Plot, and Radar Chart** using **Plotly** (interactive) and **Matplotlib/SciPy** (static), applied to scenarios like budget allocation, student progression, clustering, and skill assessment.

---

## 📖 Theory

### 1. Treemap — Hierarchical Part-to-Whole
- Represents hierarchical data as nested rectangles; area is proportional to a quantitative value
- Built using `px.treemap()` where `path` defines the hierarchy levels and `values` sets rectangle sizes
- Ideal for visualizing budget or resource distribution interactively across categories

### 2. Dendrogram — Hierarchical Clustering
- Tree diagram showing how data points are progressively merged based on similarity (distance)
- Linkage matrix computed using `linkage(data, method='ward')` from `scipy.cluster.hierarchy`; rendered with `dendrogram(linked)`
- The y-axis (linkage distance) indicates dissimilarity — higher merge point means more different clusters

### 3. Venn Diagram — Set Relationships
- Overlapping circles show intersections, unions, and differences between sets
- Created using `venn2([A, B], set_labels=('Set A','Set B'))` from the `matplotlib_venn` library
- Overlapping region automatically represents the intersection; non-overlapping regions are set-exclusive elements

### 4. Sankey Diagram — Flow Visualization
- Visualizes how quantities move through sequential stages; link width is proportional to flow value
- Built with `go.Sankey()` using `node` for stage labels and `link` with `source`, `target`, and `value` lists
- Plotly's interactivity enables hover tooltips showing exact flow amounts at each stage

### 5. 3D Scatter Plot — Multi-Dimensional Analysis
- Positions each observation in 3D space defined by three numerical variables
- Created using `px.scatter_3d()` with `x`, `y`, and `z` column parameters
- Plotly renders a fully rotatable, zoomable interactive plot with per-point hover annotations

### 6. Radar Chart — Multi-Attribute Profile
- Maps multiple attributes onto equally spaced radial axes, connecting values to form a polygon
- Built using `go.Scatterpolar()` with `r` (values), `theta` (attribute names), and `fill='toself'`
- Enclosed polygon area reflects overall strength; asymmetric shape highlights relative weaknesses

---

## ✅ Conclusion

- Six advanced chart types were implemented to handle hierarchical, clustered, flow-based, 3D, and multi-attribute data
- Plotly's interactivity — hover, zoom, and rotation — makes these charts far more informative than static alternatives
- These visualization types are directly applicable to dashboards, research, and industry-level analytics
