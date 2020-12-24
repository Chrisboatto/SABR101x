We will write a SQL query that finds the players with the lowest percentage of earned runs, as a percentage of total runs. Select the following items from the pitching table:
\1. playerID
\2. ERA, calculated by taking the sum of earned runs (ER), multiplying by 9, and dividing by the sum of IP (the sum of IPOuts divided by 3).
\3. Runs allowed per 9 (aliased as RA9), calculated as in 2, but with R insead of ER.
\4. ERPercentage, defined as total ER divided by total R.

Group your results by playerID, so that each result is for one player. Include only years between 2000 and 2009 (including 2000 and 2009), and limit your results to players with at least 1000 total IP over the decade (3000 IPOuts). Order your results by ERPercentage, with the smallest first. Also, secondarily order your results by playerID.

**SELECT playerID, 9*SUM(ER)/(SUM(IPOuts)/3) AS ERA,
9*SUM(R)/(SUM(IPOuts)/3) AS RA9,**
**SUM(ER)/SUM(R) AS ERPercentage**
**FROM Pitching**
**WHERE yearID >= 2000 AND yearID < 2010**
**GROUP BY playerID**
**HAVING SUM(IPOuts) >= 3000**
**ORDER BY ERPercentage, playerID**

![image-20201224150852481](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224150852481.png)

We will write a SQL Query to determine average (slightly modified) game score for a single season. Select playerID, yearID, and GameScore from the Pitching Table, for years since (and including) 1980, for pitchers with at least 20 games started. The seasonal average game score formula we will use is:

(50*Games Started + Outs Recorded + Strikeouts - 2*Hits Allowed - 4*Earned Runs Allowed - 2*Unearned Runs Allowed (aka R-ER) - Walks Allowed + 2*(IPOuts/3 - GS*4))/GS

The last term is an adjustment designed to give pitchers two points for each inning completed after the fouth. Since we don't have game-level data, this is an adjustment that is close, but not quite equal. On average, these game scores will be higher than the real ones. Sort your results by total GameScore Descending, secondarily on playerID, and thirdly on yearID.



Note that due to the Lahman Database displaying by stint and by season, this query will be off for those pitchers who pitched for multiple teams in a year. Do not worry about that - there is no need to group by playerID and yearID.



**SELECT playerID, yearID,**
          **(50*GS + IPOuts + SO - 2*H -4*ER - 2*(R-ER) - BB + 2*(IPOuts/3 - GS*4))/GS AS GameScore**
**FROM Pitching**
**WHERE yearID >= 1980 AND GS >= 20**
**ORDER BY GameScore DESC, playerID, yearID**

![image-20201224150953148](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224150953148.png)