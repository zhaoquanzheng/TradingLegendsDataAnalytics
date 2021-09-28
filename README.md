# TradingLegendsDataAnalytics
Trading Legends is an idle-playing mobile phone game with many events and minigames within. The goal of idle-games is to maximise earnings but this is not simple in Trading Legends, due to the different ways earnings can be improved. 

## Introduction
At the start of the game there are 3 main sources of income. The currency is called silvers.
1) Bank
 - Tapping the bank gives silver
 - Upgrading the bank unlocks autotaps per second
2) Market stalls
 - Recruit staff in stalls with silver
 - Each stall has earnings based on: (Stall base * staff number) * bonuses  
3) Heirs
 - Heirs have earnings (salary) which increases while you raise them and becomes fixed once they are adults
 - Heir earnings depends mainly on their mother intimacy, and can also be increased by other bonuses

## Question 1) Maximising Market Earnings  
The Market has a simple formula in calculating earnings:  
Earnings = ((Staff_Earning * Number_of_Staff) + Retainer_Bonus) * Other Bonuses 
where Retainer_Bonus = Retainer_Earnings / 1000  
The cost to recruit staff is exponential and is more expensive for more advanced buildings.  
Intuitively the equation to maximising market earnings would be: Expected_Earning_Increase/Recruitment_Cost  
where Expected_Earning_Increase = ((Staff_Earning * 1) + Retainer_Bonus) * Other Bonuses  
then for all possible market buildings, select the one which has highest Expected_Earning_Increase   

Interestingly, I did a bit of research regarding idle games and found a different formula, which also takes into account the current earning rate and time required to be able to afford the next recruitment/upgrade.   
Upgrade_Cost_to_Yield(X) = Cost(X)/Current_Earning_Rate + Cost(X)/(Current_Earning_Rate + Rate(X))    
// reproduced from https://gamedevelopment.tutsplus.com/articles/numbers-getting-bigger-the-design-and-math-of-incremental-games--cms-24023   
then for all possible market buildings, select the one which has lowest Upgrade_Cost_to_Yield  

Most of the time, the two formulas point to the same market building, but what should be chosen when they don't? The answer is simple! The 2nd formula considers affordability so if you have been afk for awhile and amassed tons of silver use the 1st formula. Otherwise where silver is limiting your purchase choices, go by the 2nd formula!

//TODO Upload the xlsx file or create google sheet link?

## Question 2) Maximising Retainer Earnings


