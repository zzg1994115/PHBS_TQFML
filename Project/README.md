# League of Legend Prediction model

## Team member
   Zhiguang(Gordon) Zhu 
   1701213175
  
## Backgroud 
I believe that many of you have ever played the game called league of legend. And if you play this game, you must have experienced this circumstance.
   
For example, you are the last player to choose your hero, and all of us want to win to get a better rank, but you have a lot of choice, you want to win but don’t know which one to choose to cooperate with others. Then my model will help you choose the last hero to keep a highest win rate.

## LOL Predictor
My project wants to use the machine learning to analyze the lol game (league of legends), it may contains the following questions:
      1、Given the other heroes, which last hero should you choose to make your win rate the highest.
      2、which team will win considering all the heroes chosen. I can offer the win rate, you can gamble on it.
      
## Training model
The algorithm used for training is Logistic Regression
it contains ten input variables and one input variable(1 or 0).
for example, ([59, 56, 54, 48, 31],[40, 41, 52, 68, 61]), 1 or 0.

## Querying a model
There are two type of queries you can do:

full query: insert all 10 heroes in a game and predict the winner
partial query: insert 9 heroes in a game and the prediction will be made in order to maximize the 10th player's winning chance
from training.query import query

full_result = query([59, 56, 54, 48, 31],
                    [40, 41, 52, 68, 61])

partial_result = query([59, 56, 54, 48, 31],
                       [40, 41, 52, 68])
                      
## Dataset description
Kaggle https://www.kaggle.com/paololol/league-of-legends-ranked-matches
Data about 300000 League of Legends ranked games, spanning across several years
All data belongs ultimately to Riot Games and their data policies applies. 
