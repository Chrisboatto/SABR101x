Let's take a look at exactly how different Run Scoring Environments can be, even within an "era" such as the Expansion Era. Write a SQL Query that draws teamID, yearID, and R/G from the Teams table. Only draw from two seasons - the low-scoring nadir of 1968, and the steroid-fueled high-scoring zenith of 2000. Order your results so that the teams with the lowest Runs/Game average are first in your result. Also, add teamID as a secondary ORDER BY condition. There should be 50 results from this query, 20 team seasons in 1968, and 30 in 2000.



**SELECT teamID, yearID, R/G**
**FROM Teams**
**WHERE yearID = 1968 OR yearID = 2000**
**ORDER BY R/G, teamID**



![image-20201224144506440](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224144506440.png)



Now, add Team Slugging Percentage to the previous query using the formula `(H+2B+2*3B+3*HR)/AB` from the Tech Track in Module 1. Label this column Team_SLG and order your results from lowest Team_SLG to highest.

**SELECT teamID, yearID, R/G, (H+2B+2*3B+3*HR)/AB AS Team_SLG**
**FROM Teams**
**WHERE yearID = 1968 OR yearID = 2000**
**ORDER BY Team_SLG**



![image-20201224144553188](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224144553188.png)



Let's now use a new SQL query to find the Teams throughout the Expansion Era that have most outperformed the Run-Scoring Environment that they played in. To do this, use the following query (added below only because it is less intuitive than many examples you have used so far) to find the outliers - the Teams that have scored the most runs compared to the League Average team in the same year.

```
SELECT 
       	SUM(R)/SUM(G) as LeagueRunAverage, 
       	yearID, 
       	(MAX(R/G))/(SUM(R)/SUM(G)) as BestOffenseRatio, 
       	SUM(R)/SUM(G)*(MAX(R/G))/(SUM(R)/SUM(G)) as BestOffenseRunAverage
FROM Teams
WHERE yearID >= 1961
GROUP BY yearID
ORDER BY BestOffenseRatio DESC
```



**SELECT** 
       	**SUM(R)/SUM(G) as LeagueRunAverage,** 
       	**yearID,** 
       	**(MAX(R/G))/(SUM(R)/SUM(G)) as BestOffenseRatio,** 
       	**SUM(R)/SUM(G)*(MAX(R/G))/(SUM(R)/SUM(G)) as BestOffenseRunAverage**
**FROM Teams**
**WHERE yearID >= 1961**
**GROUP BY yearID**
**ORDER BY BestOffenseRatio DESC**



![image-20201224144654533](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224144654533.png)



Let's modify the previous SQL query to now find the Teams throughout the Expansion Era that have most **underperformed** the Run-Scoring Environment that they played in. When modifying the query (reproduced below), change the MAX functions as necessary and relabel the relevant columns as WorstOffenseRatio and WorstOffenseRunAverage. Make sure to order your new results starting with the lowest ratio.

```
SELECT 
       	SUM(R)/SUM(G) as LeagueRunAverage, 
       	yearID, 
       	(MAX(R/G))/(SUM(R)/SUM(G)) as BestOffenseRatio, 
       	SUM(R)/SUM(G)*(MAX(R/G))/(SUM(R)/SUM(G)) as BestOffenseRunAverage
FROM Teams
WHERE yearID >= 1961
GROUP BY yearID
ORDER BY BestOffenseRatio DESC
```



**SELECT** 
       	**SUM(R)/SUM(G) as LeagueRunAverage,** 
       	**yearID,** 
       	**(MIN(R/G))/(SUM(R)/SUM(G)) as WorstOffenseRatio,** 
       	**SUM(R)/SUM(G)*(MIN(R/G))/(SUM(R)/SUM(G)) as WorstOffenseRunAverage**
**FROM Teams**
**WHERE yearID >= 1961**
**GROUP BY yearID
ORDER BY WorstOffenseRatio** 

![image-20201224144801592](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224144801592.png)



Use the query below to find the Teams in the Expansion Era that struck out the most times per game.

```
SELECT 
       	SUM(SO)/SUM(G) as LeagueKRate, 
       	(MAX(SO/G)) as HighestKRate,
        yearID 
FROM Teams
WHERE yearID >= 1961
GROUP BY yearID
ORDER BY HighestKRate DESC
```

**SELECT** 
       	**SUM(SO)/SUM(G) as LeagueKRate,** 
       	**(MAX(SO/G)) as HighestKRate,**
        **yearID**
**FROM Teams**
**WHERE yearID >= 1961**
**GROUP BY yearID**
**ORDER BY HighestKRate DESC**

![image-20201224144849832](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224144849832.png)



Now, create a metric similar to the one in the last assessment - but instead of finding the outliers with regard to Run-Scoring, we instead want to find outliers with regard to Strikeout Rate. By adding a column *after* yearID that divides the HighestKRate by the LeagueKRate (let's call this column HighestKRatio) we can find the team that struck out compared to their environment more than any other in the Expansion Era. I have reproduced the previous query below. Order your results using the DESC command so that the largest **HighestKRatio** appears first.

```
SELECT 
       	SUM(SO)/SUM(G) as LeagueKRate,  
       	(MAX(SO/G)) as HighestKRate,
        yearID
FROM Teams
WHERE yearID >= 1961
GROUP BY yearID
ORDER BY HighestKRate DESC
```



**SELECT** 
       	**SUM(SO)/SUM(G) as LeagueKRate,  
       	(MAX(SO/G)) as HighestKRate,**
        **yearID,**
        **(MAX(SO/G))/(SUM(SO)/SUM(G)) as HighestKRatio**
**FROM Teams**
**WHERE yearID >= 1961**
**GROUP BY yearID**
**ORDER BY HighestKRatio DESC**

![image-20201224144930378](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224144930378.png)