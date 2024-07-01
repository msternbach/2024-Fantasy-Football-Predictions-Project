# 2024-Fantasy-Football-Predictions-Project

### Tableau Visualization:
https://public.tableau.com/app/profile/michael.sternbach/viz/FantasyFootballVisualization/Dashboard1

### Project Code: 


## Summary

The goal of this project was to build a machining learning model that could predict a player's performance better than "experts" on sites like ESPN and NFL.com. It started as a group project for our data science class, and then something that I and some of my other
groupmates kept working on after graduation. After trying out many different variables and techniques I was able to build an optimal model for each position group given our availble data. The models for rookie performance were a bit unreliable as there is no statistical data that could be used, but they were still overall pretty good at predicting who would be the top 3/5 performing rookies per position. However the veteran models all had RMSE and R squared values ranging from 55 - 75 and 0.5 - 0.63 respectively. They were also reliable in predicting which players would finish in the top 20 with that accuracy ranging from 60% - 80%, which is very impressive considering many of the incorrect predictions were due to unforseen injuries. The predictions for the 2024 season are by no means perfect, but it does give you a good estimate of around where a player will perform, and can absolutely be used as a valuable tool when it comes to drafting a fantasy team.

## Data collection
### Statistical Data
*Collected by: Michael Sternbach*

This data contains all the statistical information we used. It was collected from [nfl verse](https://github.com/nflverse/nflverse-data/releases/tag/player_stats)

|player_id |player_name             |position|recent_team|season|games_played|completions|attempts|passing_yards|passing_tds|interceptions|sacks|sack_yards|sack_fumbles|sack_fumbles_lost|passing_air_yards|passing_yards_after_catch|passing_first_downs|passing_epa |passing_2pt_conversions|pacr       |dakota      |carries|rushing_yards|rushing_tds|rushing_fumbles|rushing_fumbles_lost|rushing_first_downs|rushing_epa |rushing_2pt_conversions|receptions|targets|receiving_yards|receiving_tds|receiving_fumbles|receiving_fumbles_lost|receiving_air_yards|receiving_yards_after_catch|receiving_first_downs|receiving_epa|receiving_2pt_conversions|racr        |target_share|air_yards_share|wopr        |special_teams_tds|fantasy_points|fantasy_points_ppr|
|----------|------------------------|--------|-----------|------|------------|-----------|--------|-------------|-----------|-------------|-----|----------|------------|-----------------|-----------------|-------------------------|-------------------|------------|-----------------------|-----------|------------|-------|-------------|-----------|---------------|--------------------|-------------------|------------|-----------------------|----------|-------|---------------|-------------|-----------------|----------------------|-------------------|---------------------------|---------------------|-------------|-------------------------|------------|------------|---------------|------------|-----------------|--------------|------------------|
|00-0000104|Troy Aikman             |QB      |DAL        |1999  |14          |258        |430     |2920         |17         |11           |19   |130       |5           |1                |0                |0                        |124                |36.24471432 |0                      |0          |1.32621242  |21     |10           |1          |2              |0                   |3                  |-8.846873051|0                      |0         |0      |0              |0            |0                |0                     |0                  |0                          |0                    |NULL         |0                        |NULL        |NULL        |NULL           |NULL        |0                |167.8         |167.8             |
|00-0000104|Troy Aikman             |QB      |DAL        |2000  |11          |153        |259     |1616         |7          |14           |13   |91        |2           |2                |0                |0                        |81                 |-29.087924  |1                      |0          |0.99540348  |10     |13           |0          |0              |0                   |5                  |-2.118868183|0                      |0         |0      |0              |0            |0                |0                     |0                  |0                          |0                    |NULL         |0                        |NULL        |NULL        |NULL           |NULL        |0                |63.94         |63.94             |
|00-0000145|Derrick Alexander       |WR      |KC         |1999  |16          |0          |0       |0            |0          |0            |0    |0         |0           |0                |0                |0                        |0                  |NULL        |0                      |NULL       |NULL        |2      |82           |1          |0              |0                   |1                  |5.45365649  |0                      |54        |103    |832            |2            |0                |0                     |0                  |0                          |31                   |22.726649    |0                        |0           |0.216717289 |NULL           |NULL        |0                |109.4         |163.4             |
|00-0000145|Derrick Alexander       |WR      |KC         |2000  |15          |0          |0       |0            |0          |0            |0    |0         |0           |0                |0                |0                        |0                  |NULL        |0                      |NULL       |NULL        |3      |45           |0          |0              |0                   |2                  |1.518605682 |0                      |72        |134    |1265           |9            |0                |0                     |0                  |0                          |51                   |36.46909667  |0                        |0           |0.253857667 |NULL           |NULL        |0                |185           |257               |
|00-0000145|Derrick Alexander       |WR      |KC         |2001  |13          |0          |0       |0            |0          |0            |0    |0         |0           |0                |0                |0                        |0                  |NULL        |0                      |NULL       |NULL        |2      |16           |0          |0              |0                   |1                  |0.731802382 |0                      |27        |68     |470            |3            |0                |0                     |0                  |0                          |22                   |2.118592931  |0                        |0           |0.163619062 |NULL           |NULL        |0                |66.6          |93.6              |

### Depth Chart Data
*Collected by: Michael Sternbach*

This data contains where each player was on the depth chart week 1 of every season.

Most of the data came from [nfl verse](https://github.com/nflverse/nflverse-data/releases/tag/depth_charts) while the rest was manually collected using pro football reference and espn.

|season    |club_code               |depth_team|player_id|position|depth_position|player_name|
|----------|------------------------|---|---|----|---|---|
|2024      |ARI                     |2  |00-0032398|WR  |WR |Chris Moore|
|2024      |ARI                     |2  |00-0038122|QB  |QB |Desmond Ridder|
|2024      |ARI                     |2  |00-0035500|WR  |WR |Greg Dortch|
|2024      |ARI                     |1  |00-0033553|RB  |RB |James Conner|
|2024      |ARI                     |1  |00-0035228|QB  |QB |Kyler Murray|


### Demographic Information
*Collected by: Alex Szczepanski*

This data sought to pull the height, weight, college, high school, high school state, place of birth, draft team, draft number/round, draft year, and birthday of every player in the dataset.

The data was from pro football reference collected using Selenium and BeautifulSoup in Python. The code used for this can be found [here](https://github.com/aszczep1/Fantasy_Football_Project/blob/main/Scrape_Info/Clean_Scraping_File.ipynb).

|player_name|feet                    |inches|weight(lbs.)|college|high_school_name|high_school_state|draft_team        |draft_info                                                                      |birthday  |
|-----------|------------------------|------|------------|-------|----------------|-----------------|------------------|--------------------------------------------------------------------------------|----------|
|Jared Goff |6                       |4     |217lb       |California|Marin Catholic  |CA               |Los Angeles Rams  |Draft: Los Angeles Rams in the 1st round (1st overall) of the 2016 NFL Draft.   |10/14/1994|
|Evan Engram|6                       |3     |240lb       |Mississippi|Hillgrove       |GA               |New York Giants   |Draft: New York Giants in the 1st round (23rd overall) of the 2017 NFL Draft.   |9/2/1994  |
|Shane Matthews|6                       |3     |196lb       |Florida|Pascagoula      |MS               |                  |                                                                                |6/1/1970  |
|Alec Pierce|6                       |3     |211lb       |Cincinnati|Glenbard West   |IL               |Indianapolis Colts|Draft: Indianapolis Colts in the 2nd round (53rd overall) of the 2022 NFL Draft.|5/2/2000  |
|Jared Cook |6                       |5     |246lb       |South Carolina|North Gwinnett  |GA               |Tennessee Titans  |Draft: Tennessee Titans in the 3rd round (89th overall) of the 2009 NFL Draft.  |4/7/1987  |


### Injury Data
*Collected by: Maggie Conners, Brett Gaebel, Conor Hughes, Michael Leahey, Michael Sternbach, and Alex Szczepanski*

This data collection sought to pull information on if the player was injured the prior season, injury type, injury severity, and if it was season-ending.

The data was collected by manually searching the internet and using various resources like Draft Sharks, Rotowire, Wikipedia, and other news outlets.

### Coaching Data
*Collected by: Conor Hughes*

This data contains the coach's name, team, season, first year with the team or not, years coached, wins, losses, and ties.

The data was manually collected from Wikipedia.

|coach_name|recent_team             |season|firstyearwithteam|years_coached|wins|loses|ties              |
|----------|------------------------|---|---|----|---|---|------------------|
|VinceTobin|ARI                     |1998|0  |2   |9  |7  |0                 |
|VinceTobin|ARI                     |1999|0  |3   |6  |10 |0                 |
|VinceTobin|ARI                     |2000|0  |4   |3  |13 |0                 |
|DaveMcGinnis|ARI                     |2001|1  |0   |7  |9  |0                 |
|DaveMcGinnis|ARI                     |2002|0  |1   |5  |11 |0                 |

## Data Preprocessing
*Conducted by: Michael Sternbach*
- Creating new variables:
  - New team
  - Quarterback has over 4000 passing yards
  - Running back has over 1000 rushing yards
  - Receiver has over 1000 receiving yards
  - Fantasy points per game over previous 3 seasons
- Merging datasets
- Binning height, weight, and draft round
- Handling undrafted players
- Handling injury data
- Correlation analysis
