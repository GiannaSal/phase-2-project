# phase-2-project
data science phase 2 project
# Directors vs Writers: Impact on Movie Budget Performance (EDA)

## Project Overview

This notebook, `eda_directors_vs_writers.ipynb`, explores whether creative leadership choices—directors and writers—have a measurable impact on movie budget performance.

Using historical film data, the analysis focuses on Return on Investment (ROI) as the core financial metric and applies exploratory data analysis and statistical testing to determine whether differences in performance across directors and writers are statistically significant.

The project is designed to support evidence-based decision-making for a hypothetical new movie studio.

---

## Business Problem

A new movie studio wants to enter the market but lacks experience in film production.

**Key question:**

> Does the choice of director or writer materially influence a movie’s financial efficiency (ROI), or are outcomes primarily driven by randomness and budget size?

Answering this helps the studio:

* Decide who to hire
* Allocate budgets more efficiently
* Avoid value-destroying creative decisions

---

## Data Description

The analysis is built from multiple movie datasets that were cleaned and merged into an analysis-ready table.

Key fields include:

* `movie_id`
* Movie titles and release year
* Budget and revenue
* Director names
* Writer names
* Ratings and vote counts

### Key Metric

Return on Investment (ROI) is calculated as:

```
ROI = (Revenue − Budget) / Budget
```

ROI is used instead of raw revenue to normalize performance across different budget levels.

---

## Analytical Approach

### 1. Data Cleaning & Preparation

* Removed missing or invalid budget/revenue records
* Ensured one-to-many relationships (movies ↔ directors/writers) were handled correctly
* Computed ROI for each movie

### 2. Exploratory Data Analysis (EDA)

* Aggregated mean ROI by director** and by writer
* Ranked creatives based on ROI performance
* Visualized results using:

  * Scatter plots
  * Bar charts

This step identified visible performance differences and potential outliers.

### 3. Statistical Testing

To determine whether observed differences are real and not due to chance:

* **One-way ANOVA** was conducted separately for:

  * Directors
  * Writers

**Hypotheses:**

* *Null (H₀):* Mean ROI is the same across all directors/writers
* *Alternative (H₁):* At least one director/writer has a different mean ROI

**Significance level:** α = 0.05

---

## Key Results

### Directors

* ANOVA results show a statistically significant difference in ROI across directors
* Director identity meaningfully affects financial efficiency
* Some directors consistently generate higher ROI even at comparable budgets

### Writers

* Writer choice also exhibits statistically significant ROI differences
* Certain writers outperform peers in terms of budget efficiency
* Writing talent impacts not only narrative quality but financial outcomes

---

## Insights & Interpretation

* Creative leadership is not financially neutral
* Higher budgets do not guarantee better ROI
* Historical performance of directors and writers provides actionable signal

Statistical significance confirms that these patterns are unlikely to be driven by random variation alone.

---

## Recommendations

For a new or growing movie studio:

1. Incorporate director and writer ROI history into greenlight decisions
2. Prioritize *efficient creative profiles over reputation alone
3. Avoid consistently low-ROI creatives unless justified by strategic goals
4. Treat creative selection as a financial decision, not just an artistic one

---

## Notebook Outputs

The notebook produces:

* ROI rankings for directors and writers
* Visual comparisons of creative performance
* Statistical test outputs (ANOVA, p-values)
* Interpretable conclusions suitable for executives

---

## Tools & Libraries

* Python
* pandas
* numpy
* matplotlib
* scipy / statsmodels
* SQL (for aggregation where applicable)


---

## Conclusion

Both directors and writers have a statistically significant impact on movie budget performance.

For studios aiming to maximize ROI, creative selection should be treated as a core strategic and financial decision, supported by data rather than intuition alone.

