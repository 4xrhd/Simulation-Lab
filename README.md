# Simulation and Modeling Lab (CSE 413)

![Simulation and Modeling Lab Dashboard](preview.png)

## 📌 Course Metadata
- **Course Code:** CSE 413
- **Course Title:** Simulation and Modeling Lab
- **Level/Term:** 4/1
- **Credit:** 3
- **Instructor:** Afroja Ahmed Smrity
- **Department:** Computer Science and Engineering (CSE)

---

## 🎯 About This Repository
This repository contains the practical lab submissions, performance evaluations, mathematical simulations, and Jupyter Notebooks for the **CSE 413: Simulation and Modeling Lab** course.

The course covers computer-based modeling and numerical simulation techniques using Python (`NumPy`, `SciPy`, `Matplotlib`, `Seaborn`, and `SymPy`), including matrix operations, random number generation, hypothesis testing, Kolmogorov-Smirnov tests, Monte Carlo simulations, and queuing models.

---

## 📁 Repository Directory Structure

```
simulation-lab/
│
├── preview.png                        # Repository banner / dashboard preview
├── README.md                          # Main repository overview & documentation
├── FOLDERS.md                         # Detailed class directory index & module log
├── .gitignore                         # Build and environment exclusions
│
├── lab1/                              # Lab Day 1 Materials & Submissions
│   ├── SIM_Lab_Day 1.ipynb            # Class reference notebook
│   └── SIM_Lab1_Azhar_1120.ipynb      # Completed Day 1 notebook submission
│
├── Lab-performances/                  # Lab Performance Evaluations
│   └── Lab-performance-01/            # Performance Evaluation 01
│       ├── SIM_Lab1_Azhar_1120.ipynb  # Executed lab assignment notebook
│       └── readme.md                  # Lab 1 revision notes & mathematical concepts
│
├── Course-docs/                       # Official syllabus & course outline
│   └── CSE 413 Simulation_and_Modeling_Lab_Course_Outline_7A_updated_COs.pdf
│
└── notes/                             # Lecture and study notes
```

---

## 📚 Completed Lab Modules

| Module / Lab Day | Directory Path | Key Topics & Operations | Status |
| :--- | :--- | :--- | :---: |
| **Lab Day 01** | [`lab1/`](lab1/) | Scalar-array broadcasting, 3×2 & 2×3 matrix operations, domain clipping (`np.clip`), descending sorting, summary statistics, Seaborn heatmaps. ([Revision Notes](Lab-performances/Lab-performance-01/readme.md)) | ✅ Completed |
| **Lab Performance 01** | [`Lab-performances/Lab-performance-01/`](Lab-performances/Lab-performance-01/) | Performance assignment submission & execution verification. | ✅ Completed |

---

## 💻 Tech Stack & Libraries
- **Language:** Python 3.11+
- **Numerical Computing:** NumPy, SymPy
- **Data Visualization:** Matplotlib, Seaborn
- **Environment:** Jupyter Notebooks (`.ipynb`)

---

## 🚀 How to Run the Notebooks Locally

1. **Clone the repository**:
   ```bash
   git clone https://github.com/4xrhd/Simulation-Lab.git
   cd Simulation-Lab
   ```

2. **Set up virtual environment (optional but recommended)**:
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

3. **Install required dependencies**:
   ```bash
   pip install numpy matplotlib seaborn sympy notebook
   ```

4. **Launch Jupyter Notebook**:
   ```bash
   jupyter notebook
   ```
