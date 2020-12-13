
1. 'rating_distr_train_set' or 'counts of each sentiment in train data' shows the distribution of ratings in training data. The distribution of the data in train set is very well balanced, meaning no over- or undersampling is needed. Also, from this image, it can be seen that one 'rating' in the train is holding some texts, which ruins the numeric (1,2,3,4,5) order of classes. This instance got removed!

![alt text](https://github.com/Mehrdad93/Chata-assessment/blob/main/EDA/rating_distr_train_set.png)

2. 'rating_distr_dev_set' or 'counts of each sentiment in dev data' shows the distribution of ratings in development data. The distribution of the data in dev set is very well balanced, meaning no over- or undersampling is needed.

![alt text](https://github.com/Mehrdad93/Chata-assessment/blob/main/EDA/rating_distr_dev_set.png)

3. 'wordcloud_highest' shows the most frequent words in the raw train set for the highest rating hotels (5). As you can see, words like excellent, relaxing, friendly, perfectly, convinent, are among the most frequent ones.

![alt text](https://github.com/Mehrdad93/Chata-assessment/blob/main/EDA/wordcloud_highest.png)

4. 'wordcloud_lowest' shows the most frequent words in the raw train set for the lowest rating hotels (1). As you can see, words like worst, tired, annoyed, declined, are among the most frequent ones.

![alt text](https://github.com/Mehrdad93/Chata-assessment/blob/main/EDA/wordcloud_lowest.png)

5. 'rating_length_relation' represents the relation between the rating scores and their review length. **This one perhaps is the most interesting finding! Why?** As you can see, for lower ratings (1, 2, 3), there is almost the same distribution and pattern (large second peak and smaller first peak). However, for the higher ratings (4, 5) trend is reversed (large first peak and smaller second peak) 
**This means that most of the relatively unhappy customers tend to write a longer review in compare to satisfied ones.** Such a behavior makes sense as people with a bad experience tend to complain and write more about their bad experience.

![alt text](https://github.com/Mehrdad93/Chata-assessment/blob/main/EDA/rating_length_relation.png)

6. 'cleaning_effect' represents the effect of text cleaning/pre-processing on the length of reviews, which makes the computation in the basic model much faster! The red bar plot shows too many lengthy reviews with useless words in them for model training, which in the blue bar plot they have been removed using the StopWords and/or other NLP techniques such as lemmatization.

![alt text](https://github.com/Mehrdad93/Chata-assessment/blob/main/EDA/cleaning_effect.png)
