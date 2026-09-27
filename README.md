# cs418-football
## Research Question
Home-Field Advantage in Soccer - How does playing at home affect team performance and match outcomes? 

### Primary dataset 1: Premier League matches 2025/26 (Zc4466: Lu)

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
