# League of Legend Prediction model

## Team member
   Zhiguang(Gordon) Zhu 
   1701213175
  
## Backgroud 
I believe that many of you have ever played the game called league of legend. And if you play this game, you must have experienced this circumstance.
   
   
For example, you are the last player to choose your hero, and all of us want to win to get a better rank, but you have a lot of choice, you want to win but don’t know which one to choose to cooperate with others. Then my model will help you choose the last hero to keep a highest win rate.

## Overview
LoL-predictor is a tool that uses Machine Learning to predict the outcome of a LOL game and suggest the best last pick. 

it may answer the following questions:

1、Given the other heroes, which last hero should you choose to make your win rate the highest.
      
2、which team will win considering all the heroes chosen. I can offer the win rate, you can gamble on the pro game.

The project achieves roughly 0.628 ROC AUC score and 0.65 accuracy using Logistic Regression. The code is used mainly for creating models used by https://www.kaggle.com/paololol/league-of-legends-ranked-matches.

## Mining data
Mining approximate 100000 games and the filtered data is as follows:

![Image text](https://github.com/zzg1994115/PHBS_TQFML/blob/master/Project/picture/1.JPG)

I give 139 different heros as orders [1,2,3,...,139]

in excel saving them to a file is as simple as:

![Image text](https://github.com/zzg1994115/PHBS_TQFML/blob/master/Project/picture/2.JPG)

red team 1: red team top 

red team 2: read team jungle

red team 3: read team mid

red team 4: read team adc

red team 5: red team support

blue team win: 1 stands for blue team win and 0 stands for red team win 
      
## Training and evaluating a model
The algorithm used for training is Logistic Regression and the evaluation is done through cross validation. The trained model can be saved to a pickle file for later use. The cross validation is done on the train dataset and the final accuracy scores (ROC AUC and raw accuracy) are on the test dataset.

output:

INFO:preprocessing.dataset:The train dataset contains 78727 games

INFO:preprocessing.dataset:The test dataset contains 33740 games

INFO:training.cross_validation:Cross validation scores over the training set (7 folds): 0.646 +/- 0.000

INFO:training.cross_validation:Test ROC AUC: 0.628

INFO:training.cross_validation:Test accuracy score: 0.65

##Visualizing data
![Image text](https://github.com/zzg1994115/PHBS_TQFML/blob/master/12.JPG)
                                       learning curve

## Querying a model
There are two type of queries you can do:

full query: insert all 10 heroes in a game and predict the winner

partial query: insert 9 heroes in a game and the prediction will be made in order to maximize the 10th player's winning chance
from training.query import query

full_result = query([59, 56, 54, 48, 31],
                    [40, 41, 52, 68, 61])

partial_result = query([59, 56, 54, 48, 31],
                       [40, 41, 52, 68])
                      
## Real world Example 
If you put [9,78,65,43,23],[4,8,76,122,]

which meams if your team mate choose Leesin, Ahri, Lucian and Tresh, and enemy choose Riven, Reksai, Ziggs, Ezreal and Lulu. Then your best choice must be Garen, which is a counter of Riven. It make sense!
 
## Dataset description
Kaggle https://www.kaggle.com/paololol/league-of-legends-ranked-matches
Data about 100000 League of Legends ranked games, spanning across several years
All data belongs ultimately to Riot Games and their data policies applies. 
