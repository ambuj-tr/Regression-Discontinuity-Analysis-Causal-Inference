# 📊 Regression Discontinuity Design for Causal Inference

<p align="center">

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Statsmodels](https://img.shields.io/badge/Statsmodels-Statistical%20Modeling-4051B5?style=for-the-badge)
![Linearmodels](https://img.shields.io/badge/Linearmodels-IV%20%7C%202SLS-8A2BE2?style=for-the-badge)
![Causal Inference](https://img.shields.io/badge/Causal-Inference-FF6F00?style=for-the-badge)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-Interactive%20Visualization-3F4F75?style=for-the-badge&logo=plotly&logoColor=white)

</p>

---

# 📖 Project Overview

This project demonstrates the practical application of **Regression Discontinuity Design (RDD)** as a causal inference technique for estimating treatment effects in quasi-experimental settings.

Regression Discontinuity is particularly useful when treatment or program eligibility is determined by whether an observable variable crosses a predefined **cutoff or threshold**. Instead of relying only on correlation, RDD uses observations around that threshold to investigate whether the outcome changes discontinuously when treatment assignment changes.

The notebook explores two major forms of Regression Discontinuity:

- 🔵 **Sharp Regression Discontinuity Design**
- 🟠 **Fuzzy Regression Discontinuity Design**

The project begins with a Sharp RDD example based on an **age-21 threshold and all-cause mortality**. It then extends the analysis to a Fuzzy RDD example using a **tutoring-program dataset**, where tutoring eligibility is determined by an entrance-exam cutoff.

The Fuzzy RDD section further introduces **Instrumental Variables (IV)** and **Two-Stage Least Squares (2SLS)** to estimate the causal effect when treatment assignment is not perfectly enforced.

---

# 🎯 Aim

The primary objectives of this project are to:

- Understand the fundamentals of Regression Discontinuity Design.
- Estimate causal effects around a predefined cutoff.
- Understand the difference between Sharp and Fuzzy RDD.
- Analyze treatment assignment based on a running variable.
- Center the running variable around the cutoff.
- Explore linear and quadratic RDD specifications.
- Understand the importance of bandwidth selection.
- Apply heteroskedasticity-robust standard errors.
- Examine possible discontinuities in other variables.
- Understand treatment non-compliance in Fuzzy RDD.
- Apply Instrumental Variables to estimate causal effects.
- Implement Two-Stage Least Squares (2SLS).
- Understand Local Average Treatment Effect (LATE).

---

# 💡 Why Regression Discontinuity?

Traditional predictive modeling mainly focuses on:

```text
"What can we predict?"
```

Causal inference focuses on:

```text
"What is the effect of changing the treatment?"
```

RDD provides a quasi-experimental framework for answering this question when treatment assignment is determined by a known threshold.

For example:

```text
                Cutoff
                   │
                   ▼
─────────────── 70 ───────────────
     Control          Treatment
```

Observations close to the threshold can be compared because they are more similar in terms of the running variable.

The key idea is to determine whether there is a **discontinuity in the outcome at the treatment cutoff**.

---

# ✨ Project Highlights

✅ Regression Discontinuity Design

✅ Sharp RDD

✅ Fuzzy RDD

✅ Cutoff-Based Treatment Assignment

✅ Running Variable Analysis

✅ Variable Centering

✅ Exploratory Data Visualization

✅ Linear RDD

✅ Quadratic RDD

✅ Treatment × Running Variable Interactions

✅ Bandwidth Analysis

✅ Robust Standard Errors

✅ RDD Validity Checks

✅ Instrumental Variables

✅ Two-Stage Least Squares (2SLS)

✅ Local Average Treatment Effect (LATE)

✅ Causal Effect Interpretation

---

# 🔵 Sharp Regression Discontinuity

The first section implements a **Sharp RDD** example using an age-based cutoff.

### Running Variable

```text
Age
```

### Cutoff

```text
21 years
```

### Treatment Definition

```text
Age >= 21 → Treatment
Age < 21  → Control
```

The notebook centers the running variable around the threshold:

```text
Age_centered = Age - 21
```

The outcome analyzed is **all-cause mortality**.

This creates a local comparison around the age-21 threshold to investigate whether the outcome exhibits a discontinuous change at the cutoff.

---

# 📈 Sharp RDD Model

The analysis begins with a basic specification:

```text
Outcome ~ Treatment + Centered Running Variable
```

The notebook then extends the model to include:

- Treatment × Age interaction
- Age²
- Age² × Treatment interaction

This allows different functional relationships on either side of the cutoff.

The quadratic specification provides greater flexibility than forcing the relationship to follow a single straight line.

---

# 🧮 Quadratic RDD

The notebook explicitly introduces quadratic terms because a linear specification may be too restrictive when modeling the relationship between the running variable and outcome.

Conceptually:

```text
Linear RDD
Outcome = β₀ + β₁Treatment + β₂Age + ε
```

Extended model:

```text
Outcome =
β₀
+ β₁Treatment
+ β₂Age
+ β₃Treatment×Age
+ β₄Age²
+ β₅Treatment×Age²
+ ε
```

This allows the model to capture curvature and different trends around the threshold.

---

# 📏 Bandwidth Analysis

RDD is fundamentally a **local estimation method**.

The project therefore examines observations closer to the cutoff rather than relying only on the complete sample.

Conceptually:

```text
Full Dataset
────────────────────────────────────────

              │
            Cutoff
              │

      ◄──── Bandwidth ────►
              │
```

A narrower bandwidth means the analysis focuses more closely on observations around the cutoff.

This creates an important trade-off:

```text
Wider Bandwidth
→ More observations
→ Greater statistical information
→ Potentially less local

Narrower Bandwidth
→ More local comparison
→ Fewer observations
→ Potentially larger uncertainty
```

The notebook demonstrates this trade-off when estimating the treatment effect closer to the cutoff.

---

# 🛡️ Robust Standard Errors

The Sharp RDD models use **HC1 heteroskedasticity-robust standard errors**.

This provides more robust statistical inference when the regression error variance may not be constant across observations.

---

# 🔍 RDD Validity Checks

An important part of RDD is checking whether other variables also exhibit discontinuities at the cutoff.

The notebook highlights:

```text
"Do other variables jump at the cut-off?"
```

This matters because a discontinuity in unrelated variables could indicate that something other than the intended treatment is changing at the threshold.

Therefore, cutoff-based validity checks are an important part of interpreting an RDD design.

---

# 🟠 Fuzzy Regression Discontinuity

The second section implements a **Fuzzy RDD** using a tutoring-program dataset.

Unlike Sharp RDD, crossing the cutoff does not perfectly determine who receives treatment.

Instead, the threshold changes the **probability of treatment**.

### Dataset Variables

| Variable | Description |
|----------|-------------|
| `id` | Unique observation identifier |
| `entrance_exam` | Entrance examination score |
| `tutoring` | Whether the student received tutoring |
| `tutoring_text` | Text representation of tutoring status |
| `exit_exam` | Exit examination score |

---

# 📊 Dataset Analysis

The uploaded tutoring dataset contains:

```text
Rows:    1,000
Columns: 5
Missing Values: 0
```

The dataset contains **318 students who received tutoring** and **682 who did not**.

The entrance-exam score ranges approximately from:

```text
28.84 → 99.78
```

with an average of approximately:

```text
78.14
```

The exit-exam score has an average of approximately:

```text
66.94
```

---

# 🎯 Fuzzy RDD Cutoff

The tutoring example uses an entrance-exam cutoff of:

```text
70
```

The running variable is centered as:

```text
entrance_centered = entrance_exam - 70
```

The notebook creates an eligibility/instrument variable:

```text
V = 1  if entrance_exam < 70
V = 0  otherwise
```

This cutoff-based variable is subsequently used as an instrument for actual tutoring participation.

---

# ⚖️ Treatment Assignment Around the Cutoff

The dataset also illustrates the difference between **eligibility and actual treatment**.

Among students with entrance-exam scores below 70, approximately:

```text
84.9% received tutoring
```

Among students with scores of 70 or above:

```text
15.2% received tutoring
```

This shows that the cutoff strongly changes treatment probability without perfectly determining treatment assignment.

That is the key setting in which **Fuzzy RDD** becomes useful.

---

# 🔀 Sharp vs Fuzzy RDD

| Sharp RDD | Fuzzy RDD |
|-----------|-----------|
| Cutoff determines treatment directly | Cutoff changes treatment probability |
| Assignment is deterministic | Assignment is imperfect |
| Treatment status follows threshold | Some units do not comply |
| Direct RDD estimation | IV / 2SLS is required |
| Treatment effect at cutoff | Local treatment effect for affected units |

---

# ⚠️ Why Naive OLS Is Not Enough

The project first estimates a simple OLS model:

```text
Exit Exam ~ Tutoring + Entrance Score
```

This produces a direct association between tutoring and exit-exam performance.

However, in a Fuzzy RDD setting, actual tutoring participation is not perfectly determined by the cutoff.

Students can differ in treatment participation even when they are on the same side of the threshold.

This creates a potential **endogeneity problem**, making a direct OLS estimate unsuitable as the primary causal estimate.

---

# 🧠 Instrumental Variables

To address treatment non-compliance, the project uses an **Instrumental Variable (IV)**.

The cutoff-based eligibility variable:

```text
V
```

acts as an instrument for:

```text
Tutoring
```

The causal structure can be represented as:

```text
Entrance Exam Cutoff
          │
          ▼
       Eligibility
          │
          ▼
       Tutoring
          │
          ▼
      Exit Exam
```

The instrument provides variation in treatment participation associated with the threshold.

---

# 🧮 Two-Stage Least Squares (2SLS)

The project implements **IV2SLS** using the `linearmodels` library.

### Stage 1 — Predict Treatment

```text
Tutoring
    ↑
    │
Eligibility Instrument + Running Variable
```

The first stage estimates treatment participation using the cutoff-based instrument.

### Stage 2 — Estimate Outcome

```text
Exit Exam
    ↑
    │
Predicted Tutoring + Running Variable
```

The second stage estimates the causal effect of the treatment using the predicted treatment component.

This approach addresses the treatment non-compliance present in the Fuzzy RDD setting.

---

# 🎯 Local Average Treatment Effect (LATE)

The Fuzzy RDD / IV framework estimates a **Local Average Treatment Effect (LATE)**.

LATE represents the causal effect for observations whose treatment status is affected by the cutoff-based instrument.

This is an important distinction from a simple average treatment effect across the entire population.

---

# ⚙️ Complete Project Workflow

```text
                  CAUSAL INFERENCE
                         │
                         ▼
                  Dataset Analysis
                         │
                         ▼
                Identify Running Variable
                         │
                         ▼
                    Define Cutoff
                         │
              ┌──────────┴──────────┐
              │                     │
              ▼                     ▼
          Sharp RDD             Fuzzy RDD
              │                     │
              ▼                     ▼
      Define Treatment        Define Eligibility
              │                     │
              ▼                     ▼
     Center Running Variable  Center Running Variable
              │                     │
              ▼                     ▼
       Linear Specification    Naive OLS Model
              │                     │
              ▼                     ▼
      Quadratic Specification  Identify Non-Compliance
              │                     │
              ▼                     ▼
       Bandwidth Analysis       Instrumental Variable
              │                     │
              ▼                     ▼
      Robust Standard Errors        2SLS
              │                     │
              ▼                     ▼
       RDD Interpretation          LATE
              │                     │
              └──────────┬──────────┘
                         ▼
                Causal Interpretation
```

---

# 🛠️ Tech Stack

| Category | Technologies |
|----------|--------------|
| Programming Language | Python |
| Data Manipulation | Pandas, NumPy |
| Statistical Modeling | Statsmodels |
| Instrumental Variables | Linearmodels |
| Causal Estimation | RDD, IV, 2SLS |
| Visualization | Plotly |
| Data Format | CSV / Stata |
| Notebook Environment | Jupyter Notebook |

---

# 📊 Results

The project demonstrates how causal effects can be studied when treatment assignment is governed by a threshold.

### 🔵 Sharp RDD

The Sharp RDD section investigates the change in all-cause mortality around the age-21 threshold using:

- Linear RDD
- Quadratic RDD
- Interaction terms
- Robust standard errors
- Local bandwidth analysis

### 🟠 Fuzzy RDD

The tutoring dataset contains **1,000 observations** and shows a strong difference in treatment participation around the score-70 cutoff.

A direct OLS model estimates the observed tutoring association, while the IV/2SLS model is used to account for imperfect treatment assignment and estimate the local causal effect.

The notebook therefore demonstrates the transition from:

```text
Naive Association
        ↓
RDD Identification
        ↓
Instrumental Variables
        ↓
2SLS
        ↓
Local Causal Effect
```

---

# 🔍 Key Insights

### 1. Thresholds can create quasi-experiments

A known treatment cutoff can provide a useful source of quasi-experimental variation.

### 2. Local comparisons are important

Observations close to the cutoff are generally the focus of RDD because they are more comparable in terms of the running variable.

### 3. Functional form matters

Linear and quadratic specifications can model the relationship around the cutoff differently.

### 4. Bandwidth affects estimation

Changing the region around the cutoff changes the number of observations and the degree of locality in the estimate.

### 5. Treatment compliance matters

Fuzzy RDD is necessary when eligibility does not perfectly determine treatment participation.

### 6. IV can address treatment endogeneity

The cutoff-based eligibility variable can be used as an instrument for treatment participation in a Fuzzy RDD design.

---

# 📚 Key Concepts Learned

- 🧠 Causal Inference
- 📊 Regression Discontinuity Design
- 🔵 Sharp RDD
- 🟠 Fuzzy RDD
- 🎯 Running Variables
- 🚦 Treatment Cutoffs
- 📐 Centered Variables
- 🧮 Linear Regression
- 📈 Quadratic Regression
- 🔄 Interaction Terms
- 📏 Bandwidth Analysis
- 🛡️ Robust Standard Errors
- 🔍 RDD Validity Checks
- 🧠 Instrumental Variables
- ⚙️ Two-Stage Least Squares
- 🎯 Local Average Treatment Effect
- 🔬 Quasi-Experimental Analysis

---

# 💼 Real-World Applications

Regression Discontinuity can be applied in many real-world settings where decisions are made using thresholds.

### 🎓 Education

Evaluating the effect of tutoring, scholarships, or admission programs based on entrance-exam scores.

### 🏥 Healthcare

Studying treatment effects when eligibility depends on age, medical scores, or clinical thresholds.

### 🏛️ Public Policy

Evaluating government programs assigned using income or eligibility thresholds.

### 💰 Economics

Analyzing the impact of subsidies, tax benefits, or financial assistance programs.

### 📊 Business

Studying customer programs, credit eligibility, promotional thresholds, or access to services.

---

# 📂 Repository Structure

```text
📦 Regression-Discontinuity-Causal-Inference
│
├── 📁 notebooks
│   └── Regression_Discontinuity.ipynb
│
├── 📁 data
│   └── tutoring_program_fuzzy.csv
│
├── 📁 images
│   ├── sharp_rdd.png
│   ├── quadratic_rdd.png
│   ├── bandwidth_analysis.png
│   ├── fuzzy_rdd.png
│   ├── tutoring_cutoff.png
│   └── treatment_effect.png
│
├── requirements.txt
├── LICENSE
└── README.md
```

---

# 🚀 Future Improvements

- Implement automated bandwidth selection.
- Add local polynomial regression.
- Perform placebo-cutoff tests.
- Conduct density tests around the cutoff.
- Add covariate balance diagnostics.
- Compare different RDD specifications.
- Implement additional IV estimators.
- Add sensitivity analysis.
- Explore heterogeneous treatment effects.
- Apply RDD to real-world healthcare and policy datasets.
- Build an interactive causal inference dashboard.
- Extend the project toward modern **Causal Machine Learning**.

---

# 🎓 Learning Outcomes

Through this project, you will gain practical experience in:

- Regression Discontinuity Design
- Sharp and Fuzzy RDD
- Quasi-Experimental Research
- Causal Identification
- Running Variable Analysis
- Cutoff-Based Treatment Assignment
- Polynomial Regression Specifications
- Bandwidth Selection
- Robust Statistical Inference
- Instrumental Variables
- Two-Stage Least Squares
- Local Average Treatment Effects
- Treatment Effect Estimation

---

# 📌 Project Significance

This project demonstrates a progression from traditional statistical modeling toward **causal reasoning**.

Rather than simply asking whether two variables are associated, the project investigates whether a treatment or intervention can be linked to a change in an outcome under a carefully defined quasi-experimental design.

By implementing both **Sharp and Fuzzy RDD**, and extending the Fuzzy RDD analysis to **Instrumental Variables and 2SLS**, the project provides a practical foundation for understanding how modern causal inference handles threshold-based treatment assignment and treatment non-compliance.

---

# 👨‍💻 Author

**Ambuj Tripathi**

🎓 Pre-Final Year B.Tech (Electronics & Computer Science)

🤖 Aspiring AI/ML Engineer

💡 **Interests:** Machine Learning • NLP • Deep Learning • LLMs • Agentic AI • Causal AI

---

⭐ **If you found this project useful, consider giving it a star!**
