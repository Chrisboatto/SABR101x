

Tech: SQL Sandbox Walkthrough and First Queries



In the previous lecture, the `Describe Batting` command is shown. Now, use a similiar command, but instead - describe the `Fielding` table in you query



**Describe Fielding**

![image-20201224140717298](C:\Users\cboat\OneDrive\Documents\GitHub\Offense-Stopping--Predict\image-20201224140717298.png)





Copy and paste the following query into the textbox below. Then use the "Check" button to execute the query and look up all the batting statistics from the 2000 MLB season:

```
SELECT *
FROM Batting
WHERE yearID = 2000;

    
```

Remember that the "*" indicates that all columns from the table should be returned, and that the WHERE statement is used to filter which rows are returned.



**SELECT ***
**FROM Batting**
**WHERE yearID = 2000;**



![image-20201224141013317](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224141013317.png)



Now modify the previous query (shown again below) to instead return the batting statistics for the 1950 MLB season. (`WHERE yearID=1950`)

```
SELECT *
FROM Batting
WHERE yearID=2000;
```



**SELECT ***
**FROM Batting**
**WHERE yearID=1950;**



![image-20201224141213613](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224141213613.png)



Modify the following WHERE clause to only return the stats for the 1927 "Murderer's Row" New York Yankees (add `AND teamID = 'NYA'`)

```
SELECT *
FROM Batting
WHERE yearID = 1927;
```

**SELECT ***
**FROM Batting**
**WHERE yearID = 1927 AND teamID='NYA';**



![image-20201224141353779](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224141353779.png)



As shown in the last lecture, it is possible to create statistics using the available data in the Lahman Database. Let's try to calculate our own statistic using this method: Batting Average. Modify the SELECT clause in the following query to look like: `SELECT *, H/AB AS BA` Note the comma separating the two parts of the SELECT, and the way we use AS to name the calculated expression. The new column `BA` will be the last column (all the way to the right), so you may have to scroll in the results box to see it. This column, labeled BA, will have the Batting Averages for players on the Big Red Machine - the 1975 Cincinnati Reds.

```
SELECT *
FROM Batting
WHERE teamID = 'CIN' AND yearID = 1975 AND AB > 0
```



**SELECT *, H/AB AS BA**
**FROM Batting**
**WHERE teamID = 'CIN' AND yearID = 1975 AND AB > 0;**



![image-20201224141510224](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224141510224.png)



Now let's add a slightly more complicated statistic formula to the query. We will keep our Batting Average column (`BA`), but we will also calculate Slugging Percentage in the SELECT command, using the formula `(H+2B+2*3B+3*HR)/AB AS SLG`. The order of columns must be `*, BA, SLG`

Note: the formula for SLG is `(H+2B+2*3B+3*HR)/AB AS SLG` and not `(H+2*2B+3*3B+4*HR)/AB AS SLG` because the first component is "Hits" and not "Singles". Thus, because one Total Base is added for every 2B, 3B, and HR as part of the "Hits" component, the multipliers for 2Bs, 3Bs, and HRs are one less than the traditional value to avoid double counting.

```
SELECT *
FROM Batting
WHERE teamID = 'CIN' AND yearID = 1975 AND AB > 0;
```



**SELECT *, H/AB AS BA, (H+2B+2*3B+3*HR)/AB AS SLG**
**FROM Batting**
**WHERE teamID = 'CIN' AND yearID = 1975 AND AB > 0;**



![image-20201224141557931](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224141557931.png)



Let's use the statistics recorded in the Lahman Database to get results that resemble a classic baseball card format. Use the following query to get results that look more like a typical baseball card. Note that simple counting statistics such as `G, AB, H, 2B, 3B, HR, R, RBI, SB` are present in the database, and more complicated rate statistics like the ones calculated above - `BA, OBP, SLG` - can be calculated using the correct formulas.

```
SELECT playerID, yearID, teamID, G, AB, H, 2B, 3B, HR, R, RBI, SB,
		H/AB AS BA,
		(H+BB+HBP)/(AB+BB+HBP+SF) AS OBP,
		(H+2B+2*3B+3*HR)/AB AS SLG
FROM Batting
WHERE teamID = 'CIN' AND yearID = 1975 AND AB > 50;
```



**SELECT playerID, yearID, teamID, G,**
	**AB, H, 2B, 3B, HR, R, RBI, SB,**
	**H/AB AS BA,**
	**(H+BB+HBP)/(AB+BB+HBP+SF) AS OBP,**
	**(H+2B+2*3B+3*HR)/AB AS SLG**
**FROM Batting**
**WHERE teamID = 'CIN' AND yearID = 1975 AND AB > 50;**

![image-20201224142022855](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224142022855.png)



Finally, let's create a baseball card for the career of Johnny Bench, a key member of the 1975 Cincinnati Reds Big Red Machine. Now, we are not concerned with the teamID, yearID, or number of ABs - those stipulations can be deleted from the WHERE clause. We simply want to SELECT all the same statistics from the last query for all results in the Lahman Database where the `playerID = 'benchjo01'`. Edit the WHERE clause in the query from the last problem (duplicated below) to achieve these results.

```
SELECT playerID, yearID, teamID, G, AB, H, 2B, 3B, HR, R, RBI, SB,
		H/AB AS BA,
		(H+BB+HBP)/(AB+BB+HBP+SF) AS OBP,
		(H+2B+2*3B+3*HR)/AB AS SLG
FROM Batting
WHERE teamID = 'CIN' AND yearID = 1975 AND AB > 50;
```



**SELECT playerID, yearID, teamID, G, AB, H, 2B, 3B, HR, R, RBI, SB,
		H/AB AS BA,
		(H+BB+HBP)/(AB+BB+HBP+SF) AS OBP,
		(H+2B+2*3B+3*HR)/AB AS SLG**
**FROM Batting**
**WHERE teamID = 'CIN' AND yearID = 1975 AND AB > 50;**



![image-20201224141843025](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224141843025.png)



