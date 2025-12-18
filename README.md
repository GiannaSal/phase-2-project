
# phase-2-project
# data science phase 2 project



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


# phase-2-project
data science phase 2 project
## Movie Budget vs Performance Analysis

## Overview

This project analyzes how different movie genres perform relative to their budgets. The main objective is to group movie genres according to their budgets and evaluate which genres are most efficient in generating revenue per unit of budget.

## Datasets

Three datasets were utilized in this analysis:
	1.	movie_budgets
	•	Contains budget information for movies.
	•	Challenges: Some budget values were missing or inconsistent across records.
	2.	movie_gross
	•	Contains revenue (gross) information for movies.
	•	Challenges: Revenue data required cleaning and alignment with budget data to ensure accurate analysis.
	3.	tmdb.movies
	•	Contains movie metadata including genre information.
	•	Challenges: Genres were represented numerically rather than descriptively.
	•	Solution: A genre name column was created using reference data obtained from the TMDb website to map numerical genre IDs to readable genre names.

## Analysis Approach
	1.	Data Cleaning and Integration
	•	Standardized budgets and revenue data.
	•	Merged datasets on common movie identifiers to form a complete dataset containing budget, gross revenue, and genre information.
	2.	Genre Classification
	•	Mapped numerical genre IDs to descriptive genre names.
	•	Grouped movies by genre for comparative analysis.
	3.	Ratings Evaluation

	

## Key Insights
	•	The analysis identifies genres that are most budget-efficient.
	•	Provides insights for production and investment decisions in the film industry.

Notes
	•	Data inconsistencies and missing values were handled where possible.


## Insights
	•	Low-budget genres like Comedy, Drama, and Romance maintain solid ratings with higher counts of movies, indicating consistent audience appeal.
	•	Action and Adventure genres perform better in mid to high budget categories with higher average ratings, suggesting higher investment yields slightly higher audience appreciation.
	•	Science Fiction and Fantasy show high ratings in mid to high budget categories, but the sample size is small, so results should be interpreted cautiously.
	•	Overall, lower-mid to high budget Action and Adventure movies are most efficient in combining budget with audience ratings.



    

## Box Office EDA: Consistently Top-Performing Genres and Studios (2010–2018)

## Project context

This analysis was conducted to support a strategic decision: the company intends to launch a new movie studio and needs evidence on what types of films are currently doing well at the box office, translated into practical go-ahead guidance.

Because “doing well” can be interpreted as “highest total earnings overall” or “reliably strong year after year,” the notebook focuses on consistency: categories that repeatedly rank near the top across many years, and whose performance is not driven by a random or single ups/peaks.

## Data used and what it contains

Two datasets were used for complementary purposes:

1) Box Office Mojo gross dataset (bom.movie_gross.csv.gz)
This dataset contains movie-level box office earnings with fields similar to:
	•	title, studio, domestic_gross, foreign_gross, year

From this, we created an earnings metric (worldwide gross) by combining domestic and foreign grosses where available. This dataset is reliable for studio performance, because studio labels are present and gross is numeric.

2) IMDb database extract (im.db.zip)
This source was useful for title metadata and genres (e.g., “Drama,” “Action,” etc.). However, it typically does not include box office earnings, which created a key hinderance: genres exist here, but gross exists in the BOM file, and a clean genre-to-gross join is not available without enrichment and careful title matching.

## Data preparation and observations from the code

The work followed a standard EDA and cleaning pipeline:
	•	Loaded the BOM gross file and inspected shape, columns, dtypes, and missingness.
	•	Coerced gross columns to numeric (handling nulls/non-numeric values).
	•	Constructed a usable earnings column (worldwide gross via domestic + foreign).
	•	Normalized time (year) and removed/handled incomplete rows where earnings could not be computed.
	•	Aggregated results at a yearly level to prevent one very large year from dominating the entire ranking unfairly.

A crucial observation surfaced during execution: the BOM gross dataset does not include a genre column. As a result, the notebook includes two useful batches of information:
	•	a studio track that is fully supported by true gross data, and
	•	a genre track that can only be definitively answered once the dataset is enriched with genre labels for the gross records.

Where genre-to-gross was not directly available, the notebook used a rough early estimate by looking at IMDb engagement (like number of votes) as a stand-in for audience interest. This is disclosed explicitly below because it materially affects how strongly we can claim “top earning” by genre.

## Methods used to produce the findings

To make “consistency” measurable and defensible, the analysis used the following approach for each category (studio, and genre where applicable):
	1.	Yearly totals: compute total earnings per category per year.
	2.	Ranking-based consistency: count how often a category ranks #1 or appears in the top 3 across the observed years.
	3.	Stability metrics: compute variability using standard deviation and the coefficient of variation (CV = std/mean), where lower CV implies more stable year-to-year performance.
	4.	Composite interpretation: categories that are frequently top-ranked and have reasonable stability are treated as “consistently strong.”

This combination avoids a common trap where one blockbuster year makes a category look dominant “overall,” even if it is otherwise unreliable.

## Findings

Studio performance (based on true box office gross)

Across the 9-year window observed (2010–2018), a small set of studios repeatedly led total worldwide box office and also showed relatively stable annual performance:
	•	BV (Buena Vista / Disney) had the highest average annual worldwide gross at approximately $4.91B, with CV ≈ 0.27 (strong and comparatively steady).
	•	Fox followed at about $3.45B, CV ≈ 0.28.
	•	WB (Warner Bros.) was close behind at about $3.43B, CV ≈ 0.29.
	•	Uni. (Universal) averaged about $3.31B, CV ≈ 0.32.
	•	Sony averaged about $2.49B, with a notably low CV ≈ 0.25 among the top group (strong stability relative to peers).
	•	Par. (Paramount) averaged about $2.17B, CV ≈ 0.30.

What this means in practice: if you were benchmarking “what a reliably successful commercial slate looks like,” these studios are the closest available proxies for repeatable execution—because they don’t only win once; they remain near the top across years.

Genre performance (current run is not yet true “box office by genre”)

A cautious but important point: the current dataset state does not support a clean, defensible “box office gross by genre” conclusion, because the gross file lacks genre labels.

To avoid pretending the genre question was answered when it wasn’t, the notebook’s genre section used a proxy metric (IMDb numvotes) for a preliminary view of which genres appear to attract consistently high audience engagement across years. Under that proxy-based definition of consistency:
	•	Drama emerged as the most consistently top-performing genre, ranking #1 in 8 years and appearing in the top 3 in 9 years, with an average yearly proxy performance of roughly 11.96M and a CV ≈ 0.41.
	•	Action followed with strong average proxy performance (≈ 10.12M) and relatively better stability (CV ≈ 0.35), but fewer #1 finishes.

These findings are useful as a directional signal on audience interest consistency, but they should not be represented as “highest box office earnings by genre” until the genre-to-gross enrichment step is completed.

Recommendations for the head of the new studio

## The recommendations are split into what can be acted on confidently now versus what should be finalized after enrichment.

From the studio (true gross) results, the strongest actionable takeaway is benchmarking and strategy design:
	•	Use the top studios’ output as a reference for what “repeatable commercial success” looks like: Careful planning of the movie lineup (choosing the right mix of films and release timing), franchise strategy, distribution strength, release timing, and portfolio balance. If you intend to compete commercially, you are implicitly competing against the playbooks of BV/Disney, Fox, WB, Universal, Sony, and Paramount.

From the genre (proxy-based) results, the takeaway is conditional:
	•	If you must make an early movie line-up decision before enrichment is complete, a defensible ready strategy is to ensure a portion of the content is in Drama (because it is consistently high-engagement) and pair it with Action/Adventure-style projects as higher-upside commercial swings—while treating this as provisional pending true gross-by-genre validation.

Across both tracks, the practical film for consumption logic is portfolio-based rather than “pick one genre forever”: consistent categories fund experimentation, while a smaller share of higher-variance bets creates upside.

## Next steps to make the genre conclusion analytically dependable: 

To answer the business question exactly as stated (Question 1 as part of the overall business analysis “which genre consistently earns the most at the box office”), the next iteration should:
	1.	Enrich the BOM gross dataset with genres by joining a reliable genre source (e.g., IMDb title.basics TSV, TMDB exports/API). This requires careful title normalization and year alignment to avoid false matches.
	2.	Re-run the same yearly aggregation + ranking + stability framework using worldwide gross as the earnings metric, now grouped by genre.
	3.	Add budget (where available) to shift from “gross” to ROI, because high gross can still be a poor business if costs are extreme.
	4.	Stress-test results using medians (not just means), inflation adjustment, and separating franchise sequels from originals, so the final recommendation reflects a strategy the studio can actually replicate.

[Tableau Dashboard](https://public.tableau.com/app/profile/innocent.moruri/viz/Group3Analysis1-DirectorWriterImpactonBudgetPerformance/Dashboard1)

<img width="1304" height="749" alt="Screenshot 2025-12-18 at 18 08 07" src="https://github.com/user-attachments/assets/a980b826-6866-426d-88a7-a5d5e3bfc153" />




