# Lab 06 — One-Sample & Two-Sample t-Test Evaluation

**Course Code:** CSE 413 — Simulation and Modeling Lab  
**Level / Term:** 4/1 | **Credit:** 1.5  
**Course Instructor:** Afroja Ahmed Smrity  
**Student Name:** Azhar  
**Student ID:** 1120  
**Source Task Sheet:** [`T test (7B2).pdf`](T%20test%20%287B2%29.pdf)  
**Notebooks:** [`1120_7B2.ipynb`](1120_7B2.ipynb), [`SIM_Lab6_Azhar_1120.ipynb`](SIM_Lab6_Azhar_1120.ipynb)  

---

## 📌 Short Revision Notes (Lab 6 Key Concepts)

### 1. Conceptual Overview of t-Tests
The $t$-test is an inferential parametric hypothesis test used when:
- Population variance $\sigma^2$ is unknown and estimated using sample variance $s^2$ with Bessel's correction ($ddof = 1$).
- Sample sizes are typically small ($n < 30$), assuming underlying normal distributions.
- Student's $t$-distribution accounts for the additional sampling error in estimating $\sigma$.

---

## 📘 Question 1: One-Sample t-Test (Lab Experiment Completion Time)

### Problem Description
A university claims that the average time students spend completing a laboratory experiment is **45 minutes**. A random sample of 8 students recorded:
$$\text{Data} = [42, 47, 44, 49, 46, 43, 48, 45] \quad (n = 8)$$
Significance level: $\alpha = 0.05$ (two-tailed).

### 1. Hypotheses
- **Null Hypothesis ($H_0$):** $\mu = 45$ (average completion time is 45 minutes)
- **Alternative Hypothesis ($H_1$):** $\mu \neq 45$ (average completion time differs from 45 minutes)

### 2. Formulations & Results
1. **Sample Mean ($\bar{x}$):**
   $$\bar{x} = \frac{\sum x}{n} = \frac{364}{8} = \mathbf{45.5000} \text{ min}$$
2. **Sample Variance ($s^2, ddof = 1$):**
   $$s^2 = \frac{\sum (x_i - \bar{x})^2}{n - 1} = \frac{42}{7} = \mathbf{6.0000}, \quad s = \sqrt{6} \approx \mathbf{2.4495} \text{ min}$$
3. **Standard Error ($SE$):**
   $$SE = \frac{s}{\sqrt{n}} = \frac{\sqrt{6}}{\sqrt{8}} = \sqrt{0.75} \approx \mathbf{0.8660} \text{ min}$$
4. **Degrees of Freedom ($df$):**
   $$df = n - 1 = 8 - 1 = \mathbf{7}$$
5. **$t$-Statistic:**
   $$t = \frac{\bar{x} - \mu_0}{SE} = \frac{45.50 - 45.00}{0.8660} = \mathbf{0.5774}$$
6. **Two-Tailed $p$-Value:**
   $$p = 2 \times [1 - F_{t, 7}(0.5774)] \approx \mathbf{0.5818}$$
7. **Decision:** **Fail to Reject $H_0$** ($p = 0.5818 > \alpha = 0.05$).  
   There is no statistically significant evidence to reject the university's claim that the average completion time is 45 minutes.

---

## 📗 Question 2: Two-Sample Pooled t-Test (Algorithm Comparison)

### Problem Description
Processing times (in ms) of two algorithms:
- **Algorithm A ($n_A = 7$):** $[42, 45, 39, 44, 41, 43, 40]$
- **Algorithm B ($n_B = 7$):** $[48, 51, 46, 49, 50, 47, 52]$
Assumptions: Equal population variances ($\sigma_A^2 = \sigma_B^2$), significance level $\alpha = 0.05$.

### Task-by-Task Solutions

| Task | Description | Formulation / Value |
| :---: | :--- | :--- |
| **Task 1** | **State $H_0$ & $H_1$** | $H_0: \mu_A = \mu_B \ (\mu_A - \mu_B = 0)$<br>$H_1: \mu_A \neq \mu_B \ (\mu_A - \mu_B \neq 0)$ |
| **Task 2** | **Sample Means & Variances** | $\bar{x}_A = \mathbf{42.00} \text{ ms}, \ \bar{x}_B = \mathbf{49.00} \text{ ms}$<br>$s_A^2 = \mathbf{4.6667} \ (s_A = 2.1602), \ s_B^2 = \mathbf{4.6667} \ (s_B = 2.1602)$ |
| **Task 3** | **Mean Difference** | $\Delta \bar{x} = \bar{x}_A - \bar{x}_B = 42.00 - 49.00 = \mathbf{-7.00} \text{ ms}$ |
| **Task 4** | **Pooled Variance & $SE$** | $s_p^2 = \frac{6(4.6667) + 6(4.6667)}{12} = \mathbf{4.6667}$<br>$SE = \sqrt{s_p^2 (1/7 + 1/7)} = \sqrt{1.3333} = \mathbf{1.1547} \text{ ms}$ |
| **Task 5** | **$t$-Statistic & $df$** | $df = 7 + 7 - 2 = \mathbf{12}$<br>$t = \frac{-7.00}{1.1547} = \mathbf{-6.0622}$ (SciPy: $-6.06$) |
| **Task 6** | **Two-Tailed $p$-Value** | $p = 2 \times [1 - F_{t, 12}(|-6.0622|)] = \mathbf{0.000057}$ |
| **Task 7** | **95% Confidence Interval** | $\Delta \bar{x} \pm t_{0.025, 12} \times SE = \mathbf{[-9.52, -4.48]} \text{ ms}$ |
| **Task 8** | **Decision & Interpretation** | Since $p = 0.000057 < 0.05$, **Reject $H_0$**.<br>Algorithm A is significantly faster than Algorithm B (average reduction of 7.00 ms). |

---

### 💻 Verification via SciPy
Both `scipy.stats.ttest_1samp` (for Q1) and `scipy.stats.ttest_ind(..., equal_var=True)` (for Q2) produce results matching manual analytical derivations.
