# Lab Performance 03 — Two-Sample t-Test Hypothesis Testing

**Course Code:** CSE 413 — Simulation and Modeling Lab  
**Level / Term:** 4/1 | **Credit:** 1.5  
**Course Instructor:** Afroja Ahmed Smrity  
**Student Name:** Azhar  
**Student ID:** 1120  
**Notebook:** [`SIM_Lab3_Azhar_1120.ipynb`](SIM_Lab3_Azhar_1120.ipynb)  

---

## 📌 Short Revision Notes (Lab 3 Key Concepts)

### 1. Conceptual Overview of Two-Sample t-Test
The **independent two-sample $t$-test** (Student's $t$-test) is an inferential statistical test used to evaluate whether the true population means of two independent groups differ significantly.
- **Key Assumptions**:
  1. Continuous, interval, or ratio-level scale.
  2. Independent observations (random sampling without mutual influence).
  3. Approximate normal distribution within each group.
  4. Homogeneity of variances ($\sigma_1^2 = \sigma_2^2$), justifying the pooled variance estimation.

---

### 2. Hypothesis Formulation
- **Null Hypothesis ($H_0$):**
  $$H_0: \mu_1 = \mu_2 \quad \Longleftrightarrow \quad \mu_1 - \mu_2 = 0$$
  *There is no statistically significant difference between the true population means of Data 1 and Data 2.*
- **Alternative Hypothesis ($H_1$):**
  $$H_1: \mu_1 \neq \mu_2 \quad \Longleftrightarrow \quad \mu_1 - \mu_2 \neq 0$$
  *There is a statistically significant difference between the true population means of Data 1 and Data 2.*
- **Significance Level ($\alpha$):** Set to $\alpha = 0.05$ (two-tailed).

---

### 3. Mathematical Formulations & Derivations

#### A. Sample Mean & Unbiased Sample Variance (ddof = 1)
For each sample group $i \in \{1, 2\}$ with size $n_i$:
$$\bar{x}_i = \frac{1}{n_i} \sum_{j=1}^{n_i} x_{ij}$$
$$s_i^2 = \frac{1}{n_i - 1} \sum_{j=1}^{n_i} (x_{ij} - \bar{x}_i)^2$$
> **Delta Degrees of Freedom (`ddof = 1`)**: In NumPy, `np.var(..., ddof=1)` and `np.std(..., ddof=1)` apply Bessel's correction to remove sample variance bias when estimating the unknown population variance.

#### B. Degrees of Freedom ($df$)
$$df = n_1 + n_2 - 2$$
For $n_1 = 5, n_2 = 5$:
$$df = 5 + 5 - 2 = 8$$

#### C. Pooled Variance ($s_p^2$)
When equal variances are assumed ($\sigma_1^2 = \sigma_2^2 = \sigma^2$), the pooled sample variance is a weighted average of sample variances:
$$s_p^2 = \frac{(n_1 - 1)s_1^2 + (n_2 - 1)s_2^2}{n_1 + n_2 - 2}$$
$$s_p = \sqrt{s_p^2}$$

#### D. Standard Error of the Mean Difference ($SE$)
$$SE = \sqrt{s_p^2 \left( \frac{1}{n_1} + \frac{1}{n_2} \right)} = s_p \sqrt{\frac{1}{n_1} + \frac{1}{n_2}}$$

#### E. Two-Sample $t$-Statistic
$$t = \frac{(\bar{x}_1 - \bar{x}_2) - (\mu_1 - \mu_2)_0}{SE} = \frac{\bar{x}_1 - \bar{x}_2}{SE}$$

#### F. Two-Tailed $p$-Value
$$p\text{-value} = 2 \times \left[1 - F_{t, df}(|t|)\right]$$
Where $F_{t, df}$ is the cumulative distribution function (CDF) of the Student's $t$-distribution with $df$ degrees of freedom.

---

### 4. 95% Confidence Interval for the Difference of Means
The $(1 - \alpha) \times 100\%$ confidence interval for the true population mean difference $(\mu_1 - \mu_2)$ is:
$$\text{CI} = (\bar{x}_1 - \bar{x}_2) \pm t_{\alpha/2, \, df} \times SE$$
Where $t_{0.025, 8} \approx 2.3060$ is the two-tailed critical value.
- **Duality Property**: If the $95\%$ confidence interval does **not** contain $0$, the null hypothesis $H_0: \mu_1 - \mu_2 = 0$ is rejected at $\alpha = 0.05$.

---

### 5. Evaluation Data & Numerical Results Summary

| Parameter / Metric | Symbol / Formula | Computed Value |
| :--- | :--- | :--- |
| **Data 1 Observations** | $x_1$ | `[18.4, 19.1, 17.9, 18.7, 18.3]` |
| **Data 2 Observations** | $x_2$ | `[20.2, 20.5, 20.1, 20.3, 20.4]` |
| **Sample Sizes** | $n_1, n_2$ | $5, 5$ |
| **Sample Mean 1** | $\bar{x}_1$ | **18.4800** |
| **Sample Mean 2** | $\bar{x}_2$ | **20.3000** |
| **Mean Difference** | $\bar{x}_1 - \bar{x}_2$ | **-1.8200** |
| **Sample Variance 1 (ddof=1)** | $s_1^2$ | **0.2020** |
| **Sample Variance 2 (ddof=1)** | $s_2^2$ | **0.0250** |
| **Sample Standard Deviation 1** | $s_1$ | **0.4494** |
| **Sample Standard Deviation 2** | $s_2$ | **0.1581** |
| **Degrees of Freedom** | $df = n_1 + n_2 - 2$ | **8** |
| **Pooled Variance** | $s_p^2$ | **0.1135** |
| **Pooled Standard Deviation** | $s_p$ | **0.3369** |
| **Standard Error** | $SE$ | **0.2131** |
| **Two-Sample $t$-Statistic** | $t$ | **-8.5417** |
| **Critical $t$-Value ($\alpha=0.05$)** | $\pm t_{0.025, 8}$ | **±2.3060** |
| **Two-Tailed $p$-Value** | $p$ | **0.000027** ($2.69 \times 10^{-5}$) |
| **95% Confidence Interval** | $(\bar{x}_1 - \bar{x}_2) \pm t_{crit} \cdot SE$ | **[-2.3113, -1.3287]** |
| **Statistical Decision** | Reject $H_0$ if $p < 0.05$ | **Reject the Null Hypothesis ($H_0$)** |

---

### 6. Decision & Plain-English Interpretation
1. **Statistical Rejection**:
   Since the computed $p$-value ($0.000027$) is strictly less than $\alpha = 0.05$, and $|t| = 8.5417$ exceeds the critical threshold $t_{\text{crit}} = 2.3060$, we reject the null hypothesis $H_0$.
2. **Substantive Conclusion**:
   There is strong, statistically significant evidence that the true population means of Data 1 and Data 2 are different. Data 2 has a significantly higher average value ($\bar{x}_2 = 20.30$) than Data 1 ($\bar{x}_1 = 18.48$), with an estimated difference of approximately $1.82$ units ($95\%\text{ CI: } [-2.31, -1.33]$).

---

### 7. Python Implementation Comparison

```python
import numpy as np
import scipy.stats as stats

# Data definition
data1 = np.array([18.4, 19.1, 17.9, 18.7, 18.3])
data2 = np.array([20.2, 20.5, 20.1, 20.3, 20.4])

# 1. SciPy Built-in Function
t_stat, p_val = stats.ttest_ind(data1, data2, equal_var=True)

# 2. Analytical Formulation
mean_diff = np.mean(data1) - np.mean(data2)
n1, n2 = len(data1), len(data2)
sp_sq = ((n1 - 1) * np.var(data1, ddof=1) + (n2 - 1) * np.var(data2, ddof=1)) / (n1 + n2 - 2)
std_err = np.sqrt(sp_sq * (1/n1 + 1/n2))
t_manual = mean_diff / std_err
p_manual = 2 * (1 - stats.t.cdf(abs(t_manual), df=n1 + n2 - 2))

# 3. 95% Confidence Interval
ci = stats.t.interval(0.95, df=n1 + n2 - 2, loc=mean_diff, scale=std_err)
```
Both manual analytical formulation and SciPy library methods produce identical numerical values ($t = -8.5417, p = 0.000027, \text{CI} = [-2.3113, -1.3287]$).
