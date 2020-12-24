We will run a query to find the triple-slash stats for all MVP winners since (not including) 1990. Join the Batting table (aliased as b) with the master table (aliased on m) on playerID. Then, join the AwardsPlayers table (aliased as a) on BOTH playerID and yearID, so that the values match those of the batting table. This can be done with an AND modifier in the ON clause. Then select `CONCAT(m.nameFirst, " ", m.nameLast)` as playerName, b.yearID as Year, BA, OBP, and SLG. Recall that the formulas for BA, OBP, and SLG are H/AB, (H+BB+HBP)/(AB+BB+HBP+SF), and (H+2B+2*3B+3*HR)/AB respectively. Limit your results to those in which a.awardID is 'Most Valuable Player' and b.yearID is after 1990. Order your results by SLG from greatest to least. Then, order by b.playerID secondarily.

**SELECT CONCAT(m.nameFirst, " ", m.nameLast) AS playerName,**
  **b.yearID AS Year,** 
  **H/AB AS BA,**
  **(H+BB+HBP)/(AB+BB+HBP+SF) AS OBP,**
  **(H+2B+2*3B+3*HR)/AB AS SLG**
**FROM Batting b**
**JOIN Master m**
  **ON b.playerID = m.playerID**
**JOIN AwardsPlayers a**
**ON a.playerID = b.playerID AND a.yearID = b.yearID**
**WHERE a.awardID = 'Most Valuable Player' AND b.yearID > 1990**
**ORDER BY SLG DESC, b.playerID**

![image-20201224150422899](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224150422899.png)



We will run a query to determine which all stars also batted in the postseason. Join the BattingPost table (aliased as b, in the FROM clause) with the AllstarFull table (aliased as a) on playerID and yearID. Use the correct join to return results for ALL all stars, whether or not they played in the postseason. Select a.playerID, a.yearID, a.startingPos and postseason total bases `SUM(b.H + b.2B + 2*b.3B + 3*b.HR)` as Post_TB. Limit your results to those since (and including) 1950 (using yearID from the AllstarFull table). Group your results by playerID and yearID, to return results for one full postseason. Order your results with the largest number of postseason total bases first, secondarily by playerID, and lastly by yearID.

**SELECT a.playerID, a.yearID, a.startingPos, SUM(b.H + b.2B + 2*b.3B + 3*b.HR) AS Post_TB**
**FROM BattingPost b**
**RIGHT JOIN AllstarFull a**
**ON b.playerID = a.playerID**
**AND b.yearID = a.yearID**
**WHERE a.yearID >= 1950**
**GROUP BY playerID, yearID**
**ORDER BY Post_TB DESC, playerID, yearID**

![image-20201224150529193](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224150529193.png)