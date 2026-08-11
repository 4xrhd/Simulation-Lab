# Class Performance 02 — Matrix Operations & Vector Visualization

**Course Code:** CSE 413 | **Credit:** 1.5  
**Instructor:** Afroja Ahmed Smrity  
**Notebook:** [`Student_CP2_Azhar_1120.ipynb`](file:///home/tr/Desktop/LAB-uni/simulation-lab/lab3/Student_CP2_Azhar_1120.ipynb)  
**Task Specification PDF:** [`CP2 7B2.pdf`](file:///home/tr/Desktop/LAB-uni/simulation-lab/lab3/CP2%207B2.pdf)  

---

## 📌 Tasks Completed (`CP2 7B2.pdf`)

### 1. Task 1: Generate and Plot Two Random Vectors
- **Vector Generation**: Generated two 15-element vectors (`v1`, `v2`) containing random floats using `np.random.rand(15)`.
- **Matplotlib Line Graph (`plt.plot`)**:
  - Plotted both vectors on the same line graph using markers (`o`, `--s`).
  - Added plot title `Comparison of Two 15-Element Random Vectors`.
  - Formatted x-axis (`Vector Element Index (1 to 15)`) and y-axis (`Float Value`).
  - Added legend and grid for comparative clarity.

---

### 2. Task 2: Matrix Operations and Bar Plot Visualization (4×4 Matrices)
- **4×4 Random Matrices**: Created two $4 \times 4$ matrices $A$ and $B$ containing random integer values.
- **Matrix Operations**:
  - **Addition ($A + B$)**: Element-wise matrix sum.
  - **Subtraction ($A - B$)**: Element-wise matrix difference.
  - **Multiplication ($A \cdot B$)**: Compatible $4 \times 4$ dot product matrix multiplication using `np.dot(A, B)`.
- **Bar Plot Visualizations (`plt.subplots`, `axes[i].bar`)**:
  - Flattened each $4 \times 4$ result matrix into 16 individual elements (`range(1, 17)`).
  - Plotted $1 \times 3$ subplots of bar charts where **each bar represents one element of the 4×4 matrix**.
