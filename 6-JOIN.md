## Questions Index

* [Ques 1](#ques-1-show-the-matchid-and-player-name-for-all-goals-scored-by-germany)

* [Ques 2](#ques-2-show-id-stadium-team1-team2-for-just-game-1012)

* [Ques 3](#ques-3-show-the-player-teamid-stadium-and-mdate-for-every-german-goal)

* [Ques 4](#ques-4-show-the-team1-team2-and-player-for-every-goal-scored-by-a-player-called-mario)

* [Ques 5](#ques-5-show-player-teamid-coach-gtime-for-all-goals-scored-in-the-first-10-minutes)

* [Ques 6](#ques-6-list-the-dates-of-the-matches-and-the-name-of-the-team-in-which-fernando-santos-was-the-team1-coach)

* [Ques 7](#ques-7-list-the-player-for-every-goal-scored-in-a-game-where-the-stadium-was-national-stadium-warsaw)

* [Ques 8](#ques-8-show-the-name-of-all-players-who-scored-a-goal-against-germany)

* [Ques 9](#ques-9-show-teamname-and-the-total-number-of-goals-scored)

* [Ques 10](#ques-10-show-the-stadium-and-the-number-of-goals-scored-in-each-stadium)

* [Ques 11](#ques-11-for-every-match-involving-pol-show-the-matchid-date-and-the-number-of-goals-scored)

* [Ques 12](#ques-12-for-every-match-where-ger-scored-show-matchid-match-date-and-the-number-of-goals-scored-by-ger)

* [Ques 13](#ques-13-list-every-match-with-the-goals-scored-by-each-team-sort-your-result-by-mdate-matchid-team1-and-team2)


### Ques 1. Show the matchid and player name for all goals scored by Germany.

```sql
SELECT matchid, player
FROM goal
WHERE teamid = 'GER'
```

### Ques 2. Show id, stadium, team1, team2 for just game 1012.

```sql
SELECT id,stadium,team1,team2
FROM game
WHERE id = 1012
```

### Ques 3. Show the player, teamid, stadium and mdate for every German goal.

```sql
SELECT player,teamid, stadium, mdate
FROM game
JOIN goal ON (id=matchid)
WHERE teamid = 'GER'
```

### Ques 4. Show the team1, team2 and player for every goal scored by a player called Mario.

```sql
SELECT team1, team2, player
FROM game
JOIN goal ON (id=matchid)
WHERE player LIKE 'Mario%'
```

### Ques 5. Show player, teamid, coach, gtime for all goals scored in the first 10 minutes.

```sql
SELECT player, teamid, coach, gtime
FROM goal
JOIN eteam ON (teamid=id)
WHERE gtime <= 10
```

### Ques 6. List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.

```sql
SELECT mdate, teamname
FROM game g
JOIN eteam e ON (g.team1 = e.id)
WHERE e.coach = 'Fernando Santos'
```

### Ques 7. List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'.

```sql
SELECT player
FROM goal g1
JOIN game g2 ON (g1.matchid = g2.id)
WHERE stadium = 'National Stadium, Warsaw'
```

### Ques 8. Show the name of all players who scored a goal against Germany.

```sql
SELECT DISTINCT player
FROM game
JOIN goal ON (id = matchid)
WHERE teamid <> 'GER' AND (team1 = 'GER' OR team2='GER')
```

### Ques 9. Show teamname and the total number of goals scored.

```sql
SELECT teamname, COUNT(teamid) AS total_goals
FROM goal
JOIN eteam ON (teamid = id)
GROUP BY teamname
ORDER BY total_goals DESC
```

### Ques 10. Show the stadium and the number of goals scored in each stadium.

```sql
SELECT stadium, COUNT(stadium) as total_goals_scored
FROM game
JOIN goal ON (id=matchid)
GROUP BY stadium
ORDER BY total_goals_scored DESC
```

### Ques 11. For every match involving 'POL', Show the matchid, date and the number of goals scored.

```sql
SELECT id, mdate, COUNT(id) as total_goals
FROM game
JOIN goal ON (id = matchid)
WHERE team1 = 'POL' or team2 = 'POL'
GROUP BY id, mdate
```

### Ques 12. For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'.

```sql
SELECT id, mdate, COUNT(id) as total_goals
FROM game
JOIN goal ON (id = matchid)
WHERE teamid = 'GER'
GROUP BY id, mdate
```

### Ques 13. List every match with the goals scored by each team. Sort your result by mdate, matchid, team1 and team2.

```sql
SELECT mdate,
       team1,
       SUM(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) score1,
       team2,
       SUM(CASE WHEN teamid=team2 THEN 1 ELSE 0 END) score2
FROM game
LEFT JOIN goal ON (id = matchid)
GROUP BY mdate, matchid, team1, team2
ORDER BY mdate, matchid, team1, team2
```
