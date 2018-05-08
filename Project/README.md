# League of Legend Prediction model

## Team member
   
   name : Zhiguang(Gordon) Zhu 
   
   student ID : 1701213175
  
## Backgroud 
I believe that many of you have ever played the game called league of legend. And if you play this game, you must have experienced this circumstance.
   
   
For example, you are the last player to choose your hero, and all of us want to win to get a better rank, but you have a lot of choice, you want to win but don’t know which one to choose to cooperate with others. Then my model will help you choose the last hero to keep a highest win rate.

## Overview
LoL-predictor is a tool that uses Machine Learning to predict the outcome of a LOL game and suggest the best last pick. 

it may answer the following questions:

1、Given the other heroes, which last hero should you choose to make your win rate the highest.
      
2、which team will win considering all the heroes chosen. I can offer the win rate, you can make a gamble on the pro game and win some money.

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
      
## Using the logistic regression and evaluation
The algorithm used for training is Logistic Regression and the evaluation is done through cross validation. The trained model can be saved to a pickle file for later use. The cross validation is done on the train dataset and the final accuracy scores (ROC AUC and raw accuracy) are on the test dataset.

from sklearn.linear_model import LogisticRegression

lr = LogisticRegression(C=0.01, random_state=42)
lr.fit(X_train, y_train)


output:

INFO:preprocessing.dataset:The train dataset contains 78727 games

INFO:preprocessing.dataset:The test dataset contains 33740 games

INFO:training.cross_validation:Cross validation scores over the training set (7 folds): 0.646 +/- 0.000

INFO:training.cross_validation:Test ROC AUC: 0.628

INFO:training.cross_validation:Test accuracy score: 0.65



## Using the decision tree and evaluation

from sklearn.tree import DecisionTreeClassifier

tree = DecisionTreeClassifier(criterion='gini', 
                              max_depth=4, 
                              random_state=1)
                              
tree.fit(X_train, y_train)

![Image text](https://github.com/zzg1994115/PHBS_TQFML/blob/master/Project/picture/3.JPG)

![Image text](https://github.com/zzg1994115/PHBS_TQFML/blob/master/Project/picture/4.JPG)

confusion matrix

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

![Image text](https://github.com/zzg1994115/PHBS_TQFML/blob/master/Project/picture/5.JPG)

![Image text](https://github.com/zzg1994115/PHBS_TQFML/blob/master/Project/picture/7.JPG)

![Image text](https://github.com/zzg1994115/PHBS_TQFML/blob/master/Project/picture/6.JPG)

which meams if your team mate choose Leesin, Ahri, Lucian and Tresh, and enemy choose Riven, Reksai, Ziggs, Ezreal and Lulu. Then your best choice must be Jax, which is a counter of Riven. It makes sense!
 
## FAQ
1.Only 60% accuracy? That is not much better than predicting that radiant always wins.

Yes, after a lot of feature engineering and algorithm searching, this is the best I could come up with. Along my experiments, I tried using a variety of classification algorithms and even Neural Networks. Even with a lot of tuning, the NNs acted at best as good as the Logistic Regression, so yeah... There is also the human factor that strongly influences the outcome of a game, so there is no way of predicting each game with close-to-perfect accuracy.
