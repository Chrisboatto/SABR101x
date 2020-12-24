Write a query that selects the playerID and Career Home Run totals from the Batting Table for each player in the Lahman Database. Call this variable Career_HR.



**SELECT playerID, SUM(HR) AS Career_HR**
**FROM Batting**
**GROUP BY playerID**



![image-20201224143449584](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224143449584.png)

Write a query that selects the playerID and Career Strikeout totals from the Batting Table for each player in the Lahman Database. Call this variable Career_SO. Sort the results so that the players with the highest strikeout totals appear first in the results.

**Furthermore, we will now introduce another component of the ORDER BY command - in case of ties in Career Strikeouts, we want to order by playerID (not descending). The way to do this is add a comma following your first ORDER BY condition (your query should be in the format of ORDER BY (condition 1), (condition 2)).**



**SELECT playerID,** 
**SUM(SO) AS Career_SO**
**FROM Batting**
**GROUP BY playerID**
**ORDER BY SUM(SO) DESC, playerID**



![image-20201224143540494](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224143540494.png)

Now, modify your query from the previous problem to only return the top 30 players in career strikeouts.



**SELECT playerID, SUM(SO) AS Career_SO**
**FROM Batting**
**GROUP BY playerID**
**ORDER BY SUM(SO) DESC, playerID**
**LIMIT 30**

![image-20201224143701800](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224143701800.png)

Now, modify your previous query to select the yearID and the number of strikeouts in the MLB for each of the 30 years in MLB history with the most total strikeouts, from the Batting Table. Call this variable League_SO. Remember to order the 30 years; the year with the most total strikeouts should appear first.



**SELECT yearID, SUM(SO) AS League_SO**
**FROM Batting**
**GROUP BY yearID**
**ORDER BY SUM(SO) DESC**
**LIMIT 30**



![image-20201224143745208](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224143745208.png)



Write a query that selects the yearID and strikeout totals from the Batting Table for the yearly leaders for each year in the Lahman Database. Call the total Leading_SO. Order the results so the most recent years are first.

**SELECT yearID, MAX(SO) AS Leading_SO**
**FROM Batting**
**GROUP BY yearID**
**ORDER BY yearID DESC**



![image-20201224143827345](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224143827345.png)



Write a query that selects the yearID and the average number of home runs for all players between 450 and 500 ABs (not including 450 and 500), for each year since and including 1950. Call this value Average_HR. ORDER the results so that the years with the greatest average home runs for these players is first. Also ORDER the results using yearID in descending order (this sub-ORDER should come second).

**SELECT yearID, AVG(HR) AS Average_HR**
**FROM Batting**
**WHERE AB > 450 AND AB < 500 AND yearID >= 1950**
**GROUP BY yearID**
**ORDER BY AVG(HR) DESC, yearID DESC**



![image-20201224143911162](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224143911162.png)