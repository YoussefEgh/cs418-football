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




### European Football Matches 2024/2025 (Youssef)

**Source:** [tarekmasryo/football-matches-2025-dataset, file football_matches_2024_2025.csv.](https://github.com/tarekmasryo/football-matches-2025-dataset)

**Motivation:** 
- The dataset was created by Tarek Masryo using data from the Football-Data.org API, and it was designed to provide football match results and statistics from the top five European leagues and the UEFA Champions League in one dataset, which makes it incredibly easier to analyze team performance and match outcomes across competitions. The publisher does not document any specific funding for creating the dataset.

**Composition:** 
- Each row represents one football/soccer match. The dataset contains 1,941 rows and 23 columns covering the 2024/2025 season across six competitions: Premier League, La Liga, Serie A, Bundesliga, Ligue 1, and UEFA Champions League. It covers the matches recorded for these competitions so it's every possible instance.  There are no missing values in the columns, although 2 matches have an AWARDED status and 3 matches contain unknown referee information. The dataset does not contain attendance, shots, possession, or other detailed match statistics so there are some limitations as to what we can investigate about home advantage.

**Collection:** 
- The data was collected through the Football-Data.org API, which provides s match information such as teams, scores, dates, referees, and competitions. The dataset covers all the matches played from August 2024 through May 2025, and it contains actual publicly available match records. There isn't any documented consent about the referee names.

**Preprocessing:**
- The publisher organized the API data into a CSV file and it includes the derived columns such as goal difference, total goals, match outcome, and points earned by each team. The repository also provides a data dictionary and validation scripts (which is code that checks the dataset for errors or inconsistencies, such as invalid scores or incorrect match outcomes). However, the complete original API responses are not included.

**Uses:** 
- This dataset is generally used to analyze match results and it was actually used by the creator himself to create an interactive dashboard here: https://github.com/tarekmasryo/football-matches-dashboard. However, this data should not be used to draw conclusions about other seasons or competitions that are not included in this dataset.

**Distribution:**
- The dataset is publicly available as a CSV file on GitHub and is also published on Kaggle. It is also licensed as Creative Commons Attribution 4.0 (CC BY 4.0).

**Maintenance:** 
- The repository is only maintained by Tarek himself but there are only 4 commits to it this year (2026). This is because the data is for the complete 2024/2025 season so there wouldn't be any more matches to add for the most part.


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



### European Football Matches 2024/2025 (Youssef)

**Research Question:** How does home-field advantage vary across European football competitions when comparing home-win, away-win, and draw percentages?

**Target Population:** The target population is basically all football matches played during the 2024/2025 season across the Premier League, La Liga, Serie A, Bundesliga, Ligue 1, and UEFA Champions League (for men's soccer). 

**Access Frame:** The access frame is all the football matches available through the Football-Data.org API and included in the football_matches_2024_2025.csv dataset published on GitHub. As previously stated, it includes 1,941 matches across the six competitions during the 2024/2025 season.

**Sample:** The 1,939 finished matches used in our exploratory analysis after excluding 2 awarded matches is the sample. These include 380 Premier League matches, 380 La Liga matches, 380 Serie A matches, 305 Bundesliga matches, 305 Ligue 1 matches, and 189 Champions League matches.

**Limitations:** This dataset contains only 6 competitions/leagues. They are the most competitive, but it's still not enough to generalize our findings to all football leagues or other seasons. Also, attendance numbers are not recorded in the data.


### RQ - Home vs. Away Yellow Cards (Nate Rodriguez)
**Research Question:** Do home teams receive fewer yellow cards during the 2020/21 Premier League season, when matches were largely played with spectators?

**Target population:** Premier League matches played under different home and away conditions, particularly matches played without spectators. The goal is to understand whether home teams tend to receive by home and away teams.

**Access frame:** The match-level data available in `date/epl_2020.csv`, which contains information about Premier League matches during the 2020/21 season, including match dates and yellow cards received by home and away teams.

**Sample:** The 380 Premier League matches from the 2020/21 season included in the analysis. Each match provides the number of yellow cards received by the home team (`HY`) and away team (`AY`). The matches were sorted chronologically and organized into 19 groups of 20 matches.

**Missing representation and limitations:** This analysis only examines one Premier League season and does not directly compare matches with and without spectators. Although the 2020/21 season was largely played without fans, the dataset does not include spectator attendance information. Other factors, such as referee decisions, team playing styles, fouls committed, and match intensity, may influence yellow-card totals. Therefore, the results cannot establish that the absence of spectators caused any difference in yellow cards. The findings also cannot automatically be generalized to other leagues or seasons.

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


### European Football Matches 2024/2025 (Youssef)

| Column | Data Type | Units | Meaning | Range / Allowed Values | Missing Values | Source |
|---|---|---|---|---|---|---|
| `competition_name` | String | N/A | Name of the competition | Six competitions | None | Original CSV |
| `date_utc` | Datetime | UTC date/time | Date and time of the match | Aug 15, 2024 – May 31, 2025 | None | CSV; converted in EDA notebook |
| `home_team` | String | N/A | Name of the home team | Football club names | None | Original CSV |
| `away_team` | String | N/A | Name of the away team | Football club names | None | Original CSV |
| `fulltime_home` | Integer | Goals | Goals scored by the home team | 0–9 | None | Original CSV |
| `fulltime_away` | Integer | Goals | Goals scored by the away team | 0–7 | None | Original CSV |
| `halftime_home` | Integer | Goals | Home team goals at halftime | 0–6 | None | Original CSV |
| `halftime_away` | Integer | Goals | Away team goals at halftime | 0–5 | None | Original CSV |
| `match_outcome` | String | N/A | Result of the match | Home Win, Away Win, Draw | None | Publisher-derived in CSV |
| `goal_difference` | Integer | Goals | Home goals minus away goals | -6 to +8 | None | Publisher-derived in CSV |
| `total_goals` | Integer | Goals | Total goals scored by both teams | 0–11 | None | Publisher-derived in CSV |
| `home_points` | Integer | Points | Points earned by the home team | 0, 1, 3 | None | Publisher-derived in CSV |
| `away_points` | Integer | Points | Points earned by the away team | 0, 1, 3 | None | Publisher-derived in CSV |
| `matchday` | Integer | Matchday number | Round or matchday of the competition | 0–38 | None | Original CSV |
| `stage` | String | N/A | Stage of the competition | Seven recorded stage labels, including REGULAR_SEASON | None | Original CSV |
| `status` | String | N/A | Status of the match | FINISHED, AWARDED | None | Original CSV |
| `match_id` | Integer | N/A | Unique identifier for each match | 497410–524120 | None | Original CSV |
| `referee` | String | N/A | Name of the referee | Referee names or Unknown | "Unknown" in 3 matches | Original CSV |
| `referee_id` | Integer | N/A | Identifier for the referee | -1 to 157 | -1 in 3 matches | Original CSV |
| `home_win_pct` | Float | Percentage (%) | Percentage of home wins within each competition | 0–100%; observed 38.69–50.79% | None | Calculated in EDA notebook |


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

### European Football Matches 2024/2025 (Youssef)

**Input file:** `data/football_matches_2024_2025.csv`  
**Code references:** `football_matches_2024_2025.ipynb` and `eda.ipynb`

1. **Download the dataset.** Download `football_matches_2024_2025.csv` from [GitHub](https://github.com/tarekmasryo/football-matches-2025-dataset) and save it in the `data` folder.

2. **Load the CSV.** Load the dataset containing 1,941 matches and 23 columns using:
   `df = pd.read_csv("data/football_matches_2024_2025.csv")`

3. **Check missing values and duplicates.** Use `isnull()` and `duplicated()` to check for missing values and duplicate rows. No issues were found.

4. **Remove awarded matches.** Exclude 2 awarded matches, which leaves us with 1,939 finished matches:
   `df_clean = df[df["status"] == "FINISHED"].copy()`

5. **Fix data types.** Convert `date_utc` into datetime format:
   `df_clean["date_utc"] = pd.to_datetime(df_clean["date_utc"], utc=True, errors="coerce")`

6. **Validate the data.** Check for invalid goals, points, match outcomes, and inconsistent formatting. No additional corrections were needed and three matches with unknown referee information were kept.

7. **Calculate home-win percentages.** Group matches by `competition_name` and calculate the percentage of home wins using `groupby()`.

8. **Joins.** No joins with secondary datasets were performed in my individual analysis, so there are no join keys or matched/unmatched rows to report. 

**Final output:** `df_clean` contains 1,939 finished matches and 23 columns.



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


### European Football Matches 2024/2025 (Youssef)

- **Findable:** The dataset is available on [GitHub](https://github.com/tarekmasryo/football-matches-2025-dataset/blob/main/data/football_matches_2024_2025.csv)

- **Accessible:** The CSV file can be downloaded for free without an account. It covers the 2024/2025 season. Accessed: 9/27/2026

- **Interoperable:** There are 1,941 rows and 23 columns. It can be loaded using Pandas or Polars. Dates are recorded in UTC, and the dataset includes strings and numeric values.

- **Reusable:** The publisher licenses the dataset's packaging, cleaning, and derived columns under CC BY 4.0, which allows reuse with attribution. The original match information comes from Football-Data.org, which has its own terms and requires the attribution "Football data provided by the Football-Data.org API". Our cleaning code and analysis summaries can be reused with attribution, but redistribution of the processed match-level data must also comply with the original API's terms.


## 6. People in the data (CARE)
### International Football Results (Hannan)
This dataset does not record individual player names, but rather records national teams. Player names only appear in goalscorers.csv, which we are not using. Though there are still some groups which could get misrepresented:

- Some under recorded countries, generally Europe and South American countries have more well documented stats.  
- Very small nations can at times give lopsided results like American Samoa’s 31-0 loss. 

The data is free and public domain, and obviously this should not be used to rank a nation's overall wealth for non football related information.


### European Football Matches 2024/2025 (Youssef)

This dataset mainly records football teams and match results so there aren't any individual players. 

- **Representation:** The dataset only covers men's football in five major European leagues and the Champions League during the 2024/2025 season. Women's football, lower divisions, and smaller European leagues are not represented.
- **Limitations:** Since the dataset focuses on team results, it cannot accurately measure individual player performance or explain why certain teams perform better at home. Three matches also have unknown referee information.
- **Ethical considerations:** The results should not be used to make unfair judgments about individual players, coaches, or referees. For example, a team's losses should not automatically be blamed on a particular player or referee without additional information.

So, this dataset should be used responsibly by recognizing that it only represents certain competitions and that it does not provide a complete picture of football performance.


### EPL 2020/2021 - Dominic Aidoo

While the dataset consists of numbers, it indirectly captures the behaviors and performances of three distinct groups of people:
*   **Players:** Represented collectively through team-level offensive metrics (Goals, Shots, Shots on Target).
*   **Referees:** Represented indirectly through the disciplinary actions they take (Home/Away Fouls and Yellow/Red Cards).
*   **Fans:** Represented contextually by comparing the empty stadium matches against normal, fully-attended seasons.

**Misrepresented Groups**
Because this dataset focuses exclusively on the English Premier League, it inherently only represents elite, male athletes competing in a highly funded European league. Using this data to make universal claims about the sport as a whole misrepresents youth leagues, women leagues, etc. 

