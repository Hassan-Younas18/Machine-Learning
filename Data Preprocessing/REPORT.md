# DL-3002 Data Mining Lab — Lab Task 1
## Analysis Report: Movies and FIFA Datasets

| | |
|---|---|
| **Course** | DL-3002 Data Mining Lab |
| **Instructor** | Saad Munir |
| **Student** | Hassan Younas |
| **Institution** | Department of Computer Science, FAST-NUCES, Islamabad |
| **Submission** | Lab Task 1 |

---

## 1. Introduction

This report documents the complete exploratory data analysis (EDA) performed on two distinct
real-world datasets:

- **1000 Movies Data.csv** — 1,000 IMDb-catalogued films with attributes spanning ratings,
  revenue, runtime, director, genre, and vote counts.
- **Fifa.csv** — 18,278 professional footballers with 104 attributes including wages, physical
  measurements, nationality, and skill ratings extracted from the FIFA video-game database.

The analysis is divided into three phases: *Data Loading & Exploration*, *Data Manipulation*,
and *Data Visualization*, each designed to extract meaningful patterns and insights from raw data.

---

## 2. Task 1 — Data Loading and Exploration

### 2.1 Dataset Overview

| Dataset | Rows | Columns |
|---------|------|---------|
| Movies | 1,000 | 12 |
| FIFA | 18,278 | 104 |

**Movies columns:** `Rank`, `Title`, `Genre`, `Description`, `Director`, `Actors`, `Year`,
`Runtime (Minutes)`, `Rating`, `Votes`, `Revenue (Millions)`, `Metascore`

### 2.2 Descriptive Statistics — Movies

| Statistic | Runtime (min) | Rating | Votes | Revenue ($M) |
|-----------|--------------|--------|-------|-------------|
| Mean | 113.2 | 6.72 | 169,808 | 82.96 |
| Median | 111.0 | 6.80 | 61,480 | 47.99 |
| Std Dev | 18.9 | 1.06 | 270,629 | 103.25 |
| Min | 66 | 1.9 | 61 | 0.0 |
| Max | 191 | 9.0 | 1,791,916 | 936.63 |

The large gap between mean and median in `Votes` and `Revenue` reflects highly right-skewed
distributions — a small number of blockbusters dominate the upper tail.

### 2.3 Missing Values and Handling Strategy

| Column | Missing Count | Missing % | Strategy |
|--------|--------------|-----------|---------|
| Revenue (Millions) | 128 | 12.8% | Retain rows; drop inline for revenue analyses |
| Metascore | 64 | 6.4% | Retain rows; drop inline where required |

**Rationale:** Blindly dropping 128 rows (12.8% of the dataset) would introduce systematic bias
because lower-profile films are more likely to lack revenue records. Retaining all rows and
filtering inline for specific computations preserves the full dataset for non-revenue analyses
(ratings, genres, directors, runtime).

For the FIFA dataset, many columns (`loaned_from`, `nation_position`, `nation_jersey_number`)
contain blanks only for players not on loan or not in national-team duty — this is *structurally
expected* and does not represent data quality problems.

---

## 3. Task 2 — Data Manipulation

### 3.1 Top 10 Movies by Rating and Votes

Movies are ranked by **Rating** first, then **Votes** as a tiebreaker to balance critical quality
with audience reach.

| Rank | Title | Rating | Votes | Director | Year |
|------|-------|--------|-------|----------|------|
| 1 | The Dark Knight | 9.0 | 1,791,916 | Christopher Nolan | 2008 |
| 2 | Inception | 8.8 | 1,583,625 | Christopher Nolan | 2010 |
| 3 | Dangal | 8.8 | 48,969 | Nitesh Tiwari | 2016 |
| 4 | Interstellar | 8.6 | 1,047,747 | Christopher Nolan | 2014 |
| 5 | The Intouchables | 8.6 | 557,965 | Olivier Nakache | 2011 |
| 6 | Kimi no na wa | 8.6 | 34,110 | Makoto Shinkai | 2016 |
| 7 | The Dark Knight Rises | 8.5 | 1,222,645 | Christopher Nolan | 2012 |
| 8 | The Departed | 8.5 | 937,414 | Martin Scorsese | 2006 |
| 9 | The Prestige | 8.5 | 913,152 | Christopher Nolan | 2006 |
| 10 | Whiplash | 8.5 | 477,276 | Damien Chazelle | 2014 |

**Observation:** Christopher Nolan appears **5 times** in this list, confirming his exceptional
consistency across both critical acclaim and audience engagement.

### 3.2 Top 10 Movies by Highest Gross Revenue

> *Note: The dataset provides `Revenue (Millions)` but no budget figures, so gross revenue serves
> as a proxy for profitability.*

| Rank | Title | Revenue ($M) | Rating | Director |
|------|-------|-------------|--------|----------|
| 1 | Star Wars: The Force Awakens | $936.63M | 8.1 | J.J. Abrams |
| 2 | Avatar | $760.51M | 7.8 | James Cameron |
| 3 | Jurassic World | $652.18M | 7.0 | Colin Trevorrow |

**Observation:** The highest-grossing films span a wide rating range (7.0–8.1), reinforcing that
franchise power and marketing muscle can drive revenue independently of critical reception.

### 3.3 Relationship Between Rating and Revenue

**Pearson r = 0.2177** — a *weak positive* correlation.

Higher-rated films tend to earn slightly more on average, but the relationship is not strong
enough to be predictive. Several factors explain this:

- **Genre bias:** Action, superhero, and franchise films earn disproportionate revenues regardless
  of ratings (e.g., Jurassic World: 7.0 rating, $652M revenue).
- **Marketing and brand recognition** heavily influence revenue — qualities not captured in ratings.
- **Limited data:** Revenue records exist for only ~87% of films, and the missing entries are
  biased toward lower-profile releases.

**Conclusion:** Movies with higher ratings do **not** always earn higher revenues.

### 3.4 Average Runtime by Director

The most prolific director in the dataset is **Ridley Scott** with **8 movies**. Christopher Nolan,
known for ambitious narratives, has a noticeably higher-than-average runtime reflecting his
preference for elaborate storytelling.

### 3.5 Genre with Highest Average Rating

After exploding the multi-genre `Genre` column so each genre is counted independently:

| Rank | Genre | Avg Rating | Movie Count |
|------|-------|-----------|-------------|
| 1 | **War** | **7.354** | 26 |
| 2 | Animation | 7.324 | 49 |
| 3 | Biography | 7.290 | 81 |
| 4 | History | 7.128 | 29 |
| 5 | Music | 7.075 | 20 |

**Observation:** War and Animation films earn the highest average ratings. These genres tend to
attract serious creative investments and self-selected audiences with strong pre-existing interest,
naturally elevating ratings.

### 3.6 Total Revenue by Year

**Peak year: 2016** with a total gross revenue of **$11,211.6 Million** across all movies in the
dataset for that year. This reflects the dominance of major studio franchises (Marvel, DC,
animated blockbusters) during the 2010s.

### 3.7 Most Prolific Director

**Ridley Scott** directed the most movies in the dataset (**8 films**), spanning genres from
science fiction to historical epics.

### 3.8 Correlation Between Runtime and Rating

**Pearson r = 0.3922** — a *weak-to-moderate positive* correlation.

Films with longer runtimes score marginally higher on IMDb, but the relationship is insufficient
to use runtime as a predictor. Longer films may attract higher ratings because:
- Studios allocate more runtime to ambitious, high-budget productions.
- Audiences who commit to a 3-hour film typically have strong prior interest or trust in the
  filmmaker, producing a favourable rating bias.

**Conclusion:** Runtime alone does **not** reliably predict ratings.

### 3.9 Movie with the Longest Runtime

| Attribute | Value |
|-----------|-------|
| **Title** | Grindhouse |
| **Director** | Robert Rodriguez |
| **Year** | 2007 |
| **Runtime** | 191 minutes |

### 3.10 Highest Paid Footballers from Germany (FIFA)

| Rank | Name | Club | Weekly Wage (EUR) |
|------|------|------|------------------|
| 1 | T. Kroos | Real Madrid | €330,000 |
| 2 | M. ter Stegen | FC Barcelona | €250,000 |
| 3 | L. Sane | Manchester City | €195,000 |

### 3.11 Average Height of French Footballers

| Statistic | Value |
|-----------|-------|
| Count | 914 players |
| **Average height** | **181.86 cm** (~5 ft 11.6 in) |
| Minimum | 166 cm |
| Maximum | 201 cm |

French footballers are slightly above the global average footballer height, consistent with
France's tradition of producing physically well-rounded players.

---

## 4. Task 3 — Data Visualization

### 4.1 Distribution of Movie Durations (Histogram)

The runtime distribution is **right-skewed**:
- Mean: **113.2 minutes**, Median: **111.0 minutes** (mean > median confirms skew)
- The bulk of films cluster between **90 and 120 minutes**, the standard commercial window
- A long right tail extends to 191 minutes (Grindhouse)

### 4.2 Distribution of Movie Ratings (Histogram)

The rating distribution is **approximately normal** with a slight left skew:
- Mean: **6.72**, Median: **6.80**
- Most films rate between 6.0 and 8.0
- Very few films fall below 4.0 — this dataset captures notable releases, not random samples

### 4.3 Average Rating per Genre (Bar Chart)

War, Animation, and Biography lead the genre rankings. Niche genres with passionate fan bases
(War: 26 films, Music: 20 films) produce higher concentrated ratings compared to mass-market
genres like Action or Comedy which face greater rating dilution across large, heterogeneous
audiences.

### 4.4 World's Highest Paid Footballers (Bar Chart)

At the time of the FIFA dataset snapshot:
- **L. Messi** (Argentina / FC Barcelona) leads at **€565,000/week**
- **E. Hazard** (Belgium) follows at **€470,000/week**
- **C. Ronaldo** (Portugal / Juventus) earns **€405,000/week**

The bar chart starkly illustrates how wages are heavily concentrated at the very top of the
talent pyramid, with a sharp drop-off after the top 3–5 players.

### 4.5 World's Fastest Footballers — Top 10 by Pace (Bar Chart)

Top pace ratings:
- **Adama Traore** (Spain) — 96
- **K. Mbappé** (France) — 96
- **K. Nagai** (Japan) — 95

The fastest players are predominantly wingers and attacking fullbacks, positions where explosive
speed is the primary attribute.

---

## 5. Summary and Conclusions

### Movies Dataset

| Question | Finding |
|----------|---------|
| Best films (rating + votes) | The Dark Knight dominates; Christopher Nolan placed 5/10 |
| Highest grossing | Star Wars: TFA ($936.63M), Avatar ($760.51M) |
| Rating ↔ Revenue | Weak positive (r = 0.22) — revenue driven more by franchise than quality |
| Runtime ↔ Rating | Weak-to-moderate positive (r = 0.39) — longer films score marginally higher |
| Top genre | War (avg rating: 7.35) |
| Peak revenue year | 2016 ($11.2B total) |
| Most prolific director | Ridley Scott (8 movies) |
| Longest film | Grindhouse (191 min, 2007) |

### FIFA Dataset

| Question | Finding |
|----------|---------|
| Highest paid German | T. Kroos — €330,000/week at Real Madrid |
| Avg height (France) | 181.86 cm |
| World's highest paid | L. Messi — €565,000/week |
| World's fastest | Adama Traore & K. Mbappé — pace rating 96 |

### Broader Insights

1. **Revenue is not a proxy for quality.** The weak rating-revenue correlation shows the market
   rewards franchise power, spectacle, and marketing budgets as much as — or more than —
   critical excellence.

2. **Genre composition shapes perceived quality.** War and Biography genres attract committed
   viewers with high critical standards, producing higher average ratings than mass-market genres.

3. **Wage inequality in football is extreme.** The top earners command wages orders of magnitude
   above average, reflecting winner-takes-most market dynamics in elite sports.

4. **Missing data requires judgment, not reflexes.** Blindly dropping NaN rows would have
   introduced systematic bias and reduced analytical power. A column-specific strategy (retain
   for general analysis, drop inline for specific computations) produced a richer analysis.

---

## 6. Tools and Technologies

| Tool | Version | Role |
|------|---------|------|
| Python | 3.11 | Runtime |
| Pandas | ≥ 1.5 | Data loading, manipulation, groupby |
| NumPy | ≥ 1.23 | Array operations, Pearson correlation |
| Matplotlib | ≥ 3.6 | Histograms, scatter plots, bar charts |

---

*Report prepared for DL-3002 Data Mining Lab, FAST-NUCES Islamabad.*
