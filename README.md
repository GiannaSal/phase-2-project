# phase-2-project
data science phase 2 project
Box Office EDA: Consistently Top-Performing Genres and Studios (2010–2018)

Project context

This analysis was conducted to support a strategic decision: the company intends to launch a new movie studio and needs evidence on what types of films are currently doing well at the box office, translated into practical go-ahead guidance.

Because “doing well” can be interpreted as “highest total earnings overall” or “reliably strong year after year,” the notebook focuses on consistency: categories that repeatedly rank near the top across many years, and whose performance is not driven by a random or single ups/peaks.

Data used and what it contains

Two datasets were used for complementary purposes:

1) Box Office Mojo gross dataset (bom.movie_gross.csv.gz)
This dataset contains movie-level box office earnings with fields similar to:
	•	title, studio, domestic_gross, foreign_gross, year

From this, we created an earnings metric (worldwide gross) by combining domestic and foreign grosses where available. This dataset is reliable for studio performance, because studio labels are present and gross is numeric.

2) IMDb database extract (im.db.zip)
This source was useful for title metadata and genres (e.g., “Drama,” “Action,” etc.). However, it typically does not include box office earnings, which created a key hinderance: genres exist here, but gross exists in the BOM file, and a clean genre-to-gross join is not available without enrichment and careful title matching.

Data preparation and observations from the code

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

Methods used to produce the findings

To make “consistency” measurable and defensible, the analysis used the following approach for each category (studio, and genre where applicable):
	1.	Yearly totals: compute total earnings per category per year.
	2.	Ranking-based consistency: count how often a category ranks #1 or appears in the top 3 across the observed years.
	3.	Stability metrics: compute variability using standard deviation and the coefficient of variation (CV = std/mean), where lower CV implies more stable year-to-year performance.
	4.	Composite interpretation: categories that are frequently top-ranked and have reasonable stability are treated as “consistently strong.”

This combination avoids a common trap where one blockbuster year makes a category look dominant “overall,” even if it is otherwise unreliable.

Findings

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

The recommendations are split into what can be acted on confidently now versus what should be finalized after enrichment.

From the studio (true gross) results, the strongest actionable takeaway is benchmarking and strategy design:
	•	Use the top studios’ output as a reference for what “repeatable commercial success” looks like: Careful planning of the movie lineup (choosing the right mix of films and release timing), franchise strategy, distribution strength, release timing, and portfolio balance. If you intend to compete commercially, you are implicitly competing against the playbooks of BV/Disney, Fox, WB, Universal, Sony, and Paramount.

From the genre (proxy-based) results, the takeaway is conditional:
	•	If you must make an early movie line-up decision before enrichment is complete, a defensible ready strategy is to ensure a portion of the content is in Drama (because it is consistently high-engagement) and pair it with Action/Adventure-style projects as higher-upside commercial swings—while treating this as provisional pending true gross-by-genre validation.

Across both tracks, the practical film for consumption logic is portfolio-based rather than “pick one genre forever”: consistent categories fund experimentation, while a smaller share of higher-variance bets creates upside.

Next steps to make the genre conclusion analytically dependable: 

To answer the business question exactly as stated (Question 1 as part of the overall business analysis “which genre consistently earns the most at the box office”), the next iteration should:
	1.	Enrich the BOM gross dataset with genres by joining a reliable genre source (e.g., IMDb title.basics TSV, TMDB exports/API). This requires careful title normalization and year alignment to avoid false matches.
	2.	Re-run the same yearly aggregation + ranking + stability framework using worldwide gross as the earnings metric, now grouped by genre.
	3.	Add budget (where available) to shift from “gross” to ROI, because high gross can still be a poor business if costs are extreme.
	4.	Stress-test results using medians (not just means), inflation adjustment, and separating franchise sequels from originals, so the final recommendation reflects a strategy the studio can actually replicate.

