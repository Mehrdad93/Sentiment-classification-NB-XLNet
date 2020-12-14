# XLNet-base vs. Naive Bayes classifier

**Folder Structure**

    |+--- README.md
    |
    |+--- EDA
    |     +--- EDA related images (.png) + explanations 
    |
    |+--- data
    |     +--- train/dev/test datasets (.csv)
    |
    |+--- result
    |     +--- SOTA
    |          +--- model evaluation results (.csv) + fine-tuned xlnet model + explanations 
    |     +--- basic
    |          +--- model evaluation results (.csv) + multinomial naive bayes trained model + explanations 
    |
    |+--- src
    |     +--- SOTA
    |          +--- fine-tuned xlnet model source code
    |     +--- basic
    |          +--- multinomial naive bayes algo source code


Each folder has its own README file. So, for extra explanations please visit the sub-folders.


--------------------------------

## Problem

**Data description:**
This is a sentiment classification task for hotel reviews. There are 5 ratings that are the labels to be predicted based on the text in the reviews. You have been given the ratings for the train and dev sets. The ratings on the test set have been withheld. 

## Task Description:
 Building 2 models for the text classification task – 
1. A Baseline model  
2. A State of the art (SOTA) model and compare them.

