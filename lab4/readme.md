# Lab 04 — Probability Distributions, Random Variates & Simulation Sampling

**Course Code:** CSE 413 | **Course Title:** Simulation and Modeling Lab  
**Academic Level/Term:** 4/1 | **Credit:** 1.5  
**Course Instructor:** Afroja Ahmed Smrity  

---

## 📌 Overview & Objectives

In stochastic simulation and computational modeling, generating and analyzing random variates from specific theoretical distributions is fundamental for modeling physical processes, queuing networks, and uncertain systems. Lab 04 covers:
1. **Uniform Probability Distribution**: Generating pseudo-random numbers in $U[0, 1)$, understanding binning, and comparing raw frequency vs. normalized probability density.
2. **Normal (Gaussian) Distribution**: Simulating standard normal $\mathcal{N}(0, 1)$ and parameterized $\mathcal{N}(\mu, \sigma^2)$ variates, computing empirical sample statistics ($\bar{x}, s$), and verifying the bell curve.
3. **Random Permutations**: Shuffling sequences and generating randomized discrete indexing without replacement.
4. **RNG Seed & Reproducibility**: Demonstrating deterministic sequence regeneration via `np.random.seed()` vs. unseeded pseudorandom stochasticity.
5. **Sample Size Impact**: Exploring how small samples ($N=10$) exhibit high sampling variance whereas large samples ($N=100,000$) converge to theoretical densities by the Law of Large Numbers.

#### 🇧🇩 সহজ বাংলায় ল্যাব উদ্দেশ্য (Overview & Objectives in Bengali):
> **সিমুলেশন ও মডেলিং ল্যাব ০৪-এর মূল উদ্দেশ্য:**  
> স্টোকাস্টিক (দৈব বা অনির্ধারিত) সিমুলেশনে বাস্তব জীবনের বিভিন্ন সিস্টেম (যেমন: কিউয়িং সিস্টেম, ট্রাফিক নেটওয়ার্ক, পরিমাপের অনিশ্চয়তা) মডেল করার জন্য নির্দিষ্ট সম্ভাব্যতা বিন্যাস (Probability Distribution) অনুযায়ী দৈব সংখ্যা (Random Variates) তৈরি ও বিশ্লেষণ করা সবচেয়ে মৌলিক ধাপ। এই ল্যাব থেকে আমরা যা যা শিখব:
> 1. **সুষম বিন্যাস (Uniform Distribution, $U[0, 1)$):** $[0, 1)$ সীমার মধ্যে সমান সম্ভাবনাবিশিষ্ট দৈব সংখ্যা তৈরি করা এবং সাধারণ ফ্রিকোয়েন্সি বনাম নরম্যালাইজড ডেনসিটি হিস্টোগ্রামের পার্থক্য নির্ণয় করা।
> 2. **স্বাভাবিক বিন্যাস (Normal / Gaussian Distribution, $\mathcal{N}(\mu, \sigma^2)$):** প্রতিসম ঘণ্টাকৃতির স্ট্যান্ডার্ড নরমাল ($Z \sim \mathcal{N}(0, 1)$) এবং প্যারামিটারাইজড নরমাল ডাটা তৈরি করা, এম্পিরিক্যাল রুল ($68-95-99.7\%$) যাচাই এবং এদের গড় ($\bar{x}$) ও পরিমিত ব্যবধান ($s$) পরিমাপ করা।
> 3. **দৈব পুনর্বিন্যাস (Random Permutation):** কোনো ক্রম বা তালিকাকে প্রতিস্থাপন ছাড়া (without replacement) এলোমেলোভাবে পুনর্বিন্যাস বা শাফল (Shuffle) করা।
> 4. **সিড নিয়ন্ত্রণ ও ফলাফল পুনরাবৃত্তি (PRNG Seed Control):** `np.random.seed()` ব্যবহারের মাধ্যমে সিউডো-র‍্যান্ডম জেনারেটরের মান অপরিবর্তিত রাখা, যা ডিবাগিং এবং সিমুলেশনের ফলাফল হুবহু প্রমাণ করার (Reproducibility) জন্য অপরিহার্য।
> 5. **নমুনার আকারের প্রভাব (Law of Large Numbers):** ছোট নমুনায় ($N=10$) দৈব ত্রুটি বেশি থাকে, কিন্তু নমুনার সংখ্যা অনেক বাড়ালে ($N=100,000$) তা কীভাবে তাত্ত্বিক ফর্মুলার সাথে নিখুঁতভাবে মিলে যায় তা পর্যবেক্ষণ করা।

---

## 🔑 Key Mathematical & Computational Concepts

### 1. Continuous Uniform Distribution $U(a, b)$
A continuous random variable $X$ is uniformly distributed over $[a, b]$ if all sub-intervals of equal length are equally likely.

- **Probability Density Function (PDF)**:
  $$f(x) = \begin{cases} \frac{1}{b - a}, & a \le x \le b \\ 0, & \text{otherwise} \end{cases}$$
- **Expected Value (Mean)**: $\mathbb{E}[X] = \mu = \frac{a + b}{2}$
- **Variance**: $\text{Var}(X) = \sigma^2 = \frac{(b - a)^2}{12}$
- **Standard Deviation**: $\sigma = \frac{b - a}{\sqrt{12}}$
- **Standard Uniform $U[0, 1)$**: $\mu = 0.5$, $\sigma^2 = \frac{1}{12} \approx 0.0833$, $\sigma \approx 0.2887$.

#### NumPy Implementation
```python
# Generate N uniformly distributed numbers in [0, 1)
N = 100000
uniform_variates = np.random.rand(N)

# Theoretical properties for U(0, 1):
# Mean = 0.5, Variance = 1/12 ≈ 0.0833, Std = 1/sqrt(12) ≈ 0.2887
print(f"Sample Mean: {np.mean(uniform_variates):.4f}")
print(f"Sample Var:  {np.var(uniform_variates):.4f}")
```

---

### 2. Frequency Histogram vs. Normalized Probability Density
When plotting empirical histograms using `matplotlib.pyplot.hist`:

| Parameter | Configuration | Y-Axis Meaning | Total Area under Curve |
| :--- | :--- | :--- | :--- |
| **Raw Frequency** | `density=False` (default) | Count of observations falling in each bin ($n_i$) | Total Sample Size $N = \sum \text{counts}$ |
| **Normalized Density** | `density=True` | Probability Density: $f(x) = \frac{\text{count}}{N \times \Delta x}$ | Total Area $= \int_{-\infty}^{\infty} f(x)dx = 1.0$ |

```python
# Raw count histogram
plt.hist(random_numbers, bins=50, alpha=0.75, color='royalblue', edgecolor='white')
plt.ylabel('Frequency (Count)')

# Normalized probability density histogram
plt.hist(random_numbers, bins=50, density=True, alpha=0.6, color='seagreen', edgecolor='black')
plt.ylabel('Probability Density')
```

---

### 3. Normal (Gaussian) Distribution $\mathcal{N}(\mu, \sigma^2)$
The Normal distribution is continuous, symmetric, and characterized by its mean $\mu$ and standard deviation $\sigma$.

- **Probability Density Function (PDF)**:
  $$f(x) = \frac{1}{\sigma \sqrt{2\pi}} \exp\left( -\frac{(x - \mu)^2}{2\sigma^2} \right)$$
- **Standard Normal Distribution $Z \sim \mathcal{N}(0, 1)$**:
  $$f(z) = \frac{1}{\sqrt{2\pi}} e^{-\frac{z^2}{2}}, \quad \mu = 0, \; \sigma = 1$$
- **Empirical Rule ($68-95-99.7\%$ Rule)**:
  - $\approx 68.27\%$ of values fall within $[\mu - \sigma, \mu + \sigma]$.
  - $\approx 95.45\%$ of values fall within $[\mu - 2\sigma, \mu + 2\sigma]$.
  - $\approx 99.73\%$ of values fall within $[\mu - 3\sigma, \mu + 3\sigma]$.

#### 🇧🇩 সহজ বাংলায় ব্যাখ্যা (Concept Note in Bengali):
> **Normal Distribution (বা Gaussian Distribution - স্বাভাবিক বা গাউসীয় বিন্যাস):**  
> এটি একটি অবিচ্ছিন্ন (continuous), প্রতিসম (symmetrical) এবং ঘণ্টাকৃতির (bell-shaped) সম্ভাব্যতা বিন্যাস। এর প্রধান বৈশিষ্ট্যগুলো হলো:
> 1. **গড়ের (Mean) চারপাশে ঘন সমাবেশ:** বেশিরভাগ ডাটা পয়েন্ট বা মানের উপস্থিতি থাকে একদম কেন্দ্রে অর্থাৎ গড়ের (Mean, $\mu$) কাছাকাছি।
> 2. **মসৃণভাবে মান হ্রাস পাওয়া:** গড় থেকে আপনি যত দূরে (বামে বা ডানে) যাবেন, ডাটা পাওয়ার সম্ভাবনা (probability) তত মসৃণ ও অবিচ্ছিন্নভাবে কমতে থাকবে।
> 3. **প্রতিসম বা Mirror Image কার্ভ:** কার্ভটির ঠিক মাঝখানের লম্ব রেখা বরাবর ভাঁজ করলে বাম পাশ ও ডান পাশ একে অপরের নিখুঁত দর্পণ প্রতিবিম্ব (mirror image) হয়। অর্থাৎ, $Mean = Median = Mode$।
> 
> **সহজ কথায়:** নরমাল ডিস্ট্রিবিউশন দেখতে একটি ঘণ্টার (Bell) মতো—যেখানে অধিকাংশ মানুষের মান থাকে মাঝের বা গড় মানের কাছাকাছি এবং খুব কম মানুষের মান থাকে অতি কম বা অতি বেশি।
> - **বাস্তব জীবনের উদাহরণ:** মানুষের উচ্চতা (বেশিরভাগ মানুষ গড় উচ্চতার হয়, খুব খাটো বা খুব লম্বা মানুষ কম), পরীক্ষার নম্বর (অধিকাংশ ছাত্রছাত্রী গড় নম্বর পায়, খুব বেশি বা খুব কম নম্বর পাওয়া শিক্ষার্থীর সংখ্যা কম), এবং বৈজ্ঞানিক পরিমাপের ত্রুটি (Measurement Errors)।

#### NumPy Implementation
```python
# Standard Normal N(0, 1) using randn
z_scores = np.random.randn(10000)

# General Normal N(mu, sigma^2) using normal(loc, scale, size)
mu, sigma, size = 100, 10, 10000
normal_data = np.random.normal(loc=mu, scale=sigma, size=size)

# Sample statistics verification
sample_mean = np.mean(normal_data)  # ≈ 100
sample_std = np.std(normal_data)    # ≈ 10
```

---

### 4. Random Permutation & Shuffling
Permutation reorders an array or integer sequence without replacement, critical for Monte Carlo shuffling, randomized trials, and bootstrapping.

```python
# Permute integers 0 to 9
perm_10 = np.random.permutation(10)

# Permute a custom range [1, 10]
perm_1_to_10 = np.random.permutation(np.arange(1, 11))
```

---

### 5. Pseudo-Random Number Generation (PRNG) & Seed Reproducibility
Computers generate *pseudo-random* numbers via deterministic mathematical algorithms (e.g., Mersenne Twister). 

- **Seed**: Initializes the internal PRNG state.
- **With Fixed Seed (`np.random.seed(S)`)**: The sequence of generated numbers is identical across runs. Essential for debugging, reproducible research, and simulation verification.
- **Without Fixed Seed (`np.random.seed(None)` / default)**: PRNG is initialized from OS entropy (e.g., system clock/`/dev/urandom`), producing different outputs each run.

```python
# Fixed Seed Run
np.random.seed(10)
matrix_a = np.random.randint(1, 51, (3, 3))

np.random.seed(10)
matrix_b = np.random.randint(1, 51, (3, 3))
# matrix_a == matrix_b is True for all elements (Exact Match)

# Unseeded Run
np.random.seed(None)
matrix_c = np.random.randint(1, 51, (3, 3))
# matrix_c generates a different stochastic instance
```

---

## 🧪 Student Exercises & Analysis

### Exercise 1: Small vs. Large Sample Uniform Distribution
1. **Generation**: Created a $1 \times 10$ vector using `np.random.rand(10)`.
2. **Observation**: A 10-sample histogram does not appear flat because small sample sizes are dominated by empirical sampling noise. As sample size $N \to \infty$ ($N = 100,000$), the histogram approaches the theoretical uniform line $f(x) = 1.0$.

### Exercise 2: Standard Normal Simulation ($N = 500$)
1. **Generation**: Generated 500 samples using `np.random.normal(0, 1, 500)`.
2. **Observation**: Histogram exhibits a distinct bell shape centered around $\mu \approx 0$ with sample standard deviation $s \approx 1$.

### Exercise 3: Seed Impact on 3×3 Integer Matrices
1. **Generation**: Generated $3 \times 3$ matrices with random integers in $[1, 50]$.
2. **Comparison**:
   - With `np.random.seed(10)`: Both executions generate identical $3 \times 3$ matrices.
   - Without seed: Each execution produces unique random integers.

---

## 📊 Summary of Functions Covered

| Function | Library | Purpose | Key Parameters |
| :--- | :--- | :--- | :--- |
| `np.random.rand(*d)` | `numpy.random` | Uniform variates in $[0, 1)$ | Dimension shapes (e.g. `10`, `(3, 3)`) |
| `np.random.randn(*d)` | `numpy.random` | Standard normal variates $\mathcal{N}(0, 1)$ | Dimension shapes |
| `np.random.normal(loc, scale, size)` | `numpy.random` | General normal variates $\mathcal{N}(\mu, \sigma^2)$ | `loc` ($\mu$), `scale` ($\sigma$), `size` |
| `np.random.randint(low, high, size)` | `numpy.random` | Discrete uniform integers in $[\text{low}, \text{high})$ | `low`, `high`, `size` |
| `np.random.permutation(x)` | `numpy.random` | Randomly permute a sequence / range | Integer $n$ or array-like object |
| `np.random.seed(s)` | `numpy.random` | Set the seed for PRNG reproducibility | Integer seed value or `None` |
| `plt.hist(x, bins, density)` | `matplotlib.pyplot` | Plot empirical distribution histogram | `bins`, `density=True/False`, `alpha`, `edgecolor` |
