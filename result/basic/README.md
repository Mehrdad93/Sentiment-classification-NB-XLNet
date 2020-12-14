## NLP basic model: Multinomial NB (naive bayes)

- The trained basic/baseline model is attached in this page in the pickle format (pickle_basic_model.pkl).

- I am not covering EDA results here as they have been already discussed in details in the `EDA` folder.

------------------------

**1) Baseline for sentiment classification**

To find the proper non deep learning classifier, I have read a lot of articles, stackoverflow comments, and Kaggle notebooks. Ultimately, based on the previous expereinces with sentiment classification tasks, I have decided to go with **multinomial naive bayes (NB)** and tree-based models including RandomForest. 

Best Kaggle Refs:

i) https://www.kaggle.com/c/sentiment-analysis-on-movie-reviews/notebooks

ii) https://www.kaggle.com/kazanova/sentiment140/notebooks


**2) Scikit-learn for feature extraction**

**CountVectorizer:** Convert a collection of text documents to a matrix of token counts.

If you do not provide an a-priori dictionary and you do not use an analyzer that does some kind of feature selection then the number of features will be equal to the vocabulary size found by analyzing the data.

Ref: https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html#sklearn.feature_extraction.text.CountVectorizer


**3) Scikit-learn for model training, evaluation, and prediction**

Here is a small snippet of the Multinomial NB results (predicted ratings) on developmenmt dataset (unseen data with ratings for comparison):

<img src="https://github.com/Mehrdad93/Chata-assessment/blob/main/result/basic/image/basic_result.png" width="750"/>

Here is the classification report on development set:

<img src="https://github.com/Mehrdad93/Chata-assessment/blob/main/result/basic/image/basic_model_report.png" width="500"/>

**4) Multinomial NB vs. Random Forest**

As discussed in the first part, these two models are showing better results among other basic (non-deep learning) NLP algorithms for the sentiment classification task. Here is the my findings:

| Accuracy | Classifier | F1-score for Rating 1 | Data Cleaning |
| :-----: | :--------: | :----: | :-------: | 
| **0.75** | Multinomial Naive Bayes | 0.80 | Only basic cleaning |
| 0.61 | Multinomial Naive Bayes | 0.66 | Basic cleaning + remove non adj./verb/adverb |
| 0.40 | Random Forest | 0.44 | Only basic cleaning |

For the purpose of sentiment analysis with basic models, some [references](https://www.kaggle.com/neokaixiang89/using-pos-tag-to-aid-textual-data-pre-processing) suggest to take advantage of Parts-Of-Speech (POS) technique to only keep adjectives and adverbs (and sometimes verbs) to better reflect the sentiment of each review/comment and make the computation faster.

However, as shown in table above, removing non -adjectives, -adverbs, and -verbs in our problem did not go very well and made the overall accuracy about 20% smaller!

**5) References**

The source code is written in Python 3 using Colab and I have used multiple references to finish the task. All references have been cited and mentioned in  the source code (colab code cells). Please look at the `src` directory. 

**6) Acknowledgment**

I would like to acknowledge the role of Google Colab platform in this assessment for providing me with free CPUs and GPUs.
