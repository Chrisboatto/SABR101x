Write a SQL query that selects playerID, awardID, and yearID from the AwardsPlayers Table. Refer to the [Lahman Database Documentation](http://seanlahman.com/files/database/readme2014.txt) if necessary. Don't forget that table names are case sensitive!



**SELECT playerID, awardID, yearID
          FROM AwardsPlayers**



![image-20201224142626367](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224142626367.png)



Now, modify your previous query, adding aliases that rename the awardID column as AwardName and the yearID column as Year.



**SELECT playerID, awardID AS AwardName, yearID as Year**
**FROM AwardsPlayers**



![image-20201224142730095](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224142730095.png)



Write a SQL Query that selects the playerID, Strikeouts, Walks, and HomeRuns from the Pitching table for all players in 2014. Make sure to use aliases to match the column names to the ones just listed. Refer to the [Lahman Database Documentation](http://seanlahman.com/files/database/readme2014.txt) if necessary.

**SELECT playerID, SO AS Strikeouts, BB as Walks, HR as HomeRuns
          FROM Pitching
          WHERE yearID = 2014;**

![image-20201224142847010](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224142847010.png)



Now modify your previous query, adding a new column called FIP. The formula for FIP that will we use follows. Note that the Lahman Database records Innings Pitched as IPOuts, equal to IP*3.

(3*Walks +3*Hit By Pitches + 13*Home Runs - 2*Strikeouts)/(IPOuts/3) + 3.132.


FIP stands for Fielding Independent Pitching and will be covered in Module 4.



**SELECT playerID, SO AS Strikeouts, BB as Walks, HR as HomeRuns, (3*BB + 3*HBP + 13*HR - 2*SO)/(IPOuts/3) + 3.132 AS FIP
          FROM Pitching
          WHERE yearID = 2014;**



![image-20201224142951090](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224142951090.png)



Write a SQL query that selects playerID, yearID, ERA, and Innings_Pitched from the Pitching Table for all players since (and including) 2010 with an ERA of less than 3.00 and at least 100 Innings Pitched (300 outs recorded). ERA is included in the database and does not need to be calculated manually.
Recall that the Lahman Database contains only Outs Recorded, and Innings Pitched is equal to Outs divided by 3. Refer to the [Lahman Database Documentation](http://seanlahman.com/files/database/readme2014.txt) if necessary.



**SELECT playerID, yearID, ERA, IPOuts/3 AS Innings_Pitched
          FROM Pitching
          WHERE yearID >= 2010 AND ERA < 3 AND IPOuts >= 300**



![image-20201224143108728](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224143108728.png)



Write a SQL query to find the batters who led the major leagues in [Three True Outcome Percentage ](http://www.baseball-reference.com/bullpen/Three_True_Outcomes)(BB + SO + HR)/(AB + BB + SF + SH + HBP) in 2000, for players with at least 500 At Bats. Select playerID and TTO Percentage, naming this column TTOPercentage. Be sure to include the appropriate ORDER BY clause.



**SELECT playerID, (BB + SO + HR)/(AB + BB + SF + SH + HBP) AS TTOPercentage**
**FROM Batting**
**WHERE yearID = 2000 AND AB >= 500**
**ORDER BY TTOPercentage desc**

![image-20201224143205627](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224143205627.png)



Use `DISTINCT` to get every unique `teamID` from the Teams table.



**SELECT DISTINCT teamID FROM Teams**



![image-20201224143308821](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224143308821.png)

