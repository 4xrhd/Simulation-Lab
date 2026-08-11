# Lab Performance 01 — Basic Matrix & Vector Operations in Simulation

**Course Code:** CSE 413 | **Credit:** 1.5  
**Instructor:** Afroja Ahmed Smrity  
**Notebook:** [`SIM_Lab1_Azhar_1120.ipynb`](Lab-performances/Lab-performance-01/SIM_Lab1_Azhar_1120.ipynb)  

---

## 📌 Short Revision Notes (Lab 1 Key Concepts)

### 1. Scalar & Array Operations
- **Scalar Operations**: Broadcast single numerical values across 1D arrays or matrices (e.g., `np.remainder(arr, 3.7)`).
- **Element-wise Functions**:
  - `np.sin(x)`, `np.cos(x)`, `np.tan(x)`: Trigonometric operations on radian inputs.
  - `np.exp(x)`: Exponential ($e^x$).
  - `np.log(x)`: Natural logarithm (base $e$).
  - `np.abs(x)`, `np.sqrt(x)`: Absolute value and square root.
  - `np.round(x)`, `np.floor(x)`, `np.ceil(x)`: Rounding to nearest integer, floor (round down), and ceiling (round up).

---

### 2. Domain Constraints & Clipping (`np.clip`)
- Inverse trigonometric functions (`np.arcsin`, `np.arccos`) are mathematically defined **only within $[-1, 1]$**.
- Values outside $[-1, 1]$ result in `NaN` warnings or domain errors.
- **Solution**: Always scale/normalize inputs and enforce domain safety using `np.clip()`:
  ```python
  asin_values = np.arcsin(np.clip(matrix / np.max(matrix), -1, 1))
  acos_values = np.arccos(np.clip(matrix / np.max(matrix), -1, 1))
  ```

---

### 3. Matrix & Vector Analysis (2D Arrays)
- **Shape & Dimensions**:
  - 3×2 Matrix: 3 rows, 2 columns.
  - 2×3 Matrix: 2 rows, 3 columns.
- **Index Extraction**:
  - `np.argmax(matrix)` / `np.argmin(matrix)` returns the index in a flattened 1D array.
  - Convert flat index to 2D coordinates `(row, column)` using `np.unravel_index()`:
    ```python
    row_col = np.unravel_index(np.argmax(matrix), matrix.shape)
    ```
- **Vector Length**: Total element count is obtained via `matrix.size` (equivalent to 1D vector length).
- **Statistics**:
  - `np.sum()`, `np.prod()`: Total sum and product across all elements.
  - `np.median()`, `np.mean()`, `np.std()`: Median, arithmetic mean, and standard deviation.

---

### 4. Sorting Techniques
- **Row-wise Descending Sort**:
  1. Sort along rows (`axis=1`): `np.sort(matrix, axis=1)`.
  2. Reverse each row along columns (`[:, ::-1]`):
     ```python
     row_sorted_desc = np.sort(matrix, axis=1)[:, ::-1]
     ```
- **Entire Matrix Descending Sort**:
  1. Flatten matrix to 1D array: `matrix.flatten()`.
  2. Sort and reverse:
     ```python
     total_sorted_desc = np.sort(matrix.flatten())[::-1]
     ```

---

### 5. Visualization & Random Input Generation
- **Random Uniform Numbers**: `np.random.uniform(low, high, size=(rows, cols))` generates floating-point matrix entries uniformly within specified bounds.
- **Seaborn Heatmap**:
  ```python
  import seaborn as sns
  import matplotlib.pyplot as plt

  sns.heatmap(matrix, annot=True, cmap="YlGnBu", fmt=".2f")
  plt.title("Matrix Heatmap Visualization")
  plt.show()
  ```
