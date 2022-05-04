# MPS-SQL
SQL Portfolio

**Project 1**

**This project will be looking at a database that inclused the results of olympic games**



**in this first query I will build the base report by querying the summer_games table, querying the sport and distinct number of athletes and limiting it to the top three results**


SELECT 
	sport, 
    count (distinct athlete_id) AS athletes
FROM summer_games
GROUP BY sport
-- Only include the 3 sports with the most athletes
ORDER BY athletes desc
LIMIT 3;


