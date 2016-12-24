<div id="#contents" ></div>

# ATP World Tour tennis data

This repository contains Python scripts that scrape tennis data from the <a href="http://www.atpworldtour.com/" target="_blank">ATP World Tour</a> website, as of Dec 2016. 

(Note: If the site layout is redesigned, then these scripts will no longer work.)

## Contents
- A. [Scraping match data by player name and by year](#part-a)
  - A1.  [The `atp_match_data_player.py` script](#part-a1)
  - A2. [Command line output](#part-a2)
  - A3. [CSV column headers](#part-a3)
- B. [Scraping match data by year](#part-b)
  - B1. [The `atp_match_data_year_no_stats.py` script](#part-b1)
  - B2. [Command line output](#part-b2)
  - B3. [CSV column headers](#part-b3)

<div id="#part-a"></div>

## A. Scraping the match data by player name and by year [^](#contents)

<div id="part-a1"></div>

### A1. The `atp_match_data_player.py` script [^](#contents)
The following Python script: 

* <a href="https://github.com/serve-and-volley/atp-world-tour-tennis-data/blob/master/python/atp_match_data_player.py" target="_blank">atp_match_data_player.py</a>

collects all of the tournament and match data for a single player in a given year from the ATP World Tour website, and exports the following example CSV file:

* <a href="https://github.com/serve-and-volley/atp-world-tour-tennis-data/blob/master/csv/players/roger-federer/roger-federer_2015.csv" target="_blank">roger-federer_2015.csv</a> (33 KB)

The Python script takes input arguments from the command line, so for this example it would be:
```shell
$ python atp_match_data_player.py "http://www.atpworldtour.com/players/roger-federer/f324/player-activity?year=2016"
```

Note that you must locate the player activity year URL:
- http://www.atpworldtour.com/players/roger-federer/f324/player-activity?year=2016

![image](https://cloud.githubusercontent.com/assets/532545/21462561/64b00504-c912-11e6-8800-854500ff0b7c.png)

The script scrapes all the match data on this page, as well as iterates through each match to find the match stats url to scrape the match stats:
- http://www.atpworldtour.com/en/players/roger-federer/F324/overview/match-stats/540/2016/R975/match-stats

![image](https://cloud.githubusercontent.com/assets/532545/21462584/a93b1d80-c912-11e6-9528-75fa64791182.png)

<div id="part-a2"></div>

### A2. Command line output [^](#contents)
In addition to the CSV output, the command line output is the following, for debugging purposes, since the ATP website is error-prone, and there are lots of inconsistencies in the ATP website HTML. These errors and inconsistencies lead to scraping errors, upon which I would have to revise the XPaths and/or the code accordingly. This console output allows me to figure out exactly which where in the site (i.e. which match) the scraper breaks down.

```shell
$ time python atp_match_data_player.py "http://www.atpworldtour.com/players/roger-federer/f324/player-activity?year=2016"
Barclays ATP World Tour Finals | Finals | Novak Djokovic
Barclays ATP World Tour Finals | Semi-Finals | Stan Wawrinka
Barclays ATP World Tour Finals | Round Robin | Kei Nishikori
Barclays ATP World Tour Finals | Round Robin | Novak Djokovic
Barclays ATP World Tour Finals | Round Robin | Tomas Berdych
ATP World Tour Masters 1000 Paris | Round of 16 | John Isner
ATP World Tour Masters 1000 Paris | Round of 32 | Andreas Seppi
Basel | Finals | Rafael Nadal
Basel | Semi-Finals | Jack Sock
Basel | Quarter-Finals | David Goffin
Basel | Round of 16 | Philipp Kohlschreiber
Basel | Round of 32 | Mikhail Kukushkin
ATP World Tour Masters 1000 Shanghai | Round of 32 | Albert Ramos-Vinolas
SUI vs. NED WG Play-Off | Round Robin | Thiemo de Bakker
SUI vs. NED WG Play-Off | Round Robin | Jesse Huta Galung
US Open | Finals | Novak Djokovic
US Open | Semi-Finals | Stan Wawrinka
US Open | Quarter-Finals | Richard Gasquet
US Open | Round of 16 | John Isner
US Open | Round of 32 | Philipp Kohlschreiber
US Open | Round of 64 | Steve Darcis
US Open | Round of 128 | Leonardo Mayer
⋮
[etc]
⋮

real	15m59.516s
user	0m19.618s
sys     0m1.259s
```

<div id="part-a3"></div>

### A3. CSV headers [^](#contents)
The following are the 99 column headers. Note that I didn't include the "tournament prize money" and "player prize money" data because of problems with outputting unicode to CSV format in my version of Python 2.7.5. I think the more recent versions of Python have rectified this problem, however updating my version of Python is non-trivial, and I don't have the time to do it right now. In any case, the unicode problem is due to the pound sterling `£` and euro `€`characters.
```
tourney_year
tourney_name
tourney_name_slug
tourney_id
tourney_location
tourney_dates
tourney_singles_draw
tourney_doubles_draw
tourney_conditions
tourney_surface
player_name
player_slug
player_id
player_event_points
player_ranking
match_round
opponent_name
opponent_name_slug
opponent_player_id
opponent_rank
match_win_loss
match_score
sets_won
sets_lost
sets_total
games_won
games_lost
games_total
tiebreaks_won
tiebreaks_lost
tiebreaks_total
match_time
match_duration
player_aces
player_double_faults
player_first_serves_in
player_first_serves_total
player_first_serve_percentage
player_first_serve_points_won
player_first_serve_points_total
player_first_serve_points_won_percentage
player_second_serve_points_won
player_second_serve_points_total
player_second_serve_points_won_percentage
player_break_points_saved
player_break_points_serve_total
player_break_points_saved_percentage
player_service_points_won
player_service_points_total
player_service_points_won_percentage
player_first_serve_return_won
player_first_serve_return_total
player_first_serve_return_percentage
player_second_serve_return_won
player_second_serve_return_total
player_second_serve_return_won_percentage
player_break_points_converted
player_break_points_return_total
player_break_points_converted_percentage
player_service_games_played
player_return_games_played
player_return_points_won
player_return_points_total
player_total_points_won
player_total_points_total
player_total_points_won_percentage
opponent_aces
opponent_double_faults
opponent_first_serves_in
opponent_first_serves_total
opponent_first_serve_percentage
opponent_first_serve_points_won
opponent_first_serve_points_total
opponent_first_serve_points_won_percentage
opponent_second_serve_points_won
opponent_second_serve_points_total
opponent_second_serve_points_won_percentage
opponent_break_points_saved
opponent_break_points_serve_total
opponent_break_points_saved_percentage
opponent_service_points_won
opponent_service_points_total
opponent_service_points_won_percentage
opponent_first_serve_return_won
opponent_first_serve_return_total
opponent_first_serve_return_percentage
opponent_second_serve_return_won
opponent_second_serve_return_total
opponent_second_serve_return_won_percentage
opponent_break_points_converted
opponent_break_points_return_total
opponent_break_points_converted_percentage
opponent_service_games_played
opponent_return_games_played
opponent_return_points_won
opponent_return_points_total
opponent_total_points_won
opponent_total_points_total
opponent_total_points_won_percentage
```

<div id="#part-b"></div>

## B. Scraping the match data by year [^](#contents)

<div id="part-b1"></div>

### B1. The `atp_match_data_year_no_stats.py` script [^](#contents)
The following Python script: 

* <a href="https://github.com/serve-and-volley/atp-world-tour-tennis-data/blob/master/python/atp_match_data_year_no_stats.py" target="_blank">atp_match_data_year_no_stats.py</a>

collects all of the tournament and match data in a given year from the ATP World Tour website (but not the individual match stats, because of runtime issues, that's for a different script), and exports the following example CSV file:
