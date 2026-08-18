# Revision Notes — Lab 4: Probability Distributions & Random Variate Generation

**Course Code:** CSE 413 | **Credit:** 1.5  
**Instructor:** Afroja Ahmed Smrity  

---

## 📌 Overview & Lab Objectives

In stochastic simulation and modeling, generating random variates from specific theoretical probability distributions forms the core of modeling physical systems, queuing networks, and computational experiments.

### 🇧🇩 সহজ বাংলায় ল্যাব উদ্দেশ্য (Overview & Objectives in Bengali):
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
- **Definition**: Every outcome in the interval $[a, b]$ has equal probability.
- **Probability Density Function (PDF)**:
  $$f(x) = \frac{1}{b - a}, \quad a \le x \le b$$
- **Moments**:
  $$\mathbb{E}[X] = \frac{a + b}{2}, \quad \text{Var}(X) = \frac{(b - a)^2}{12}$$
- **NumPy Syntax**:
  ```python
  u_samples = np.random.rand(100000)  # Generates numbers in [0, 1)
  ```

---

### 2. Frequency vs. Probability Density Histograms
- **Raw Frequency (`density=False`)**: Bin heights represent raw sample counts ($y = \text{count}$).
- **Normalized Probability Density (`density=True`)**: Bin heights represent probability density such that the total area under the histogram equals $1.0$:
  $$\text{Area} = \sum_{i} (\text{height}_i \times \text{width}_i) = 1.0$$
- **NumPy / Matplotlib Syntax**:
  ```python
  plt.hist(u_samples, bins=50, density=True, alpha=0.6, color='blue', edgecolor='black')
  ```

---

### 3. Normal (Gaussian) Distribution $\mathcal{N}(\mu, \sigma^2)$
- **Definition**: Symmetric, continuous bell-shaped distribution governed by central limit tendencies.
- **Probability Density Function (PDF)**:
  $$f(x) = \frac{1}{\sigma \sqrt{2\pi}} e^{-\frac{(x - \mu)^2}{2\sigma^2}}$$
- **Standard Normal Distribution**:
  $$Z \sim \mathcal{N}(0, 1) \implies \mu = 0, \; \sigma = 1$$
- **Empirical Rule ($68-95-99.7\%$)**:
  - $\approx 68.3\%$ of data within $[\mu - \sigma, \mu + \sigma]$
  - $\approx 95.5\%$ of data within $[\mu - 2\sigma, \mu + 2\sigma]$
  - $\approx 99.7\%$ of data within $[\mu - 3\sigma, \mu + 3\sigma]$

#### 🇧🇩 সহজ বাংলায় ব্যাখ্যা (Bengali Revision Summary):
> **Normal Distribution (স্বাভাবিক বা গাউসীয় বিন্যাস):**  
> একটি সিমেট্রিক্যাল (প্রতিসম) এবং বেল-শেপড (ঘণ্টাকৃতির) সম্ভাব্যতা বিন্যাস।  
> 
> 1. **গড় বা Mean-এ ক্লাস্টার:** বেশিরভাগ ডাটা পয়েন্ট গড়ের (Mean $\mu$) কাছাকাছি অবস্থান করে।
> 2. **মসৃণভাবে হ্রাস (Smooth Decrease):** গড় মান থেকে আপনি যত বামে বা ডানে যাবেন, ডাটা পাওয়ার সম্ভাবনা একটি স্মুথ বা মসৃণ কার্ভের মতো কমতে থাকবে।
> 3. **সিমেট্রিক্যাল বা দর্পণ প্রতিবিম্ব (Mirror Image):** কার্ভটির কেন্দ্র বরাবর ভাগ করলে বাম ও ডান পাশ একে অপরের প্রতিবিম্ব (মিরর ইমেজ) হয়। এখানে $Mean = Median = Mode$।
> 4. **বাস্তব জীবনের উদাহরণ:** মানুষের উচ্চতা, ক্লাসের পরীক্ষার ফলাফল, মেজারমেন্ট এরর ইত্যাদি।

- **NumPy Syntax**:
  ```python
  # Standard Normal: mean=0, std=1
  z = np.random.randn(10000)

  # General Normal: mean=100, std=10
  norm_vals = np.random.normal(loc=100, scale=10, size=10000)
  ```

---

### 4. Random Permutation & Sequence Shuffling
- Reorders elements of an array or integer range without replacement.
- **NumPy Syntax**:
  ```python
  perm_0_to_9 = np.random.permutation(10)
  perm_1_to_10 = np.random.permutation(np.arange(1, 11))
  ```

---

### 5. Seed Control & Determinism in PRNG
- **Deterministic Randomness**: Setting a seed fixes the starting state of the Pseudo-Random Number Generator (PRNG).
- **NumPy Syntax**:
  ```python
  # Reproducible Output:
  np.random.seed(10)
  seeded_matrix = np.random.randint(1, 51, (3, 3))

  # Stochastic / Non-reproducible Output:
  np.random.seed(None)
  unseeded_matrix = np.random.randint(1, 51, (3, 3))
  ```

---

### 6. Law of Large Numbers (LLN)
- As sample size $N$ increases ($N = 10 \to N = 500 \to N = 100,000$), the empirical distribution converges to the theoretical probability density function, reducing stochastic fluctuation.
