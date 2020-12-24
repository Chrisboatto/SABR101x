Let's use the BU SQL Sandbox to investigate the topic of Win Percentage throughout baseball history. Write a query that Selects teamID, yearID, Wins, Losses, Winning Percentage (W/(W+L)), Runs Scored, Runs Allowed, Run Differential (R - RA), and Run Differential Per Game ((R - RA)/G). Alias the Winning Percentage term as Winning_Percentage, the Run Differential term as Run_Differential, and the Run Differential Per Game as Run_Diff_Per_Game. Select this information from the Teams table. Make sure that your results only come from years after (and including) 1901 - the Modern Era. Furthermore, only select teams with Winning_Percentage greater than 70% (.700). You should order your results to start with the Highest Single Season Winning Percentage in the Modern Era. Additionally, add teamID and yearID as the 2nd and 3rd parts of your ORDER BY command (don't use ASC or DESC for either one).



**SELECT teamID, yearID, W, L, W/(W+L) as Winning_Percentage, R, RA, R-RA as Run_Differential, (R-RA)/G as Run_Diff_Per_Game**
	**FROM Teams**
	**WHERE yearID >= 1901 AND W/(W+L) > .700**
	**ORDER BY W/(W+L) DESC, teamID, yearID**

![image-20201224145158506](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224145158506.png)

Now, take your previous query, and add a term that calculates Bill James's Pythagorean Expectation for Winning Percentage. The formula for this expectation is `(R*R)/(R*R+RA*RA)`. Call this term BillJames.

**SELECT teamID, yearID, W, L, W/(W+L) as Winning_Percentage, R, RA, R-RA as Run_Differential, (R-RA)/G as Run_Diff_Per_Game, (R*R)/(R*R+RA*RA) as BillJames**
	**FROM Teams**
	**WHERE yearID > 1900 AND W/(W+L) > .700**
	**ORDER BY W/(W+L) DESC, teamID, yearID**



![image-20201224145257817](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224145257817.png)



Finally, let's create a metric that determines the actual performance of these great teams (measured by Winning Percentage) compared to how Bill James's Pythagorean Formula would have expected them to perform. Simply add another term to your SELECT command, one that subtracts your term named Winning_Percentage from your term named BillJames. Call this term JamesMinusActual. Remember, you can't use your aliases to create this new term, you must use the formulas themselves.

Order your results by this new term - JamesMinusActual - in DESCENDING order. Additionally, continue to use teamID and yearID as the 2nd and 3rd parts of your ORDER BY command (don't use ASC or DESC for either one).

**SELECT teamID, yearID, W, L, W/(W+L) as Winning_Percentage, R, RA, R-RA as Run_Differential, (R-RA)/G as Run_Diff_Per_Game, (R*R)/(R*R+RA*RA) as BillJames, (R*R)/(R*R+RA*RA)-W/(W+L) as JamesMinusActual** 
	**FROM Teams**
	**WHERE yearID > 1900 AND W/(W+L) > .700**
	**ORDER BY JamesMinusActual DESC, teamID, yearID**

![image-20201224145430673](C:\Users\cboat\AppData\Roaming\Typora\typora-user-images\image-20201224145430673.png)



