# What makes a movie popular? Genre, recency or rating?

A data cleaning and analysis project on ~9,800 popular films, in Python.

## Research question

Is a film's popularity explained mainly by its **genre**, by **how recently it was released**, or by **how well audiences rate it**?

## Data

`mymoviedb.csv` (in this repo): 9,837 popular films with release date, popularity score, vote count, average rating, original language and genres. It is often shared on Kaggle as a "Netflix" dataset, but every poster link points to The Movie Database (TMDB), so it describes popular films in general rather than Netflix's catalogue.

**Popularity** is TMDB's score for current attention (recent page views, votes and watch-list activity). It is not a measure of quality or box office.

## Notebooks

| Notebook | What it is |
|---|---|
| `movie_popularity_analysis.ipynb` | The enhanced analysis: research question, corrected cleaning, statistics and regression |
| `Movie Data Analysis - Netflix (1).ipynb` | My original pre-processing and visualisation notebook, kept unchanged |

## What I fixed from the original

| Issue | Effect | Fix |
|---|---|---|
| A few film overviews contain line breaks | 11 rows split into broken fragments, which made the minimum popularity look like 7.1 | Dropped rows with no valid vote count, popularity or year |
| `pd.cut` excluded the lowest edge of the first bin | The 100 films rated exactly 0.0 (all zero-vote films) became blank and were silently dropped by `dropna` | Kept ratings numeric; excluded films with under 50 votes from rating analysis, explicitly |
| Counts and most/least popular were taken after `explode` | Each film appeared once per genre | One row per film; explode only for genre summaries |
| Ratings were cut into quartiles, then counted | Quartiles hold ~25% each by design, so "most films are average" couldn't be concluded | Used the real rating distribution (median 6.6, middle half 6.0–7.2) |
| "Most films were released around 2020" | The median release year is actually 2011 | Reported the actual distribution |

## Findings

1. **Popularity is very unequal.** The median score is 21, but the top 1% of films hold 19% of all popularity. *Spider-Man: No Way Home* (5,084) leads; *The United States vs. Billie Holiday* (13.4) is lowest.
2. **Recency matters.** Median popularity rises steadily from 17 for 1960s films to 22 for the 2010s, then jumps to 35 for the 2020s (Spearman ρ = 0.26). Films from the last four years are 9% of the dataset but have more than double the median popularity of older films (48 vs 20).
3. **Rating barely matters.** Among films with 50+ votes, rating and popularity are only weakly related (ρ = 0.13). A well-rated film is not necessarily a popular one.
4. **Common is not the same as popular.** Drama is the most common genre (38% of films) but one of the least popular. Animation, Fantasy and Adventure have the highest median popularity; Documentary, History, War and Music have the highest ratings but low popularity.
5. **Most of popularity is unexplained.** Vote count alone explains 14% of the variation in (log) popularity, genre 7%, recency 7% and rating 2%. All four together explain 30%, so most of what makes a film popular at a given moment lies outside this data (marketing, trends, release timing).

## Limitations

- TMDB popularity reflects attention when the data was collected, so it favours new and trending films.
- Vote count is partly a measure of popularity itself, so its strong link is close to circular.
- The dataset only includes already-popular films, not a random sample of all films.
- These are associations, not causes.

## Tools

Python, pandas, NumPy, SciPy, statsmodels, Matplotlib, Seaborn, Jupyter.

## Run it

```bash
pip install pandas numpy scipy statsmodels matplotlib seaborn jupyter
jupyter notebook movie_popularity_analysis.ipynb
```

---

**Suwaasha Murugaperumal** · [Portfolio](https://suwaasham.github.io) · [LinkedIn](https://www.linkedin.com/in/suwaasham/) · suwaashaperumal@gmail.com
