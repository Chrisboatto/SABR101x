Write a query that selects teamID, yearID, Wins (W), Pythagorean Predicted Wins (predictedW), and Pythagorean Error (Error) from the teams table. Include only results for the Dodgers (teamID `LAN`) for years since and including 1980 and order your results with the greatest positive error first. Remember that pythagorean winning *percentage* is equal to R*R/(R*R + RA*RA) and error is equal to predicted wins minus actual wins. Put games (not W+L) in the front of your multiplication in calculating predicted wins and errors to avoid issues with the SQL Sandbox grader.

**SELECT teamID,**
**yearID,**
**W,** 
**G*(R*R)/(R*R + RA*RA) AS predictedW,**
**(G*(R*R)/(R*R + RA*RA) - W) AS Error**
**FROM Teams**
**WHERE teamID = 'LAN' AND yearID >= 1980**
**ORDER BY Error DESC**

![image-20201224145609318](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224145609318.png)



Modify the nested select query from the previous video to select the w.yearID, MINError, MAXError, STDError for all Pythagorean win predictions from 1955 onwards (do not use the `ABS` function for any of these). Recall that (R*R)/(R*R + RA*RA) is the formula for pythagorean win *percentage*, and error is defined as pythagorean wins minus actual wins. Order by the highest standard deviation (using the STDDEV function). ROUND your standard deviation to three decimal places using the ROUND function i.e. `ROUND(STDDEV(...),3)`

We can see from the MINError and MAXError that in some cases, teams greatly over- or under-perform Bill James's Pythagorean prediction. To get the grader to accept your answer as correct, please multiply by games at the *beginning* of your predicted win and error formulas.

**SELECT w.yearID, MIN(w.Error) AS MINError, MAX(w.Error) AS MAXError, ROUND(STDDEV(w.Error),3) AS STDError**
**FROM (**
     **SELECT teamID, yearID, W,**
        **G*(R*R)/(R*R + RA*RA) AS predictedW,**
        **(G*(R*R)/(R*R + RA*RA) - W) AS Error**
     **FROM Teams**
     **WHERE yearID >= 1955**
     **) w**
**GROUP BY w.yearID**
**ORDER BY STDError DESC**

![image-20201224145715973](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224145715973.png)

Write a query that selects ERA and FIP `(3*BB + 3*HBP + 13*HR - 2*SO)/(IPOuts/3) + 3.139` from the pitching table for all pitchers on the 1998 Braves (teamID = `ATL`) with at least 10 games started. Order your results by ERA-FIP, with the largest positive differential first.

**SELECT ERA, (-2*SO + 3*BB + 3*HBP + 13*HR)/(IPOuts/3) + 3.139 AS FIP**
**FROM Pitching**
**WHERE teamID = 'ATL' AND yearID = 1998 AND GS >= 10**
**ORDER BY (ERA - FIP) DESC**

![image-20201224145758612](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224145758612.png)

Modify your last query, selecting the same columns with the same ordering, plus yearID as column 2, but for all Pedro Martinez seasons. Do this by searching for his NameLast and NameFirst, not by searching for his playerID.

**SELECT CONCAT(m.NameFirst, ' ', m.NameLast) AS Name, yearID, ERA, (-2*SO + 3*HBP + 3*BB + 13*HR)/(IPOuts/3) + 3.139 AS FIP**
**FROM Pitching p**
**JOIN Master m**
**ON m.playerID = p.playerID**
**WHERE NameFirst = 'Pedro' AND NameLast = 'Martinez'**
**ORDER BY (ERA - FIP) DESC**

![image-20201224145841220](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224145841220.png)

Write a query that joins the batting table (aliased as b) with the pitching table (aliased as p) on playerID, yearID, and stint. Then, group by yearID to get league numbers for players who pitched. Use aggregate functions to select b.yearID, total hits for pitchers as Total_H, total at bats for pitchers as Total_AB, and league batting average for pitchers as League_AVG. When calculating league batting average, be sure to divide *total* hits by *total* at bats. Order your results with the highest league batting average for pitchers first. Secondarily, order your results by yearID.

**SELECT b.yearID, SUM(b.H) AS Total_H, SUM(b.AB) AS Total_AB, SUM(b.H)/SUM(b.AB) AS League_AVG**
**FROM Batting b JOIN Pitching p**
**ON b.playerID = p.playerID AND**
**b.yearID = p.yearID AND**
**b.stint = p.stint**
**GROUP BY yearID**
**ORDER BY League_AVG DESC, yearID**

![image-20201224145933092](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224145933092.png)

Write a query that selects yearID, teamID, and total payroll by team-season from the Salaries table, as Payroll. Note that since the Salaries table is by player, you will need to use a `GROUP BY` to ensure that each row in the result contains one season from one team. Order your results by yearID, and then by teamID. It is NOT necessary to use a join to solve this problem.

**SELECT yearID, teamID, SUM(salary) AS Payroll**
**FROM Salaries**
**GROUP BY yearID, teamID**

![image-20201224150133328](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224150133328.png)

Now, use the query from the above problem to join the Teams table (aliased as t) to the table the is the result of the above query (aliased as s), on teamID and yearID. Select yearID, teamID, and attendance from Teams, and Payroll from the derived table (s). Also select attendance per payroll dollar, as FansPerDollar. Order your result so that the team with the fewest fans per dollar is first.

**SELECT t.yearID, t.teamID, t.attendance, s.Payroll, t.attendance/s.Payroll AS FansPerDollar**
**FROM Teams t**
**JOIN (**
     **SELECT yearID, teamID, SUM(salary) AS Payroll**
     **FROM Salaries**
     **GROUP BY yearID, teamID**
     **) s**
**ON t.yearID = s.yearID**
  **AND t.teamID = s.teamID**
**ORDER BY FansPerDollar** 

![image-20201224150215283](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224150215283.png)

Join the Pitching (aliased as p) table to the Master table (aliased as m). Return results for all players from Venezuela `m.BirthCountry = "Venezuela"`, with more than 60 IP on the season. Select a player's full name (use the CONCAT funciton to combine first name, a space, and last name) as playerName, m.BirthCountry as Country, p.yearID as Year, Innings Pitched as IP, p.ERA as ERA, and (3*BB + 3*HBP + 13*HR - 2*SO)/IP + 3.2 as FIP. Remember that in the Lahman database, IP is stored as IPOuts, and IP = IPOuts/3.

**SELECT CONCAT(m.nameFirst, ' ', m.nameLast) AS playerName, m.BirthCountry AS Country,**
          **p.yearID AS Year, p.IPOuts/3 AS IP, p.ERA AS ERA, (3*BB + 3*HBP + 13*HR - 2*SO)/(IPOuts/3) + 3.2 AS FIP**
**FROM Pitching p**
**JOIN Master m**
**ON p.playerID = m.playerID**
**WHERE m.BirthCountry = "Venezuela" AND p.IPOuts > 180**

![image-20201224150303821](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224150303821.png)