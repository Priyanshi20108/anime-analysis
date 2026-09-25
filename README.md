
The notebook parses this into clean, typed columns and then analyzes:

- Whether episode count or duration predicts score
- How popularity (member count) relates to score and rank
- The distribution of scores across the top 50
- Average score by format (TV, Movie, OVA, Special)

## Dataset

`anime.csv` — 50 rows, 3 raw columns (`Rank`, `Title`, `Score`), sourced from a scraped anime ranking page. The `Title` field packs in the series name, format, episode count, air dates, member count, and (for some titles) a manga-store preview price.

## Columns produced by the notebook

| Column | Description |
|---|---|
| `Rank` | Original ranking position |
| `Score` | User rating (out of 10) |
| `Name` | Series title, parsed out of `Title` |
| `Type` | Format: TV, Movie, OVA, ONA, Special, or Music |
| `episodes` | Number of episodes |
| `Total time` | Raw air-date range string |
| `duration_months` | Airing duration in months, computed from the date range |
| `members` | Number of members who have the title on their list |
| `Preview` | Manga-store preview price in €, where available (14 of 50 rows) |

## Key findings

- **Rank is essentially a direct function of Score** (correlation ≈ -0.99).
- **Episode count and airing duration have little relationship with score** (correlations of ≈0.26 and ≈0.23) — long-running titles like *Gintama* (201 eps) and *Hunter x Hunter* (148 eps) score just as well as short ones.
- **Popularity (members) only weakly correlates with score** (≈0.20) within this top-50 slice — once a title is already elite, being more widely watched doesn't predict a higher rating.
- **Scores are tightly clustered** (8.71–9.10, mean 8.88) — expected, since this is only the top 50 rather than a representative sample of all anime.
- **Differences in average score by Type are small** and partly an artifact of uneven group sizes (38 TV titles vs. a single Special).
- **`Preview` price data is partial** (14 of 50 rows) and reflects merchandise listings, not a property of the anime itself, so conclusions from it are limited.

## Tools

- Python
- pandas
- numpy
- matplotlib
- seaborn

## Visualizations

- Scatter plot: episodes vs. score (bubble size = members)
- Correlation heatmap: members, score, rank
- Histogram: score distribution
- Bar chart: average score by type

## How to run

1. Clone the repo and make sure `anime.csv` is in the same directory as the notebook.
2. Install dependencies:
