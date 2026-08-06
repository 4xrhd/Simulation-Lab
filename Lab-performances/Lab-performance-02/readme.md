# Lab Performance 02 — Unique Matrix Value Investigation

**Course Code:** CSE 413 | **Credit:** 3  
**Instructor:** Afroja Ahmed Smrity  
**Notebook:** [`SIM_Lab2_Azhar_1120.ipynb`](file:///home/tr/Desktop/LAB-uni/simulation-lab/Lab-performances/Lab-performance-02/SIM_Lab2_Azhar_1120.ipynb)  

---

## 📌 Short Revision Notes (Lab 2 Key Concepts)

### 1. Matrix Generation from Student ID
- Student ID digits $d1$ (last digit) and $d2$ (second last digit) parameterize the individual matrix $A$:
  $$A = \begin{bmatrix} d1 + 2 & d2 + 1 \\ 2 \cdot d1 & d2 + 2 \end{bmatrix}$$
- For ID `1120`, $d1 = 0$ and $d2 = 2$:
  $$A = \begin{bmatrix} 2 & 3 \\ 0 & 4 \end{bmatrix}$$

---

### 2. Matrix Properties & Computations
- **Shape & Dimensions**: Size of matrix rows and columns (`A.shape`).
- **Determinant ($\det$)**: For a $2 \times 2$ matrix $\begin{bmatrix} a & b \\ c & d \end{bmatrix}$, $\det(A) = ad - bc$.
- **Rank**: Maximum number of linearly independent row or column vectors (`np.linalg.matrix_rank(A)`). A $2 \times 2$ matrix has full rank ($2$) if $\det \neq 0$.
- **Eigenvalues ($\lambda$)**: Roots of the characteristic polynomial $\det(A - \lambda I) = 0$. For triangular matrices, eigenvalues equal diagonal elements.
- **Matrix Inversion ($A^{-1}$)**:
  $$A^{-1} = \frac{1}{\det(A)} \begin{bmatrix} d & -b \\ -c & a \end{bmatrix} \quad (\text{if } \det(A) \neq 0)$$

---

### 3. Matrix Perturbation & Value Change Effects
- **Modifying Off-Diagonal Entries**: Changing $A_{1,0}$ from $0$ to $1$ converts an upper-triangular matrix into a full dense matrix $B$:
  $$B = \begin{bmatrix} 2 & 3 \\ 1 & 4 \end{bmatrix}$$
- **Determinant Shift**: $\det(B) = (2 \times 4) - (3 \times 1) = 5$ (decreased by $3$).
- **Rank Invariance**: Rank remains $2$ because $\det(B) \neq 0$.
- **Eigenvalue Coupling**: Trace $\text{Tr}(B) = \lambda_1 + \lambda_2 = 6$ is conserved, but eigenvalues spread from $\{2, 4\}$ to $\{1, 5\}$.
- **Inversion Complexity**: Upper-triangular $A$ can be inverted via simple back-substitution, whereas full matrix $B$ requires full elimination and non-integer cofactors.
