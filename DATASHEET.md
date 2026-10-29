# DATASHEET — CS418 Football Project

Each of us adds our own part under the matching section.

## 1. Datasheets (primary datasets)

### International Football Results (Hannan)

**Source:** [martj42/international_results](https://github.com/martj42/international_results), file `results.csv`, commit `394fe81`

**Motivation:**
- The dataset was created by Mart Jurisoo, who states the reason for creating as "I was looking for a semi-definitive easy-to-read list of international football matches and couldn't find anything decent." Not documented by the publisher. 


**Composition:** 
- One row is one men’s senior international match. The size is 49,547 rows x 9 columns, and is from 30 Nov 1872 \- 26 Aug 2026, worldwide. The dataset aims to be complete, though it does exclude Olympics matches, women’s matches, and other non traditional matches. There are no empty cells, but the volume of  documented matches played before 1900 is thin. There are also no attendance, and other specific stats about the matches. 

**Collection:** 
- The dataset was collected from “Wikipedia, [rsssf.com](http://rsssf.com), and individual football associations’ websites”. The collection started in 2018, that was the first commit date. Regarding consent, these are public results about teams.

**Preprocessing:**
- Older matches use teams’ current names, for example: Ireland in 1882 is listed as Northern Ireland. Scores include extra time, but not penalty shootouts. 

**Uses:** 
- I think the main use case for this is for your own knowledge / studying, and also Kaggle notebooks. This data should not be used for women’s football, and other non traditional matches which are not a part of the dataset.

**Distribution:**
- The data file is a csv on github, and is licensed as CC0 1.0.

**Maintenance:** 
- There are 85 commits in 2026, by the creator and other contributors, showing it is updated consistently.


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


### International Football Results (Hannan)

**Question:** How much does playing at home raise a team’s chance of winning compared to a neutral venue, and does this change with match importance, and over time?

The target population is all men’s senior international matches ever played. The Access frame is the matches the creator found online and recorded. The sample is all 49,547 rows, and the time trend plot uses 1950 onward. Some of the limits include club / women’s football. Trends before 1950 are unreliable. I don’t think we can show the direct reason only based on this dataset of why home teams win more, but we can show that they win more. 

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


### International Football Results (Hannan)

| Column | Type | Meaning | Values | Source |
| :---- | :---- | :---- | :---- | :---- |
| date | Date | Match day | 1872 to 2026 | Raw |
| home\_team | String | First listed / home | 337 teams in total | Raw |
| away\_team | String | Second listed / away | 337 | Raw |
| away\_score | Int | Away goals, same rules | 0–21 | Raw |
| tournament | String | Competition name | 202 values | Raw |
| city | String | City where played | 2,093 values | Raw |
| country | String | Country where played, name at the time | 269 values | Raw |
| neutral | Boolean | TRUE if neither team is at home | TRUE 13,158 / FALSE 36,389 | Raw |
| match\_type | String | Friendly or competitive | Friendly 18,385 / Competitive 31,162 | Derived  |
| goal\_diff | Int | `Goal difference` | −21 to 31 | Derived |
| year | Int | Year of `date` | 1872–2026 | Derived  |
| result | String | Outcome for first-listed team | Win / Draw / Loss | Derived  |


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

### B. Data Preparation Recipe - Dominic Aidoo

**Step 1: Downloads & Loading**
*   **Action:** Downloaded the primary 2020/2021 match dataset (`epl_2020.csv`) from Football-Data.co.uk.
*   **Code:** `df = pd.read_csv('data/epl_2020.csv')`

**Step 2: Filters**
*   **Action:** Filtered out the irrelevant betting odds columns to keep only the features needed to evaluate home performance: `['Date', 'HomeTeam', 'AwayTeam', 'FTR', 'FTHG', 'FTAG', 'HS', 'AS', 'HST', 'AST']`. 
*   **Code:** `df = df[columns_of_interest]`

**Step 3: Type Fixes**
*   **Action:** Converted the `Date` column from a string object into a pandas datetime object.
*   **Code:** `df['Date'] = pd.to_datetime(df['Date'], dayfirst=True)`

### C. Home Vs. Away Yellow Card Analysis
**Input file:** `data/epl_2020.csv`
**Code reference:** `eda.ipynb`, "Home vs Away Yellow Card Analysis (2020/21 Premier League) - Nate Rodriguez"
1. **Acquire the raw data.** The match-level dataset is stored in `data/epl_2020.csv`.

2. **Load the CSV.** An earlier section of `eda.ipynb` loads the file into a Pandas DataFrame:
   `df = pd.read_csv("data/epl_2020.csv")`

3. **Select columns and remove missing records.** Keep only `Date`, `HY`, and `AY`, removing rows with missing values in any of these fields:
   `yellow_cards = df[["Date", "HY", "AY"]].dropna().copy()`

4. **Convert dates.** Convert `Date` column into datetime values, interpreting dates with the day first:
   `yellow_cards["Date"] = pd.to_datetime(yellow_cards["Date"], dayfirst=True)`

5. **Sort matches.** Sort by `Date` and reset the index:
   `yellow_cards = yellow_cards.sort_values("Date").reset(drop=True)`

6. **Create a derived column.** Create `Group` to assign every 20 consecutive matches to a group:
   `yellow_cards["Group"] = np.arrange(len(yellow_cards)) // 20 + 1`

7. **Aggregate the data.** Group by `Group` and calculate the average home and away yellow cards:
   `grouped = yellow_cards.groupby("Group")[["HY", "AY"]].mean()`
    
8. **Calculate overall averages.** Calculate 'home_avg', 'away_avg', and 'combined_avg' using the mean yellow-card counts.
    
9. **Joins.** No joins with secondary datasets are performed in this yellow-card analysis. Therefore, there are no join keys or matched/unmatched join counts to report.

10. **Output.** The analysis reports 380 matches, organized into 19 groups of 20 matches. The reported overall averages are 1.424 home yellow cards and 1.447 away yellow cards per match.

### International Football Results (Hannan)
Download the file: [https\://raw.githubusercontent.com/martj42/international\_results/394fe81893b062fbc2cf6257e988ac7cc4c039a1/results.csv](https://raw.githubusercontent.com/martj42/international_results/394fe81893b062fbc2cf6257e988ac7cc4c039a1/results.csv), saved as data/results.csv. Load it, and parse the date as Date which would be 49,547 x 9\. Check to see that no rows were dropped. Derive the match\_type, goal\_diff, and year. Derive result in a copy called res. Filter per plot only for example: year \>= 1950\. 
>>>>>>> 21fbecb43aa0d39166f0ae3d1ff05ccef16ea65d


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


### International Football Results (Hannan)

Findable: [https\://github.com/martj42/international\_results/blob/394fe81893b062fbc2cf6257e988ac7cc4c039a1/results.csv](https://github.com/martj42/international_results/blob/394fe81893b062fbc2cf6257e988ac7cc4c039a1/results.csv) 

Accessable: Public on github, accessed in October 2026\.

Interoperable: CSV, 3.7 MB.

Reusable: CC0 .10. 


## 6. People in the data (CARE)
### International Football Results (Hannan)
This dataset does not record individual player names, but rather records national teams. Player names only appear in goalscorers.csv, which we are not using. Though there are still some groups which could get misrepresented:

- Some under recorded countries, generally Europe and South American countries have more well documented stats.  
- Very small nations can at times give lopsided results like American Samoa’s 31-0 loss. 

The data is free and public domain, and obviously this should not be used to rank a nation's overall wealth for non football related information.
>>>>>>> 21fbecb43aa0d39166f0ae3d1ff05ccef16ea65d

### EPL 2020/2021 - Dominic Aidoo

While the dataset consists of numbers, it indirectly captures the behaviors and performances of three distinct groups of people:
*   **Players:** Represented collectively through team-level offensive metrics (Goals, Shots, Shots on Target).
*   **Referees:** Represented indirectly through the disciplinary actions they take (Home/Away Fouls and Yellow/Red Cards).
*   **Fans:** Represented contextually by comparing the empty stadium matches against normal, fully-attended seasons.

**Misrepresented Groups**
Because this dataset focuses exclusively on the English Premier League, it inherently only represents elite, male athletes competing in a highly funded European league. Using this data to make universal claims about the sport as a whole misrepresents youth leagues, women leagues, etc. 
