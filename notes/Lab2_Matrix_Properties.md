# Revision Notes — Lab 2: Matrix Properties & Linear Algebra

**Course Code:** CSE 413 | **Credit:** 1.5  
**Instructor:** Afroja Ahmed Smrity  

---

## 🔑 Key Mathematical & Computational Concepts

### 1. Determinant ($\det$)
- For a $2 \times 2$ matrix $\begin{bmatrix} a & b \\ c & d \end{bmatrix}$, $\det(A) = ad - bc$.
- A matrix is invertible if and only if $\det(A) \neq 0$.

### 2. Rank of a Matrix
- The rank represents the maximum number of linearly independent rows or columns (`np.linalg.matrix_rank(A)`).
- A square $n \times n$ matrix has full rank $n$ if $\det(A) \neq 0$.

### 3. Eigenvalues ($\lambda$) and Eigenvectors ($\mathbf{v}$)
- Eigenvectors satisfy $A \mathbf{v} = \lambda \mathbf{v}$.
- Eigenvalues measure the scaling factor along eigenvector directions.
- Derived by solving the characteristic equation $\det(A - \lambda I) = 0$.
- In NumPy:
  ```python
  eigenvalues, eigenvectors = np.linalg.eig(A)
  ```

### 4. Characteristic Polynomial & Roots
- Coefficients obtained via `np.poly(A)`.
- Roots of the polynomial give the matrix eigenvalues:
  ```python
  char_poly = np.poly(A)
  roots = np.roots(char_poly)
  ```

### 5. Matrix Inversion & Singularity
- Inverse matrix $A^{-1}$ satisfies $A A^{-1} = I$.
- Check singularity before computing inverse:
  ```python
  if np.linalg.det(A) != 0:
      inv_A = np.linalg.inv(A)
  ```
