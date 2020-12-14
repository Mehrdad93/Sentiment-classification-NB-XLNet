## NLP basic model: Multinomial NB (naive bayes)

- The trained basic/baseline model is attached in this page in the pickle format (pickle_basic_model.pkl).

- I am not covering EDA results here as they have been already discussed in details in the `EDA` folder.

------------------------

**1) Baseline for sentiment classification**

To find the proper non deep learning classifier, I have read a lot of articles, stackoverflow comments, and Kaggle notebooks. Ultimately, based on the previous expereinces on sentiment classification tasks, I have decided to go with **multinomial naive bayes (NB)** and tree-based models including RandomForest. 

Best Kaggle Refs:

i) https://www.kaggle.com/c/sentiment-analysis-on-movie-reviews/notebooks

2) https://www.kaggle.com/kazanova/sentiment140/notebooks


**2) Scikit-learn for feature extraction**

**CountVectorizer:** Convert a collection of text documents to a matrix of token counts.

If you do not provide an a-priori dictionary and you do not use an analyzer that does some kind of feature selection then the number of features will be equal to the vocabulary size found by analyzing the data.

Ref: https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html#sklearn.feature_extraction.text.CountVectorizer


**3) Scikit-learn for model training**




**7) References**

The source code is written in Python 3 using Colab and I have used multiple references to finish the task. All references have been cited and mentioned in  the source code (colab code cells). Please look at the `src` directory. 

**8) Acknowledgment**

I would like to acknowledge the role of Google Colab platform in this assessment for providing me with free CPUs and GPUs.
