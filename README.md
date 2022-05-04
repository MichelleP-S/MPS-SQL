# MPS-SQL
SQL Portfolio

**Project 1**

**This project will be looking at a database that inclused the results of olympic games**


---


>**In this first query I will build the base report by querying the summer_games table, 
querying the sport and distinct number of athletes, group by the sport field and making the results only show 3 rows, 
with the highest athletes at the top.**


SELECT 
	sport, 
	COUNT (distinct athlete_id) AS athletes
FROM summer_games
GROUP BY sport
ORDER BY athletes desc
LIMIT 3;


>**This query shows each sport, the number of unique events, 
and the number of unique athletes from the summer_games table.
It is grouped by the non-aggregated field, which is sport.**

SELECT 
	sport, 
	COUNT (distinct event) AS events, 
	COUNT (distinct athlete_id) AS athletes
FROM summer_games
GROUP BY sport;


>**This query shows region and age of the oldest athlete, 
connects three tables by running two separate JOIN statements, 
aliasing each as the first letter in the table name.**

SELECT 
	c.region, 
	MAX(a.age) AS age_of_oldest_athlete
FROM athletes AS a
JOIN summer_games AS s
on a.id = s.athlete_id
JOIN countries AS c
ON s.country_id = c.id
GROUP BY region;


>**This query uses a UNION to combine the relevant tables, 
it shows unique events by sport for both summer and winter events and orders the query to show the highest number of events first.**

SELECT 
	s.sport, 
	COUNT(distinct s.event) AS events
FROM summer_games AS s
GROUP BY s.sport
UNION
SELECT 
	w.sport, 
	COUNT(distinct w.event) AS events
FROM winter_games AS w
GROUP BY w.sport
ORDER BY events DESC;


>**This query joins the summer_games and athletes tables to selects the athlete names and the number of gold medals won.
It only shows the athletes who won at least 3 gold medals.**

SELECT 
	a.name AS athlete_name, 
	SUM(gold) AS gold_medals
FROM summer_games AS s
JOIN athletes AS a
ON s.athlete_id	= a.id
GROUP BY athlete_name
HAVING SUM(gold) >= 3
ORDER BY gold_medals DESC;

>**This query uses a union all statement to combine the two queries 
the first shows unique events by country and season for summer events. 
The second query that shows unique events by country and season for winter events.**

SELECT 
	'summer' AS season,
	country,
	COUNT (DISTINCT event) AS events
FROM summer_games AS s
JOIN countries AS c
ON s.country_id = c.id
GROUP BY country
union all
SELECT 
	'winter' AS season, 
	country, 
	COUNT (DISTINCT event) AS events
FROM winter_games AS w
JOIN countries AS c
ON w.country_id = c.id
GROUP BY country
ORDER BY events DESC;

