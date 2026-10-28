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
### 'epl_data.csv' - Historical Premier League Statistics (Nate Rodriguez)

| Column | Data Type | Units | Meaning | Allowed Values | Missing Values | Origin |
|---|---|---|---|---|---|---|
| 'season' | Integer | Year | Starting year of the season | 1992 onward | Not yet verified | Original CSV |
| 'team_name' | String | N/A | Name of the football club | Club names | Not yet verified | Original CSV |
| 'overall_ranking' | Integer | Rank | Final league position | Positive integers | Not yet verified | Original CSV |
| 'home_matches_ranking' | Integer | Rank | Ranking based on home performance | Positive integers | Not yet verified | Original CSV | 
| 'away_matches_ranking' | Integer | Rank | Ranking based on away performance | Positive integers | Not yet verified | Original CSV |
| 'matches_played' | Integer | Matches | Number of matches played | Nonnegative integers | Not yet verified | Original CSV |
## 4. Recipe

## 5. Access & Reuse (FAIR)

### `E0.csv` — EPL 2025/26 (Lu)

- **Findable:** https://www.football-data.co.uk/englandm.php (2025/26 Premier League). Column meanings are at https://www.football-data.co.uk/notes.txt.
- **Accessible:** Free to download, no account needed. We accessed the full 2025/26 season (380 matches) on 2026-10-12. The site keeps updating this file during the season, so here is the SHA-256 of our copy: `3e3a8352f9ada6789c508d6ca184424421fed56a30400904a4a327c583407e62`.
- **Interoperable:** Plain CSV, comma-separated, dates in `dd/mm/yyyy`. It has 132 columns, but most are betting odds; we use 19 of them.
- **Reusable:** There is no formal license, but the site has a "Fair data usage policy" (https://www.football-data.co.uk/contact.php). It says the free data "is intended for private individuals only for personal betting and/or academic interest and research, via manual download or at most light (twice per week maximum) automated download. It is NOT intended for commerical [sic] or data training projects." Our class project fits this, since we downloaded the file once by hand. Because of these limits, others can reuse our code and summary numbers for academic work, but they should download the raw file from football-data.co.uk themselves, and should not use it for commercial or AI-training projects.

## 6. People in the data (CARE)
