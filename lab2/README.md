# Simulation Lab - Class Performance 1 (Lab 2)
## Advanced Scalar & Array Operations, Matrix Mathematics, Statistics, and Sorting/Searching in NumPy

---

## 📌 Project Overview

This repository contains the complete solution for **Class Performance 1 (Lab 2)**. The lab focuses on fundamental and advanced numerical computation techniques using Python's **NumPy** library. 

The primary notebook file is **`SIM_CP1_Class_Performance_1.ipynb`** (also saved as `SIM_CP1_YourName_StudentID.ipynb` for submission).

---

## 📁 Repository Structure

```text
lab2/
├── Class Performance 1.pdf        # Original assignment prompt and requirements
├── SIM_CP1_Class_Performance_1.ipynb # Fully executed Jupyter Notebook with outputs
├── SIM_CP1_YourName_StudentID.ipynb # Submission-ready copy of the executed notebook
└── README.md                      # Comprehensive code explanation (this file)
```

---

## 📖 Comprehensive Code & Task Explanation

### Task 1: Advanced Scalar & Array Operations

#### **Goal**
Perform mathematical and trigonometric operations on a 1D array using a scalar value (`scalar = 4.3`).

#### **Code Breakdown & Concepts**

1. **Scalar Broadcasting & 1D Array Definition**:
   ```python
   scalar = 4.3
   arr_1d = np.array([-0.9, -0.4, 0.0, 0.25, 0.6, 0.85, 1.5, 3.2], dtype=np.float64)
   ```
   - **Scalar Broadcasting**: NumPy automatically expands single scalar values to match the shape of arrays during element-wise arithmetic.
   - **Data Types**: `np.float64` ensures double-precision floating-point arithmetic.

2. **Basic Arithmetic Operations**:
   - `arr_1d + scalar` (Addition): Adds $4.3$ to every element.
   - `arr_1d - scalar` (Subtraction): Subtracts $4.3$ from every element.
   - `arr_1d * scalar` (Multiplication): Scales every element by $4.3$.
   - `arr_1d / scalar` (Division): Divides every element by $4.3$.
   - `np.power(np.abs(arr_1d), scalar)` (Power): Computes $|x|^{4.3}$. Taking the absolute value prevents complex numbers when raising negative bases to non-integer powers.

3. **Mathematical Functions**:
   - `np.abs(arr_1d)`: Returns the absolute value $|x|$.
   - `np.sqrt(np.abs(arr_1d))`: Computes $\sqrt{|x|}$. Using `np.abs()` avoids mathematical domain errors (`NaN` for negative inputs).
   - `np.exp(arr_1d)`: Calculates $e^x$ for each element.
   - `np.log(np.abs(arr_1d) + 1e-10)`: Computes the natural logarithm $\ln(|x| + \epsilon)$. The small epsilon ($10^{-10}$) avoids division by zero/log of zero error when $x = 0$.
   - `np.log10(np.abs(arr_1d) + 1e-10)`: Computes base-10 logarithm $\log_{10}(|x| + \epsilon)$.

4. **Trigonometric & Inverse Trigonometric Functions**:
   - `np.sin(arr_1d)`, `np.cos(arr_1d)`, `np.tan(arr_1d)`: Standard trigonometric functions expecting inputs in radians.
   - **Domain Handling with Clipping**:
     Inverse trigonometric functions $\arcsin(x)$ and $\arccos(x)$ are only defined for $x \in [-1, 1]$. Inputs outside this range yield `NaN`.
     ```python
     arr_clipped = np.clip(arr_1d, -1.0, 1.0)
     ```
     - `np.clip(arr_1d, -1.0, 1.0)` clamps any values below $-1.0$ to $-1.0$ and any values above $1.0$ to $1.0$.
     - `np.arcsin(arr_clipped)` and `np.arccos(arr_clipped)` safely compute $\arcsin$ and $\arccos$ without invalid value warnings.
     - `np.arctan(arr_1d)` computes $\arctan(x)$ (valid for all real numbers $(-\infty, \infty)$).

---

### Task 2: Matrix Mathematical Operations

#### **Goal**
Apply multi-dimensional matrix operations on a custom $4 \times 3$ matrix containing positive and negative floating-point numbers.

#### **Code Breakdown & Concepts**

1. **Custom $4 \times 3$ Matrix Creation**:
   ```python
   matrix_4x3 = np.array([
       [-1.25,  0.50,  2.10],
       [-0.75, -2.80,  0.00],
       [ 0.35,  1.20, -0.95],
       [ 3.50, -1.10,  0.80]
   ], dtype=np.float64)
   ```

2. **Trigonometric & Inverse Trigonometric Operations**:
   - `np.sin(matrix_4x3)`, `np.cos(matrix_4x3)`, `np.tan(matrix_4x3)` applied element-wise across the matrix.
   - `matrix_clipped = np.clip(matrix_4x3, -1.0, 1.0)` restricts values to $[-1, 1]$ before executing `np.arcsin(matrix_clipped)` and `np.arccos(matrix_clipped)`.
   - `np.arctan(matrix_4x3)` evaluates inverse tangent across the full matrix.

3. **Exponential & Logarithmic Operations**:
   - `np.exp(matrix_4x3)` computes $e^x$ for each entry.
   - `np.log(np.abs(matrix_4x3) + 1e-10)` and `np.log10(np.abs(matrix_4x3) + 1e-10)` compute natural and base-10 logarithms safely.

4. **Other Mathematical & Rounding Operations**:
   - `np.abs(matrix_4x3)`: Absolute values.
   - `np.sqrt(np.abs(matrix_4x3))`: Square root of absolute values.
   - `np.square(matrix_4x3)`: Element-wise squaring ($x^2$).
   - `np.cbrt(matrix_4x3)`: Cube root ($\sqrt[3]{x}$), which natively handles negative numbers (e.g., $\sqrt[3]{-8} = -2$).
   - `np.fmod(matrix_4x3, 3)`: Floating-point remainder when divided by 3.
   - `np.round(matrix_4x3)`: Rounds elements to the nearest integer.
   - `np.floor(matrix_4x3)`: Rounds down to the largest integer less than or equal to $x$.
   - `np.ceil(matrix_4x3)`: Rounds up to the smallest integer greater than or equal to $x$.

---

### Task 3: Matrix Statistics and Analysis

#### **Goal**
Generate a $3 \times 4$ random matrix using uniform distribution (`np.random.uniform(-10, 10, (3, 4))`) and analyze its global, row-wise, and column-wise statistical properties.

#### **Code Breakdown & Concepts**

1. **Random Matrix Generation**:
   ```python
   np.random.seed(42)  # Seed for reproducible results
   matrix_3x4 = np.random.uniform(-10, 10, (3, 4))
   ```

2. **Global Basic Statistics**:
   - `np.max(matrix_3x4)` & `np.min(matrix_3x4)`: Maximum and minimum values in the matrix.
   - **Argmax & Argmin Indexing**:
     - `argmax_flat = np.argmax(matrix_3x4)` gives the 1D index of the maximum value.
     - `np.unravel_index(argmax_flat, matrix_3x4.shape)` converts the 1D index into a 2D `(row, column)` coordinate pair.
   - `np.sum(matrix_3x4)`: Sum of all 12 elements.
   - `np.prod(matrix_3x4)`: Product of all 12 elements.
   - `np.mean(matrix_3x4)`: Arithmetic average $\mu = \frac{1}{N}\sum x_i$.
   - `np.median(matrix_3x4)`: Middle value when all elements are sorted.
   - `np.var(matrix_3x4)`: Variance $\sigma^2 = \frac{1}{N}\sum (x_i - \mu)^2$.
   - `np.std(matrix_3x4)`: Standard deviation $\sigma = \sqrt{\text{var}}$.

3. **Axis-Based Row & Column Analysis**:
   - **Axis Explanation**: In NumPy, `axis=0` operates vertically across rows (column-wise), while `axis=1` operates horizontally across columns (row-wise).
   - `np.sum(matrix_3x4, axis=1)`: Sum of elements in each row (returns 3 values).
   - `np.sum(matrix_3x4, axis=0)`: Sum of elements in each column (returns 4 values).
   - `np.max(matrix_3x4, axis=1)`: Maximum element in each row.
   - `np.min(matrix_3x4, axis=0)`: Minimum element in each column.

---

### Task 4: Matrix Sorting and Searching Operations

#### **Goal**
Create a $4 \times 4$ integer matrix with random values from $[-20, 20]$ (`np.random.randint(-20, 20, (4, 4))`) and perform advanced sorting, filtering, and element counting.

#### **Code Breakdown & Concepts**

1. **Random Integer Matrix**:
   ```python
   np.random.seed(101)
   matrix_4x4 = np.random.randint(-20, 20, (4, 4))
   ```

2. **Sorting Operations**:
   - **Row-wise Ascending**:
     `np.sort(matrix_4x4, axis=1)` sorts each row independently from lowest to highest.
   - **Row-wise Descending**:
     `np.sort(matrix_4x4, axis=1)[:, ::-1]` sorts each row in ascending order and then reverses column order using Python slicing `::-1`.
   - **Matrix-wide Ascending**:
     ```python
     flat_asc = np.sort(matrix_4x4.flatten())
     matrix_asc = flat_asc.reshape(4, 4)
     ```
     `matrix.flatten()` collapses the 2D matrix into a 1D array, sorts all 16 elements, and `.reshape(4, 4)` restores it to a $4 \times 4$ grid.
   - **Matrix-wide Descending**:
     Reverses the sorted 1D array (`flat_asc[::-1]`) and reshapes it to $4 \times 4$.

3. **Searching & Element Extraction**:
   - **Five Largest Values**: `np.sort(matrix_4x4.flatten())[-5:][::-1]` extracts the last 5 elements of the sorted array and orders them descending.
   - **Five Smallest Values**: `np.sort(matrix_4x4.flatten())[:5]` extracts the first 5 elements.
   - **Positions Greater Than Matrix Mean**:
     ```python
     mat_mean = matrix_4x4.mean()
     pos_gt_mean = np.argwhere(matrix_4x4 > mat_mean)
     ```
     `matrix_4x4 > mat_mean` creates a boolean mask (`True`/`False`). `np.argwhere()` returns the $(row, col)$ coordinates where the condition is `True`.
   - **Element Counts via Boolean Masking**:
     - `np.sum(matrix_4x4 > 0)`: Counts positive numbers.
     - `np.sum(matrix_4x4 < 0)`: Counts negative numbers.
     - `np.sum(matrix_4x4 == 0)`: Counts zeros.

---

## 🚀 How to Run the Notebook

1. **Open Terminal** in your project directory (`lab2`).
2. Launch Jupyter Lab or Notebook:
   ```bash
   jupyter notebook SIM_CP1_Class_Performance_1.ipynb
   ```
3. To re-run all cells:
   Go to the top menu bar in Jupyter: **Kernel** $\rightarrow$ **Restart & Run All**.

---

## ✅ Submission Checklist Verification

- [x] All code cells run cleanly without warnings or errors.
- [x] Clear text and numerical outputs for all operations.
- [x] Mathematical domain edge-cases (negative roots, zero logs, inverse trig limits) safely handled.
- [x] Clear markdown sections and informative code comments.
- [x] Follows the required file naming convention (`SIM_CP1_YourName_StudentID.ipynb`).
