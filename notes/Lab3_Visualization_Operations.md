# Revision Notes — Lab 3: Matrix Operations & Data Visualizations

**Course Code:** CSE 413 | **Credit:** 1.5  
**Instructor:** Afroja Ahmed Smrity  

---

## 🔑 Key Mathematical & Computational Concepts

### 1. Vector Comparison Line Plots (`plt.plot`)
- Plotting two equal-length random vectors on the same axes to compare values:
  ```python
  v1 = np.random.rand(15)
  v2 = np.random.rand(15)
  plt.plot(range(1, 16), v1, marker='o', label='Vector 1')
  plt.plot(range(1, 16), v2, marker='s', label='Vector 2')
  ```

### 2. Matrix Arithmetic Operations
- **Matrix Addition**: $C = A + B$ (requires identical dimensions).
- **Matrix Subtraction**: $D = A - B$ (requires identical dimensions).
- **Matrix Multiplication**: $E = A \cdot B$ (`np.dot(A, B)` or `A @ B`). Requires columns of $A$ to equal rows of $B$.

### 3. Element-wise Subplot Bar Charts
- Visualizing every element of a $4 \times 4$ result matrix (16 bars total):
  ```python
  fig, axes = plt.subplots(1, 3, figsize=(18, 4.5))
  axes[0].bar(range(1, 17), add_res.flatten(), color='royalblue')
  axes[1].bar(range(1, 17), sub_res.flatten(), color='seagreen')
  axes[2].bar(range(1, 17), mult_res.flatten(), color='crimson')
  ```

### 4. Seaborn Heatmaps (`sns.heatmap`)
- 2D matrix magnitude visualization:
  ```python
  sns.heatmap(matrix, annot=True, cmap='coolwarm', linewidths=0.5, linecolor='black')
  ```
