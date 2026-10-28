# DATASHEET — CS418 Football Project

Each of us adds our own part under the matching section.

## 1. Datasheets (primary datasets)


## 2. Scope

### RQ3 — Home advantage with and without fans (Lu)

**Question:** Does home advantage shrink or disappear without fans, and does it come back when they return?

- **Target population:** Professional football matches played with fans vs. without fans.
- **Access frame:** The Premier League seasons we have in our files: `epl_data.csv` (2016/17–2023/24), the Premier League rows of `football_matches_2024_2025.csv` (2024/25), and `E0.csv` (2025/26).
- **Sample:** 10 EPL seasons, 380 matches each = 3,800 matches. 2020/21 is the season where most matches were played without fans.
- **What's missing and what we can't claim:**
  - Other leagues (Bundesliga, La Liga, Serie A, ...) also played without fans, but we only look at the EPL, so we can't say the same thing happened in every league.
  - The last 92 matches of 2019/20 had no fans, but `epl_data.csv` only has season totals, so we can't separate them out.
  - There is no attendance data, so we only know "fans" vs. "no fans", not how many people were there.
  - 2020/21 also had a packed schedule and almost no preseason, and a few matches still had small crowds. These could affect results too, so our data suggests home advantage was weaker that season, but it does not show that missing fans *caused* it.

## 3. Codebook
### `epl_data.csv` - Historical Premier League Statistics (Nate Rodriguez)

| Column | Data Type | Units | Meaning | Allowed Values | Missing Values | Origin |
|---|---|---|---|---|---|---|
| 'season' | Integer | Year | Starting year of the season | 1992 onward | Not yet verified | `data/epl_data.csv` |
| 'team_name' | String | N/A | Name of the football club | Club names | Not yet verified | `data/epl_data.csv` |
| 'overall_ranking' | Integer | Rank | Final league position | Positive integers | Not yet verified | `data/epl_data.csv` |
| 'home_matches_ranking' | Integer | Rank | Ranking based on home performance | Positive integers | Not yet verified | `data/epl_data.csv` | 
| 'away_matches_ranking' | Integer | Rank | Ranking based on away performance | Positive integers | Not yet verified | `data/epl_data.csv` |
| 'matches_played' | Integer | Matches | Number of matches played | Nonnegative integers | Not yet verified | `data/epl_data.csv` |

### 'epl_2020.csv - Home Vs Away Yellow Card Analysis (Nate Rodriguez)
| Column | Data Type | Units | Meaning | Allowed Values | Missing Values | Origin |
|---|---|---|---|---|---|---|
| 'Date' | Date | Calendar date | Date of the Premier League match | Valid match dates | Missing rows removed using 'dropna()' | `data/epl_2020.csv` |
| 'HY' | Numeric | Yellow cards | Number of yellow cards received by the home team | Nonnegative integers | Missing rows removed using 'dropna()' | `data/epl_2020.csv` |
| 'AY' | Numeric | Yellow cards | Number of yellow cards received by the away team | Nonnegative integers | Missing rows removed using 'dropna()' | `data/epl_2020.csv` |
| 'Group' | Integer | Group number | Sequential group of 20 matches sorted by date | 1-19 | None after creation | Derived in `eda.ipynb` |

## 4. Recipe
### Data Preparation Recipe - Nate Rodriguez
This section explains how the historical Premier League data and the 2020/21 yellow-card data are prepared for analysis.

### A. Historical Premier League Dataset

**Input file:** `data/epl_data.csv`
**Code references:** 'data_acquisition.ipynb' and `eda.ipynb`
1. **Acquire the raw data.** The historical Premier League dataset is stored in `data/epl_data.csv`. The original download source and any steps used to create this CSV must be confirmed in 'data_acquisition.ipynb'.
2. **Load the CSV.** In `eda.ipynb`, under "EDA - home advantage across 10 Premier League seasons (Lu)", the dataset is loaded using Polars:
   `history = pl.read_csv("data/epl_data.csv")`
3. **Filter by season.** The notebook selects seasons beginning in 2016 or later using:
   `history.filter(pl.col("season") >= 2016`
4. **Check match totals.** The filtered records are grouped by `season`. The minimum and maximum values of `matches_played` are calculated for each season using `group_by()` and `agg()`, then sorted by season.
5. **Check data types and missing records.** The displayed preparation code does not show explicit type conversions or dropped rows for this dataset. Any earlier cleaning must be checked in `data_acquisition.ipynb`.
6. **Joins.** No join is performed in the historical filtering and match-total validation steps shown above. If this dataset is combined with another file later in the analysis, the join keys and matched/unmatched row counts must be added here.

### Data Preparation Recipe - Dominic Aidoo

**Step 1: Downloads & Loading**
*   **Action:** Downloaded the primary 2020/2021 match dataset (`epl_2020.csv`) from Football-Data.co.uk.
*   **Code:** `df = pd.read_csv('data/epl_2020.csv')`

**Step 2: Filters**
*   **Action:** Filtered out the irrelevant betting odds columns to keep only the features needed to evaluate home performance: `['Date', 'HomeTeam', 'AwayTeam', 'FTR', 'FTHG', 'FTAG', 'HS', 'AS', 'HST', 'AST']`. 
*   **Code:** `df = df[columns_of_interest]`

**Step 3: Type Fixes**
*   **Action:** Converted the `Date` column from a string object into a pandas datetime object.
*   **Code:** `df['Date'] = pd.to_datetime(df['Date'], dayfirst=True)`


## 5. Access & Reuse (FAIR)

### `E0.csv` — EPL 2025/26 (Lu)

- **Findable:** https://www.football-data.co.uk/englandm.php (2025/26 Premier League). Column meanings are at https://www.football-data.co.uk/notes.txt.
- **Accessible:** Free to download, no account needed. We accessed the full 2025/26 season (380 matches) on 2026-10-12. The site keeps updating this file during the season, so here is the SHA-256 of our copy: `3e3a8352f9ada6789c508d6ca184424421fed56a30400904a4a327c583407e62`.
- **Interoperable:** Plain CSV, comma-separated, dates in `dd/mm/yyyy`. It has 132 columns, but most are betting odds; we use 19 of them.
- **Reusable:** There is no formal license, but the site has a "Fair data usage policy" (https://www.football-data.co.uk/contact.php). It says the free data "is intended for private individuals only for personal betting and/or academic interest and research, via manual download or at most light (twice per week maximum) automated download. It is NOT intended for commerical [sic] or data training projects." Our class project fits this, since we downloaded the file once by hand. Because of these limits, others can reuse our code and summary numbers for academic work, but they should download the raw file from football-data.co.uk themselves, and should not use it for commercial or AI-training projects.


### EPL 2020/2021 - Dominic Aidoo

*   **Findable:** [https://www.football-data.co.uk/englandm.php](https://www.football-data.co.uk/englandm.php) (Downloaded the `E0.csv` file under "Season 2020/2021").
*   **Accessible:** Accessed on September 28, 2026. It is free to download
*   **Interoperable:** `.csv` (Comma-Separated Values). 308 columns and 106 rows but most were stripped due to them been unimportant to our research question
*   **Reusable:** The data is provided for free by Football-Data.co.uk for quantitative analysis and educational use. Others may freely reuse the processed data and notebooks we are producing in this repository for educational purposes. 



## 6. People in the data (CARE)

