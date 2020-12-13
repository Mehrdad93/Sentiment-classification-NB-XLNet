## NLP State-Of-The-Art (SOTA) model: XLNet

- The SOTA (fine-tuned XLNet-base) model can be here: 

> https://drive.google.com/file/d/16NriGqdPSeJ9-cap-9w1TlZpYC4aWkHW/view?usp=sharing

- To load the saved model on Python, use the code below:

`model.load_state_dict(torch.load(filepath))`

------------------------

1) **Which SOTA for sentiment classification?**

Finding a proper SOTA for sentiment classification task was the first step to be done. For that purpose, I have looked up the *NLP-progress* website: http://nlpprogress.com/english/sentiment_analysis.html

As you can see in the link above, **XLNet (Yang et al., 2019) model** shows promising results for both fine-grained as well as binary classification problems on all IMDb, Yelp, and SST datasets.

Here is another usefull document for comparing the accuracy of XLNet-base and -large models and other sota models like BERT and RoBERTa: https://www.cs.princeton.edu/courses/archive/spring20/cos598C/lectures/lec5-pretraining2.pdf

2) 
