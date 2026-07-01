# DL-3002 Data Mining Lab — Task 1
### Exploratory Data Analysis: Movies & FIFA Datasets

> **Course:** DL-3002 Data Mining Lab &nbsp;|&nbsp; **Instructor:** Saad Munir  
> **Institution:** Department of Computer Science, FAST-NUCES, Islamabad

---

## Overview

This project performs a full **Exploratory Data Analysis (EDA)** on two real-world datasets using Python's core data-science stack. The analysis spans data loading, statistical profiling, missing-value handling, feature-level manipulation, and publication-quality visualisations.

| Dataset | Rows | Columns | Domain |
|---------|------|---------|--------|
| `1000 Movies Data.csv` | 1 000 | 12 | Film industry (IMDb-based) |
| `Fifa.csv` | 18 278 | 104 | Professional football (FIFA ratings) |

---

## Repository Structure

```
Lab 1/
├── lab_task_1.ipynb          # Main Jupyter Notebook (all tasks + outputs)
├── 1000 Movies Data.csv      # Movies dataset
├── Fifa.csv                  # FIFA player dataset
├── README.md                 # This file
├── REPORT.md                 # Detailed analysis report
└── Lab Task 1.pdf            # Original task specification
```

---

## Tasks at a Glance

### Task 1 — Data Loading & Exploration
- Load both datasets into Pandas DataFrames
- Inspect first/last 10 rows of each dataset
- Compute descriptive statistics (mean, median, std, quartiles)
- Identify and handle missing values with a reasoned strategy (no blind `dropna()`)

### Task 2 — Data Manipulation
| # | Analysis | Dataset |
|---|----------|---------|
| 2.1 | Top 10 movies by Rating + Votes | Movies |
| 2.2 | Top 10 highest-grossing movies (profit proxy) | Movies |
| 2.3 | Correlation: Rating vs Revenue + scatter plot | Movies |
| 2.4 | Average runtime per director | Movies |
| 2.5 | Genre with highest average rating | Movies |
| 2.6 | Total revenue per release year | Movies |
| 2.7 | Most prolific director | Movies |
| 2.8 | Correlation: Runtime vs Rating + scatter plot | Movies |
| 2.9 | Movie with the longest runtime (full details) | Movies |
| 2.10 | Highest-paid footballers from Germany | FIFA |
| 2.11 | Average height of French footballers | FIFA |

### Task 3 — Data Visualisation
| # | Chart | Dataset |
|---|-------|---------|
| 3.1 | Histogram — distribution of movie runtimes | Movies |
| 3.2 | Histogram — distribution of IMDb ratings | Movies |
| 3.3 | Bar chart — average rating per top-10 genre | Movies |
| 3.4 | Bar chart — world's highest-paid footballers | FIFA |
| 3.5 | Bar chart — world's fastest footballers (pace) | FIFA |

---

## Key Findings

- **Runtime distribution** is right-skewed: the vast majority of films run 90–120 minutes, with a long tail of epics pulling the mean up.
- **Rating distribution** is near-normal (centred ~6.7–7.0), indicating the dataset captures notable films rather than a random sample.
- **Rating ↔ Revenue** show only a *weak positive* correlation (r ≈ 0.19) — critical acclaim alone does not drive box-office success.
- **Runtime ↔ Rating** also share a *weak positive* correlation — longer films score marginally higher, but runtime is not a reliable predictor.
- **Germany's highest-paid** players are elite midfielders and forwards playing for top European clubs.
- **French footballers** average approximately **181 cm** in height, consistent with European norms.
- **World's fastest** players (pace ≥ 96) are predominantly attacking wingers.

---

## Getting Started

### Prerequisites

```bash
pip install numpy pandas matplotlib
```

### Running the Notebook

```bash
jupyter notebook lab_task_1.ipynb
```

Run all cells top-to-bottom (`Kernel → Restart & Run All`) — outputs and plots will be reproduced inline.

> **Note:** Both CSV files must be in the same directory as the notebook.

---

## Tech Stack

| Library | Version | Purpose |
|---------|---------|---------|
| Python | ≥ 3.9 | Runtime |
| Pandas | ≥ 1.5 | Data manipulation |
| NumPy | ≥ 1.23 | Numerical computation |
| Matplotlib | ≥ 3.6 | Visualisation |

---

## Author

**Hassan Younas**  
Department of Computer Science — FAST-NUCES, Islamabad  
Course: DL-3002 Data Mining Lab (Batch 21)
