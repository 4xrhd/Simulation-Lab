# Class Performance 02 — Matrix Operations, Eigenvalues & Data Visualization

**Course Code:** CSE 413 | **Credit:** 1.5  
**Instructor:** Afroja Ahmed Smrity  
**Notebook:** [`Student_CP2_Azhar_1120.ipynb`](file:///home/tr/Desktop/LAB-uni/simulation-lab/lab3/Student_CP2_Azhar_1120.ipynb)  

---

## 📌 Short Revision Notes (Class Performance 2 Key Concepts)

### 1. Special Matrix Types in NumPy
- **Identity Matrix (`np.eye(n)`)**: Square matrix with 1s on main diagonal and 0s elsewhere.
- **Zero & Ones Matrices (`np.zeros`, `np.ones`)**: Arrays initialized with all 0s or all 1s.
- **Diagonal Matrix (`np.diag`)**: Constructs or extracts a diagonal matrix.
- **Triangular Matrices (`np.triu`, `np.tril`)**: Extracts upper or lower triangular portions.

---

### 2. Matrix Linear Algebra Properties
- **Determinant (`np.linalg.det`)**: Scalar value representing scaling factor of linear transformation.
- **Rank (`np.linalg.matrix_rank`)**: Count of linearly independent row/column vectors.
- **Matrix Inverse (`np.linalg.inv`)**: Computes $A^{-1}$ such that $A A^{-1} = I$ (valid only when $\det(A) \neq 0$).
- **Eigenvalues & Eigenvectors (`np.linalg.eig`)**:
  - Eigenvectors $\mathbf{v}$ satisfy $A \mathbf{v} = \lambda \mathbf{v}$ (direction invariant under matrix transformation).
  - Eigenvalues $\lambda$ quantify the stretching or shrinking factor.
- **Characteristic Polynomial (`np.poly`, `np.roots`)**: Solves $\det(A - \lambda I) = 0$ to derive characteristic polynomial coefficients and roots.

---

### 3. Matrix & Vector Visualization
- **Line Plot (`plt.plot`)**: Displays 1D vector values or flattened matrix elements across indices.
- **Scatter Plot (`plt.scatter`)**: Compares paired values $(x_i, y_i)$ across two random vectors to inspect distribution/correlation.
- **Heatmap (`sns.heatmap`)**: Visualizes 2D matrix magnitude with color scales (`cmap='coolwarm'`).
- **Subplot Bar Charts (`plt.subplots`, `axes[i].bar`)**: Compares element-wise results of matrix operations (addition, subtraction, multiplication).
