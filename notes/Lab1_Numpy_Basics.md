# Revision Notes — Lab 1: NumPy Basics & Matrix Operations

**Course Code:** CSE 413 | **Credit:** 1.5  
**Instructor:** Afroja Ahmed Smrity  

---

## 🔑 Key Mathematical & Computational Concepts

### 1. Scalar Operations & Broadcasting
- Scalar broadcasting applies single numerical values across entire arrays element-wise without manual loops.
- **Data Precision**: Specify `dtype=np.float64` for double-precision calculations.

### 2. Domain Safety & Input Clipping (`np.clip`)
- Functions like `np.arcsin(x)` and `np.arccos(x)` require inputs in $[-1, 1]$.
- Out-of-bounds inputs produce domain errors or `NaN`.
- **Solution**: Clip inputs before computing inverse trigonometric values:
  ```python
  arr_clipped = np.clip(matrix / np.max(matrix), -1, 1)
  asin_vals = np.arcsin(arr_clipped)
  ```

### 3. Logarithmic & Square Root Safeguards
- `np.sqrt(x)` requires non-negative values ($x \geq 0$). Use `np.abs(x)` to safeguard.
- `np.log(x)` requires positive values ($x > 0$). Add a small offset $\epsilon = 10^{-10}$ to prevent division by zero or log of zero:
  ```python
  log_vals = np.log(np.abs(arr) + 1e-10)
  ```

### 4. Index Extraction & Matrix Coordinates
- `np.argmax(matrix)` and `np.argmin(matrix)` return flat indices.
- Convert flat indices to 2D coordinates `(row, col)` using `np.unravel_index`:
  ```python
  row, col = np.unravel_index(np.argmax(matrix), matrix.shape)
  ```

### 5. Descending Sorting
- Row-wise descending sort:
  ```python
  row_sorted_desc = np.sort(matrix, axis=1)[:, ::-1]
  ```
- Overall matrix descending sort:
  ```python
  overall_sorted_desc = np.sort(matrix.flatten())[::-1]
  ```
