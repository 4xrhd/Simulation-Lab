# Simulation Lab — Lab Day 1
## Basic NumPy Operations, Matrix Calculations & Visualization

**Course Code:** CSE 413 | **Credit:** 1.5  
**Instructor:** Afroja Ahmed Smrity  
**Notebooks:** [`SIM_Lab1_Azhar_1120.ipynb`](SIM_Lab1_Azhar_1120.ipynb), [`SIM_Lab_Day 1.ipynb`](SIM_Lab_Day%201.ipynb)  

---

## 📌 Topics Covered

1. **Scalar & Array Arithmetic**:
   - Scalar broadcasting across 1D arrays (`arr + scalar`, `arr * scalar`).
   - Power operations using `np.power`.

2. **Element-wise Mathematical & Trigonometric Functions**:
   - `np.abs()`, `np.sqrt()`, `np.exp()`, `np.log()`, `np.log10()`.
   - `np.sin()`, `np.cos()`, `np.tan()`.
   - Domain clipping (`np.clip(arr, -1, 1)`) for `np.arcsin()` and `np.arccos()`.

3. **2D Matrix Operations**:
   - 3×2 and 2×3 matrix manipulations.
   - Exponential and logarithmic operations on 2D arrays.
   - Rounding functions (`np.round()`, `np.floor()`, `np.ceil()`).

4. **Statistics & Sorting**:
   - Summary statistics (`np.sum()`, `np.mean()`, `np.std()`, `np.median()`, `np.var()`).
   - Coordinate extraction with `np.unravel_index(np.argmax(matrix), matrix.shape)`.
   - Row-wise and overall matrix sorting in descending order (`np.sort(matrix, axis=1)[:, ::-1]`).

5. **Visualization**:
   - Generating random floating-point matrices with `np.random.uniform()`.
   - Heatmap visualization using `sns.heatmap(matrix, annot=True, cmap='YlGnBu')`.
