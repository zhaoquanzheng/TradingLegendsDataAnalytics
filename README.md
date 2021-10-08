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

//Link to TL_Q1.xlsx

## Question 2) Maximising Retainer Earnings
Retainers are like special staff which have names and abilities. Trading Legends is not a single player game and there are many competitions (mainly Trade Wars) where Retainers of one player fight another player with strength based on earnings. Initially, when I was trying to analyse Retainer Earnings I typed up all the different attribute stats but they kept changing very fast in the game and it was not beneficial to keep up with all the bonus modifiers. I figured out that there is a Retainer Basic Earning which depends on Retainer Level and Aptitude and not affected by modifiers, while the actual total Retainer Earning has additive and multiplicative modifiers applied onto the Basic Earning.
When I checked myself to see if these theories held, I was a bit worried because my predicted Earnings were thousands of dollars(or silvers) away from the actual Earnings. 
I noticed that there were differences in Earning between the rarity of the Retainer (SSR-A) and tried to work out empirically the earning per aptitude per level for each grade of the Retainer. 
A: 6.39
S: 6.95
SR: 7.38
SSR: 7.46
(with a total sample size of 25)
Thankfully when I did an Error Margin check, these errors were 0-1% off from the actual Earning and so I can attribute the error to rounding in Game (I don't get to see the exact actual Earning).

[TL_Q2.xlsx](https://github.com/zhaoquanzheng/TradingLegendsDataAnalytics/files/7298265/TL_Q2.xlsx)

## Question 3) Exploring Estate
At Level 25, Estate is unlocked. Estate complicates everything as it can give bonuses to the Market or Retainers.
Currently level 32, with unlocked crops: Radish, Carrot, Potato, Bamboo Shoot, Onion, Lettuce, Pumpkin; animals: Chicken, Dog, Pig, Sheep, Ox, Cat
All crops and animals have base production rate of 59/min + 1/level
There are various modifiers for each different animal, and they have different upgrade costs and different tech costs. Modifiers will be ignored and I am attempting to find a relationship in the increase of the costs.
Intuitively, levelling up everything at a constant rate (cheapest first) is most efficient.
