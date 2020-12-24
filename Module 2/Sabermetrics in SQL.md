Write a query that selects the playerID, Batting Average, On-Base Percentage `(H+BB+HBP)/(AB+BB+HBP+SF)`, and Slugging Percentage `((H+2B+2*3B+3*HR)/AB)` for all members of the 2001 Seattle Mariners (teamID `SEA`) with 100 at bats or more. Call the 3 stats BA, OBP, and SLG. Order the results by OPS (OBP plus SLG), with the highest first.

**SELECT playerID,**
**H/AB AS BA,**
**(H+BB+HBP)/(AB+BB+HBP+SF) AS OBP,** 
**(H+2B+2*3B+3*HR)/AB AS SLG**
**FROM Batting**
**WHERE teamID = 'SEA' AND yearID = 2001 AND AB >= 100**
**ORDER BY OBP + SLG DESC**



![image-20201224144028278](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224144028278.png)



Write a query that selects from the Batting Table. Using a `GROUP BY` and a `HAVING` command, select the teamID, yearID, and home run total of the team's leader (Leading_HR) for all team-seasons whose leading home run hitter hit at least 45 home runs. Order the results by Leading_HR, from greatest to least. THEN order your results by yearID, secondarily (not descending). Lastly, order by teamID, not descending. Be sure, using your `GROUP BY`, that each row in the results corresponds to one team for one season.



**SELECT teamID, yearID, MAX(HR) AS Leading_HR**
**FROM Batting**
**GROUP BY teamID, yearID**
**HAVING MAX(HR) >= 45**
**ORDER BY MAX(HR) DESC, yearID, teamID**

![image-20201224144113633](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224144113633.png)

Modify your query from the first problem of this track, from the 2001 Mariners, adding an additional column for On-Base plus Slugging (OPS). Order by OPS, from least to greatest.

**SELECT playerID,**
**H/AB AS BA,**
**(H+BB+HBP)/(AB+BB+HBP+SF) AS OBP,** 
**(H+2B+2*3B+3*HR)/AB AS SLG,**
**(H+BB+HBP)/(AB+BB+HBP+SF) + (H+2B+2*3B+3*HR)/AB AS OPS**
**FROM Batting**
**WHERE teamID = 'SEA' AND yearID = 2001 AND AB >= 100**
**ORDER BY (H+BB+HBP)/(AB+BB+HBP+SF) + (H+2B+2*3B+3*HR)/AB**

![image-20201224144156634](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224144156634.png)



Write a SQL Query that uses a nested select statement to select from the Pitching Table the playerID, yearID, teamID, and K_Minus_BB (Strikeouts minus Walks divided by Batters Faced) for all pitcher seasons since and including 1990 that have a larger K-BB% than Clayton Kershaw's `kershcl01` in 2014. Limit your results to pitchers with at least 150 innings pitched (450 outs recorded). Order your results By K-BB%, from greatest to least.



**SELECT playerID,**
**yearID,**
**teamID,**
**(SO - BB)/BFP AS K_Minus_BB**
**FROM Pitching**
**WHERE IPOuts >= 450 AND yearID >= 1990**
**HAVING K_Minus_BB > (SELECT (SO-BB)/BFP**
**FROM Pitching**
**WHERE yearID = 2014 AND playerID = 'kershcl01')**
**ORDER BY (SO-BB)/BFP DESC**

![image-20201224144256731](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224144256731.png)

