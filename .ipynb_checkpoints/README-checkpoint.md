# cs418-football
## Research Question
Home-Field Advantage in Soccer - How does playing at home affect team performance and match outcomes? 

### Primary dataset 1: Premier League matches 2025/26 (Lu)

I got this from football-data.co.uk (https://www.football-data.co.uk/englandm.php). The file is 'E0.csv', and the column names are explained here: https://www.football-data.co.uk/notes.txt. It's loaded in ‘data_acquisition.ipynb’.

I picked it because each row has both the home and away team's stats for the same game, so it's easy to compare home vs away.

What's in it:
- 380 rows and 132 columns, one row is one match
- the whole 2025/26 season, 20 teams, each plays 19 home and 19 away
- most of the 132 columns are betting odds, only kept 19 for now
- columns I'm using: `Date` (read in as a string, I converted it to a date), ‘HomeTeam’, ‘Away’, ‘Referee’, and ‘FTR’ (H/D/A result) are strings. Goals (‘FTHG‘/’FTAG’), shots (‘HS’/‘AS’), shots on target (‘HST’/‘AST’), corners (‘HC’/‘AC’), fouls (‘HF’/‘AF’), yellow cards (‘HY’/‘AY’) and red cards (‘HR’/‘AR’) are all ints
- no missing values in any of those
- it doesn't have possession, xG or attendance, so we'd need another source for those

Quick look: home teams won 42.6% of games vs 30.0% for away teams (27.4% draws). Home teams also scored more (1.53 vs 1.22 goals) and took more shots (13.8 vs 11.2). They got fewer yellow cards (1.67 vs 2.08) even though fouls were about the same (10.7 vs 11.0). This is just one season so I can't say much yet.

### Primary dataset 2: International football results (Hannan)
I got this dataset from: (https://github.com/martj42/international_results/blob/master/results.csv). The file is 'results.csv', and it's loaded in 'International_matches.ipynb'.

I picked this dataset because it shows the home, away, and neutral international games, and I found the neutral column to be important because it gives us extra information to look at. It also gives us a no home advantage baseline to compare real home games against, which the Premier League dataset can't do since every league game has a home team.

What's in it:

- 49,547 rows and 9 columns, and each row is a men’s international match.
- It covers 30 Nov 1872 to 26 Aug 2026 worldwide (national teams).
- 36,389 matches were played at home and 13,158 at a neutral venue.
- No missing values in any columns.
- Extra time scores are included but not penalty shootouts.
- Only the results are recorded, no attendance. 
- Columns being used: ‘date’(date), ‘home_team’, ‘away_team’, ‘tournament’, ‘city’,‘country’ (strings) , ‘home_score’ and ‘away_score’(ints), ‘neutral’(boolean).

Quick look: Home teams averaged 1.76 goals vs 1.18 away. At home venues the home team won 50.7%, and at neutral venues the team listed won 44.2%, a gap of about 6.5 points.



### Secondary dataset 1: Historical Premier League team performance (Nate)

I got this dataset from Kaggle (https://www.kaggle.com/datasets/alibakikoyuncu/tm-epl-9293-ranking?resource=download). The file is `epl_data.csv`, and it's loaded in `data_acquisition.ipynb`.

I picked it because it contains separate home and away performance statistics for Premier League teams across many seasons, so it's useful for comparing how teams perform at home vs away over time.

What's in it:
- 666 rows and 18 columns, one row represents one Premier League team's performance during one season
- covers Premier League seasons from 1992 through 2024
- columns I'm using: `season`, `team_name`, `home_matches_ranking`, `away_matches_ranking`, `home_matches_win`, `home_matches_draw`, `home_matches_lost`, `away_matches_win`, `away_matches_draw`, `away_matches_lost`, and `home_matches_pts`
- `team_name` is a string, while `season`, rankings, wins, draws, losses, points, and other match statistics are integers
- `average_age` is stored as a float
- there are no missing values in any of the 18 columns
- unlike the match-level dataset, this dataset summarizes each team's performance for an entire season rather than individual matches
- because it includes separate home and away records, we can use it to compare team performance at home vs away and examine home-field advantage across multiple Premier League seasons



### Secondary dataset 2: 2020/2021 Premier League Season Stats

I got this dataset from 'https://football-data.co.uk/englandm.php'. The data file is 'epl_2020.csv' and it is loaded in 'epl_2020.ipynb'. 

I chose this dataset because it represents the season in the premier league where there were no fans in the stadium because of the COVID pandemic. It will be interesting to compare the results from this season to recent seasons where they have been fans in the stadium. 

What's in it:
- 380 columns
- 106 rows
- Includes every single game from the 2020/2021 season including their results, goals, shots taken, shots on target, etc.
- Kept 9 of the columns as the rest seemed irrelevant