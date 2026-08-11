# Class Performance 02 — Matrix Operations & Vector Visualizations

**Course Code:** CSE 413 | **Credit:** 1.5  
**Instructor:** Afroja Ahmed Smrity  
**Notebook:** [`Student_CP2_Azhar_1120.ipynb`](file:///home/tr/Desktop/LAB-uni/simulation-lab/lab3/Student_CP2_Azhar_1120.ipynb)  
**Task Specification Document:** [`CP2 7B2.pdf`](file:///home/tr/Desktop/LAB-uni/simulation-lab/lab3/CP2%207B2.pdf)  

---

## 📌 Short Revision Notes (CP2 Key Concepts)

### 1. Vector Generation & Comparison Plotting (`CP2 7B2.pdf` - Task 1)
- **15-Element Random Vectors**: Generated using `np.random.rand(15)`.
- **Matplotlib Line Graph (`plt.plot`)**:
  - Plots two vectors on the same graph to compare distributions across element indices $1$ to $15$.
  - Includes custom markers (`o`, `s`), line styles (`-`, `--`), colors, axis labels, grid, and legend.

---

### 2. Matrix Operations & Bar Plot Visualizations (`CP2 7B2.pdf` - Task 2)
- **4×4 Random Matrices**: Generated using `np.random.randint(1, 10, size=(4, 4))`.
- **Matrix Addition ($A + B$)**: Element-wise addition $(a_{ij} + b_{ij})$.
- **Matrix Subtraction ($A - B$)**: Element-wise subtraction $(a_{ij} - b_{ij})$.
- **Matrix Multiplication ($A \cdot B$)**: Dot product via `np.dot(A, B)` (compatible $4 \times 4$ matrix multiplication).
- **Element-wise Bar Plots (`plt.subplots`, `axes[i].bar`)**:
  - Each 4×4 matrix is flattened (`matrix.flatten()`) into 16 elements.
  - Subplots display 16 distinct bars per operation representing individual element values.

---

### 3. Matrix Fundamentals & Heatmaps
- **Special Matrices**: Identity (`np.eye`), Zero (`np.zeros`), Ones (`np.ones`), Diagonal (`np.diag`), Upper/Lower Triangular (`np.triu`/`np.tril`).
- **Linear Algebra**: Determinant (`np.linalg.det`), Rank (`np.linalg.matrix_rank`), Inverse (`np.linalg.inv`), Eigenvalues & Eigenvectors (`np.linalg.eig`), Characteristic Polynomial & Roots (`np.poly`/`np.roots`).
- **Heatmap (`sns.heatmap`)**: Visualizes 2D float matrices with color intensity maps (`cmap='coolwarm'`).
