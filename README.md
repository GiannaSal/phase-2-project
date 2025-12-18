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



    
