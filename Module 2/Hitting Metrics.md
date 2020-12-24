As a fun exercise, let's execute a SQL query using the Lahman Database that allows us to see the wOBA leaders in the 1998 MLB Season. Don't worry if some elements of the query are unfamiliar, these will be taught in the upcoming TECH tracks in the Module. Simply copy and paste the following query to see who the wOBA Linear Weights system believes to be the best hitters in the 1998 campaign.

Note: if you wanted to find the wOBA leaderboard for a different season, you would not only need to change the yearID component of the WHERE clause, you would also need to change the wOBA constants in the equation given in this query. The constants shown are those of the 1998 season, constants for every other season are located at [Fangraphs](http://www.fangraphs.com/guts.aspx?type=cn). Feel free to play around with this query in the Ungraded SQL Sandbox as you become more comfortable with SQL throughout this Module and course.

```
SELECT playerID, 
      	yearID, 
      	teamID, 
      	(0.713*(BB-IBB) + 0.742*HBP + 0.898*(H-2B-3B-HR) + 1.257*2B + 1.580*3B + 2.007*HR) / (AB + BB - IBB + SF + HBP) AS wOBA
FROM Batting
WHERE yearID = 1998 AND AB > 300
ORDER BY wOBA DESC
```



**SELECT playerID,** 
      	**yearID,** 
      	**teamID,** 
      	**(0.713*(BB-IBB) + 0.742*HBP + 0.898*(H-2B-3B-HR) + 1.257*2B + 1.580*3B + 2.007*HR) / (AB + BB - IBB + SF + HBP) AS wOBA**
**FROM Batting**
**WHERE yearID = 1998 AND AB > 300**
**ORDER BY wOBA DESC**

![image-20201224142356440](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224142356440.png)