# Experiment 19 — Real-World and Interactive Visualizations in Python

**Name:** Lakshya Sonawane &nbsp;|&nbsp; **PRN:** 25070123068

---

## Introduction

Standard charts like bar graphs and scatter plots work well for simple datasets, but real-world analytical problems often require **specialized and interactive visualizations** to communicate complex, multi-dimensional, or hierarchical data effectively. Interactive charts allow users to zoom, hover, and explore data — making them ideal for dashboards and presentations.

This experiment demonstrates six advanced visualization techniques — **Treemap, Dendrogram, Venn Diagram, Sankey Diagram, 3D Scatter Plot, and Radar Chart** — using **Plotly** (for interactive charts) and **Matplotlib/SciPy** (for static specialized charts). Each technique is applied to a real-world inspired dataset to demonstrate practical use cases.

---

## Requirements

```python
pip install plotly matplotlib scipy matplotlib-venn pandas numpy
```

```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import plotly.express as px
import plotly.graph_objects as go
from scipy.cluster.hierarchy import dendrogram, linkage
from matplotlib_venn import venn2
```

---

## Theory & Commands

### 1. Treemap

A Treemap represents **hierarchical data using nested rectangles**. Each rectangle's size corresponds to the value of the category it represents. Larger rectangles contain smaller child rectangles, showing the proportion of each part within the hierarchy. It is ideal for visualizing budget allocations, file system usage, or market share breakdowns.

```python
import pandas as pd
import plotly.express as px

df = pd.DataFrame({
    'Department': ['HR', 'IT', 'Sales', 'Marketing'],
    'Budget': [20000, 50000, 40000, 30000]
})

fig = px.treemap(df,
                 path=['Department'],   # hierarchy levels
                 values='Budget',
                 title="Company Budget Distribution")

fig.show()
```

**Key parameters of `px.treemap()`:**

| Parameter | Purpose |
|---|---|
| `path` | List defining hierarchy levels (e.g., `['Region', 'Department']`) |
| `values` | Numerical column that determines rectangle size |
| `color` | Column to control color encoding |

> **When to use:** Budget allocation, disk usage breakdown, sales by category and subcategory.

---

### 2. Dendrogram

A Dendrogram is a **tree-like diagram** produced by hierarchical clustering. It shows how individual data points are progressively grouped into clusters based on similarity. The **height (Y-axis)** at which two branches merge represents the **distance or dissimilarity** between those clusters — lower merges = more similar.

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.cluster.hierarchy import dendrogram, linkage

# Sample 2D data points
data = np.array([
    [5, 3],
    [10, 15],
    [15, 12],
    [24, 10],
    [30, 30]
])

# Perform hierarchical clustering (Ward's method minimizes variance)
linked = linkage(data, method='ward')

plt.figure(figsize=(6, 4))
dendrogram(linked)
plt.title('Hierarchical Clustering — Dendrogram')
plt.xlabel('Data Points')
plt.ylabel('Distance')
plt.show()
```

**Linkage methods:**

| Method | Description |
|---|---|
| `ward` | Minimizes within-cluster variance (most common) |
| `single` | Distance between closest points of two clusters |
| `complete` | Distance between farthest points of two clusters |
| `average` | Average distance between all point pairs |

> **When to use:** Identifying natural groupings in data; choosing the number of clusters before K-Means.

---

### 3. Venn Diagram

A Venn Diagram uses **overlapping circles to show relationships between sets**. Each circle represents a set, the **overlapping area** shows common elements, and the **non-overlapping areas** show elements unique to each set.

```python
import matplotlib.pyplot as plt
from matplotlib_venn import venn2

# Define sets
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}

venn2([A, B], set_labels=('Set A', 'Set B'))
plt.title('Venn Diagram — Set Intersection')
plt.show()
```

**Interpreting the diagram:**

| Region | Meaning |
|---|---|
| Left only (Set A) | Elements only in A: `{1, 2}` |
| Overlap | Elements in both A and B: `{3, 4}` |
| Right only (Set B) | Elements only in B: `{5, 6}` |

> **When to use:** Comparing two or three groups — common customers, shared features, mutual skills.

---

### 4. Sankey Diagram

A Sankey Diagram visualizes **flow and quantity between nodes**. The width of each flow (link) is proportional to the quantity it represents. It is excellent for showing how a resource (students, money, traffic) moves from one stage to another.

```python
import plotly.graph_objects as go

fig = go.Figure(data=[go.Sankey(
    node=dict(
        label=["Admission", "First Year", "Second Year", "Placed"]
    ),
    link=dict(
        source=[0, 1, 2],   # index of source node
        target=[1, 2, 3],   # index of target node
        value=[100, 80, 60] # flow quantity
    )
)])

fig.update_layout(title_text="Student Flow — Sankey Diagram")
fig.show()
```

**Reading the diagram:** 100 students admitted → 80 reach Second Year → 60 get placed. The shrinking widths visually show dropout/attrition at each stage.

> **When to use:** Student progression, energy flow, budget allocation across stages, website traffic funnel.

---

### 5. 3D Scatter Plot

A 3D Scatter Plot extends the standard scatter plot to **three numerical dimensions** (X, Y, Z axes), allowing visualization of relationships among three variables simultaneously. Plotly makes these interactive — you can rotate, zoom, and hover for exact values.

```python
import pandas as pd
import plotly.express as px

df = pd.DataFrame({
    'Study_Hours': [2, 4, 6, 8, 5],
    'Marks':       [50, 65, 75, 90, 70],
    'Attendance':  [60, 75, 80, 90, 70]
})

fig = px.scatter_3d(df,
                    x='Study_Hours',
                    y='Marks',
                    z='Attendance',
                    title="Student Performance Analysis (3D)")

fig.show()
```

**Axes mapping:**

| Axis | Variable | Insight |
|---|---|---|
| X | Study Hours | Input effort |
| Y | Marks | Academic output |
| Z | Attendance | Engagement metric |

> **When to use:** Scientific analysis, multi-variable ML feature exploration, 3D spatial data.

---

### 6. Radar Chart (Spider Chart)

A Radar Chart (also called a Spider or Web Chart) plots **multiple variables on axes radiating from the center**. Each axis represents one skill/metric, and the filled polygon shows the overall profile. It is ideal for comparing performance or capabilities across multiple dimensions.

```python
import plotly.graph_objects as go

skills = ['Python', 'ML', 'DBMS', 'DSA', 'Communication']
values = [4, 3, 5, 4, 3]

fig = go.Figure()

fig.add_trace(go.Scatterpolar(
    r=values,          # radial values (scores)
    theta=skills,      # angular axis labels
    fill='toself',     # fill the enclosed area
    name='Student Skills'
))

fig.update_layout(
    polar=dict(radialaxis=dict(visible=True, range=[0, 5])),
    title="Skill Assessment — Radar Chart"
)

fig.show()
```

> **When to use:** Employee performance reviews, student skill profiles, product feature comparison, sports analytics.

---

## Visualization Techniques — Summary

| Chart | Library | Variables | Best For |
|---|---|---|---|
| Treemap | Plotly Express | Hierarchical + numerical | Budget/market share breakdown |
| Dendrogram | Matplotlib + SciPy | Numerical (2D points) | Hierarchical clustering |
| Venn Diagram | matplotlib-venn | Set data | Set intersection/union |
| Sankey Diagram | Plotly Graph Objects | Flow + quantity | Stage-wise flow analysis |
| 3D Scatter Plot | Plotly Express | 3 numerical | Multi-variable relationship |
| Radar Chart | Plotly Graph Objects | Multi-metric scores | Multi-dimensional profiles |

---

## Matplotlib vs Plotly

| Feature | Matplotlib | Plotly |
|---|---|---|
| Output | Static image | Interactive (zoom, hover, rotate) |
| 3D support | Basic (`mpl_toolkits`) | Full interactive 3D |
| Ease for complex charts | More code needed | Concise, declarative API |
| Dashboard integration | Limited | Works with Dash, Jupyter |
| Best for | Quick static charts | Interactive, shareable charts |

---

## Conclusion

This experiment explored six advanced visualization techniques applied to real-world inspired datasets:

- **Treemaps** provide an intuitive view of hierarchical proportional data — the size of each rectangle immediately communicates relative magnitude.
- **Dendrograms** visualize the result of hierarchical clustering and help determine natural groupings in data, with branch height representing inter-cluster distance.
- **Venn Diagrams** clearly illustrate set relationships — what is unique to each group and what is shared between them.
- **Sankey Diagrams** are powerful for showing stage-wise flow and attrition — the shrinking link widths visually communicate quantity lost at each transition.
- **3D Scatter Plots** using Plotly provide interactive exploration of three-variable relationships, with rotation and hover revealing patterns invisible in 2D.
- **Radar Charts** offer a compact multi-dimensional view of performance profiles, making it easy to compare strengths and weaknesses across several metrics simultaneously.

Plotly's interactivity makes it the preferred tool for real-world dashboards and presentations, while Matplotlib and SciPy remain powerful for static, publication-ready charts.

---

## Libraries Used

| Library | Purpose |
|---|---|
| `plotly.express` | Treemap, 3D Scatter Plot |
| `plotly.graph_objects` | Sankey Diagram, Radar Chart |
| `matplotlib.pyplot` | Dendrogram, Venn Diagram base |
| `scipy.cluster.hierarchy` | `linkage()` and `dendrogram()` for clustering |
| `matplotlib_venn` | `venn2()` for Venn Diagrams |
| `pandas` | DataFrame creation and manipulation |
| `numpy` | Numerical array operations |
