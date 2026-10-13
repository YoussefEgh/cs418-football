## Youssef

### 1 - Dataset Profiling

## Observations

The dataset contains 1,941 football matches and 23 columns across 6 competitions during the 2024/2025 season. Home teams scored an average of 1.54 goals per match, compared to 1.34 goals for away teams. Home Win was the most frequent match outcome, occurring 832 times. This suggests a possible home advantage, which we will investigate further by comparing home wins, away wins, and draws. Additionally, 1,939 matches have a FINISHED status, while 2 have another status that may need further investigation.

### 2 - Anomalies

The dataset contains no missing values across its 23 columns. There are also no duplicate rows or duplicate match IDs. Therefore, no rows needed to be removed or modified for these issues.

The dataset contains 1,939 finished matches and 2 awarded matches, both recorded as away wins. Since awarded results may not reflect normal match outcomes, I excluded these 2 matches (2 rows) from the analysis to avoid affecting the comparison between home and away wins. This leaves 1,939 matches for further analysis.

## Incorrect Data Types Observations

The date_utc column was originally stored as an object instead of a datetime type, affecting all 1,939 remaining rows. I converted it to datetime format to make it easier to analyze match results over time. All dates were converted successfully, with 0 invalid dates.

The dataset contains no negative goal values, incorrect total goals, or incorrect goal differences. There are 832 home wins, 644 away wins, and 463 draws. All match outcomes correctly match their final scores, with 0 inconsistencies found. Therefore, no corrections were needed for these values.

### Inconsistent Formatting Observations

I checked team names, competition names, match outcomes, stages, and referee names for extra spaces and repeated spaces. I also checked for capitalization differences in team names. No inconsistencies were found in these checks across the 1,939 matches, so no corrections were needed.

### Mixed Units Observations

I checked the goal and point columns for inconsistent values. All goal values are stored as integers, and there are no non-integer goals. All points use valid values of 0, 1, or 3. Additionally, no matches have halftime goals exceeding fulltime goals. No suspicious values were found in these checks, so no corrections were needed. The checks did not identify any mixed-unit issues.

### Referee ID Observations

The dataset contains 3 matches where referee_id is -1 and referee is listed as "Unknown". These values represent missing referee information. Since our research focuses on home advantage and match outcomes rather than referees, I decided to keep these 3 matches and flag the missing referee information instead of removing them.

### 3 - Distributions

Home wins were the most common match outcome, occurring 832 times, followed by 644 away wins and 463 draws. This suggests that home teams may have an advantage because they won more frequently than away teams. Further analysis is needed to understand whether this pattern is consistent across different leagues.

Home teams scored an average of 1.54 goals per match, with a median of 1 goal. The distribution is right-skewed, meaning most matches had relatively few home goals, while higher goal counts were less common. Goals ranged from 0 to 9, with only 15 matches having 6 or more home goals. Comparing this distribution with away goals can help us investigate whether playing at home is associated with better scoring performance.

Away teams scored an average of 1.34 goals per match, with a median of 1 goal. The distribution is right-skewed, meaning most away teams scored relatively few goals, while higher goal counts were less common. Goals ranged from 0 to 7, with only 10 matches having 6 or more away goals. Compared to home teams, which averaged 1.54 goals, away teams scored fewer goals on average.

The average goal difference was approximately +0.20 goals, while the median was 0. Most matches had goal differences close to zero, indicating that many matches were relatively close. Goal differences ranged from -6 to +8, with large differences being uncommon. The slightly positive average suggests that home teams generally scored more goals than away teams, which may indicate a home-field advantage.

The Premier League, La Liga, and Serie A each contain 380 matches, while the Bundesliga and Ligue 1 each contain 305 matches. The Champions League has the fewest matches, with 189. Since the competitions have different numbers of matches, comparing raw home-win counts could be misleading. Therefore, comparing home-win percentages across competitions will help us investigate whether home advantage differs between them.

## 4. Relationships Between Home-Win Percentage Across Competitions

### 5 - So What?

Home-win percentages differed across competitions, with the Champions League highest and Bundesliga lowest. This tells us that home teams don't win at the same frequency in every competition. I expected home-win percentages to vary somewhat across competitions because teams and playing conditions differ. However, I was surprised by the size of the difference, with the Champions League having the highest home-win percentage at 50.79% and the Bundesliga the lowest at 38.69%.

### 6 - What Next?

Next, I would compare home-win, away-win, and draw percentages within each competition to see whether home teams actually have a stronger advantage in certain leagues. This would help determine whether the differences in home-win percentages reflect home-field advantage or are partly explained by differences in draw rates. So, our original research question was: How does playing at home affect team performance and match outcomes? Based on these findings, I would restate our research question as: How does home-field advantage vary across European football competitions when comparing home-win, away-win, and draw percentages?

## Hannan

### 1 - Dataset Profiling

# International results (Hannan)

   I use `results.csv` (49,547 men's international matches, 1872–2026) to compare home games with
neutral-venue games.

This dataset has 49,547 rows and 9 columns, and no missing values. We can see that the scoring median is 1 goal for each side, but that is stretched by the max being 31 for home teams, and 21 for away teams. Home teams average 1.76 goals a game, compared to 1.18 for away teams. And this shows a bit of an advantage for home teams already. 

### 2 - Anomalies

The first table shows that there are 2 rows which share the same date and teams, but they have different scores, so it is probably two matches played on the same day. 

The second number: 979, shows the home matches which list a country that doesn't match the home team's name. I think we can use the neutral column to reliably check and differentiate home games from neutral ones.

The third number just shows some of the more extreme results, so there are 268 matches won by 10 or more goals.

The fourth number, 202, shows the different tournament names, which might be too many to compare, so we can group them by friendly and competitivee typee.

### 3 - Distributions

The first figure shows that most teams score between 0 and 2 goals. And the teams to most often score 0, are away times. The home teams distribution sits further to the right, with both have some high scoring games. 

The second figure shows that the goal differnce is centered just a little above 0 goals. We can also see that the shape is almost symmetrical, though we can see that th4 home teams win by more goals. 

The third figure shows that most of the matches are played in the home venue compared to a neutral venue. And we can also see that there are considerably more competetive games that friendly games.

The fourth figure shows the amount of matches played per year. We can see that there are very few matches played before the 1920s, with a lot more being played after the 1980s. There are a few dips closer to 2020, which might be explained by the pandemic.

### 4 - Relationships

The first plot shows the results by venue type, and we can see that the home team wins slightly above 50 percent of the matches, and looses only about 25 percent of them. At neutral venues the team which is listed first wins about 45 percent of the times, and looses about 30 percent of the times.

The second plot shows since 1950s team playing at home generally have won more often than first listed teams at neutral venues.

The third plot shows the home team win rate, and the average goal difference between friendly and competetive games. As we can see, in competetive games the home teams have a higher win rate vs friendly games. We can also see that the average goal difference in competetive games is noticeably higher than in friendly games.

### 5 - So What?

This is a bit interesting because i would have expected the results to be a bit more in favor of the home teams,, but the draw rate stays pretty flat.

I would have expect that moving forward,  the gap between those should shrink because travel is much easier now, but as we can see that it is actually increasing.

This makes sense to me because I would expect that in competetive games, home teams would have a more pumped up crowd  than in friendly games.

### 6 - What Next?

Next we should try to do something which can control for team strength, for example we can look at the corresponding fifa rankings.

Next, I will compare this with the Premier League data set that we chose to see how the club home advantage changed from international games.

Moving forward, we could break down the competetive games into different types, like world cup matches vs continental tournaments.

So our original research question was: How does playing at home affect team performance and match outcomes?

I think with my dataset, I would revise this to: How much does playing at home increase a team's chance of winning compared to a neutral venue, and does this advantage change with match importance over time?

Given my dataset, I would say the comparison between home and neutral venues turned out to be the clearest way to measure home advantage.

## Lu

### 1 - Dataset Profiling

*Not present in notebook.*

### 2 - Anomalies

Nate's file has one row per team per season, so first I checked that every team played 38 games.

2024 only has 19-20 games per team (looks like it was scraped mid season), so I left it out and used Youssef's full 2024/25 season instead.

Youssef's data writes results as "Home Win" etc., so I changed it to H / D / A like `E0.csv` so both can go through the same function. For Nate's data, adding up `home_matches_draw` gives the number of drawn matches since each match has one home team.

| anomaly | rows affected | what I did |
|---|---|---|
| `epl_data.csv` 2024 season is only half a season (199 matches instead of 380) | 20 rows | left out, used Youssef's 2024/25 instead |
| season and result are coded differently in each file | all rows | made one `season` column (start year) and changed results to H / D / A |
| 2019/20 has 92 no-fans matches inside the season total | 92 matches | flagged, can't split them with season totals |

I also checked 2020/21 against Dominic's match-by-match `epl_2020.csv` and got the same counts (144 / 83 / 153).

### 3 - Distributions

*Not present in notebook.*

### 4 - Relationships

# EDA - home advantage across 10 Premier League seasons (Lu)

I use Nate's `epl_data.csv` for 2016/17-2023/24, Youssef's `football_matches_2024_2025.csv` for 2024/25 and my `E0.csv` for 2025/26.

Each point is one full season (380 matches). The grey band is 2020/21, played without fans.

### 5 - So What?

**So what?** In 9 of 10 seasons home teams won more than away teams (home win about 41-49%, away win about 28-35%). 2020/21 is the only season where the lines cross: away teams won 40.3% and home teams 37.9%. Once fans came back home wins went up again (42.9% in 2021/22, 48.4% in 2022/23), which fits the idea that fans are part of home advantage.

**Expected?** Partly. I expected home advantage to shrink without fans, but not to flip. Seasons with fans also move around more than I thought (40.8% in 2024/25 vs 48.4% in 2022/23).

### 6 - What Next?

**What next?** 2020/21 was weird in other ways too (packed schedule, no preseason), so this doesn't prove fans cause it; comparing other leagues that played without fans would help. The last 92 matches of 2019/20 were also behind closed doors but are hidden in Nate's season totals. Also, Dominic's and my files have cards and fouls, so I want to check if referees treated home teams differently without fans.

**Revised question:** does home advantage shrink or disappear without fans, and does it come back when they return?

## Dominic

### Distributions:

## Feature Distributions: Visualizing the Home Advantage (Dominic)

To understand the baseline home advantage, we need to look at the distribution of our primary features: Match Outcomes, Goals Scored, and Shot Generation.

**Description: Match Outcomes (FTR) - 2020 "Ghost Games" Season**
* **Center (Mode):** The mode of this distribution is 'A' (Away Win), which is unusual for a standard soccer season.
* **Spread:** Away wins are the most frequent outcome, followed closely by Home wins ('H'), with Draws ('D') being the least common.
* **Takeaway:** This inverted distribution shows our primary research question. During the 2020 season played without fans in the stadiums, the traditional "home-field advantage" disappeared, resulting in a higher rate of away victories.

**Description: Goals Scored (FTHG vs FTAG) **
* **Shape & Skew:** This distributions is heavily right-skewed. The bulk of the data falls between 0 and 2 goals.
* **Center:** Unlike a normal season, the distributions are nearly identical with massive overlap. The mean for Home Goals is *not* visibly shifted higher; in fact, Away teams scored 2 and 3 goals more frequently than Home teams in this dataset. 
* **Spread:** The vast majority of team performances result in 0 to 3 goals.
* **Outliers:** There is a long right tail containing outliers for both sides, representing rare blowout matches where a team scores 4 to 8 goals.
* **Takeaway:** The lack of a distinct, right-shifted scoring advantage for the home team  aligns with the inverted match outcomes in the previous plot, showing how the absence of fans neutralized the home offensive advantage.

**Description: Shot Generation (HS vs AS)**
* **Shape & Skew:** Both distributions are slightly right-skewed but resemble a more normal, bell-shaped distribution compared to actual goals scored. 
* **Center:** The median number of shots for the Home team is slightly higher compared to the Away team. 
* **Spread :** The middle 50% of home performances generate significantly more offensive pressure than away performances.
* **Outliers:** Both distributions feature upper-bound outliers, representing extreme anomalies where a team registers an unusually high number of shots in a single match.



## Nate

### 4 - Relationships

## Home vs Away Yellow Card Analysis (2020/21 Premier League) - Nate Rodriguez

This analysis examines differences in yellow cards received by home and away teams during the 2020/21 Premier League season. Matches are grouped into sets of 20 to compare average yellow cards throughout the season and investigate whether playing at home is associated with disciplinary outcomes.

### 5 - So What?

**So what?** 
This graph compares the average yellow cards received by home and away teams throughout the 2020/21 Premier League season. Each group represents 20 matches. Home teams average 1.424 yellow cards per match, while away teams average 1.447. The difference is very small, suggesting that playing at home did not have a strong association with the number of yellow cards received during this season. Although the averages fluctuate between match groups, neither home nor away teams consistently received more yellow cards.

**Expected?** 
We expected away teams to receive more yellow cards because home-field advantage could influence referee decisions and disciplinary outcomes. However, the results were somewhat unexpected because the difference between home and away teams was very small. This suggests that yellow-card totals alone may not provide strong enough evidence of home-field advantage during the 2020/21 season.

### 6 - What Next?

Next, we could compare yellow-card averages across multiple Premier League seasons to determine whether the relationship changes when spectators are present. We could also examine the number of fouls committed by home and away teams to see whether differences in yellow cards are related to fouls rather than home-field advantage. This would help us better understand whether playing at home is associated with referee decisions
