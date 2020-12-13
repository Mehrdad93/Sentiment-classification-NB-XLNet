## NLP State-Of-The-Art (SOTA) model: XLNet

- The SOTA (fine-tuned XLNet-base) model can be here: 

> https://drive.google.com/file/d/16NriGqdPSeJ9-cap-9w1TlZpYC4aWkHW/view?usp=sharing

- To load the saved model on Python, use the code below:

`model.load_state_dict(torch.load(filepath))`

------------------------

**1) Which SOTA for sentiment classification?**

Finding a proper SOTA for sentiment classification task was the first step to be done. For that purpose, I have looked up the *NLP-progress* website and some other novel literatures in NLP area: http://nlpprogress.com/english/sentiment_analysis.html

As you can see in the link above, **XLNet (Yang et al., 2019) model** shows promising results for both fine-grained as well as binary classification problems on all IMDb, Yelp, and SST datasets.

Here is another usefull document for comparing the accuracy of XLNet-base and -large models and other sota models such as BERT and RoBERTa: https://www.cs.princeton.edu/courses/archive/spring20/cos598C/lectures/lec5-pretraining2.pdf


**2) Pytorch interface for XLNet**

To produce a classifier for text classification, I have finetune the pretrained XLNet-base model with the huggingface PyTorch library (**pytorch-transformers** and **transformers**). 

> Ref: https://colab.research.google.com/drive/16gx06PVffJwS4pRhysCmc5qbPm26vsY8


**3) XLNet tokenizer**

XLNet token pattern looks like this:

`Sentence_A + [SEP] + Sentence_B + [SEP] + [CLS]`

, which For single sentence inputs here, we just need to add `[SEP]` and `[CLS]` to the end.


XLNet also requires specifically formatted inputs. For each tokenized input sentence, we need to create:

i) input ids: a sequence of integers identifying each input token to its index number in the XLNet tokenizer vocabulary

ii)segment mask: (optional) a sequence of 1s and 0s used to identify whether the input is one sentence or two sentences long. For one sentence inputs, this is simply a sequence of 0s. For two sentence inputs, there is a 0 for each token of the first sentence, followed by a 1 for each token of the second sentence

iii) attention mask: (optional) a sequence of 1s and 0s, with 1s for all input tokens and 0s for all padding tokens (we'll detail this in the next paragraph)

iv) labels: a single value of 1 or 0. In our task 1 means "grammatical" and 0 means "ungrammatical"






**4) Fine-tuning XLNet model**

Thankfully, the huggingface pytorch implementation includes a set of interfaces designed for a variety of NLP tasks. Though **these interfaces are all built on top of a trained model**, each has different top layers and output types designed to accomodate their specific NLP task.

In this task `XLNetForSequenceClassification` was used. This is the normal XLNet model with an added single linear layer on top for classification that we will use as a sentence classifier. As we feed input data, the entire pre-trained XLNet model and the additional untrained classification layer is trained on our specific task. Rather than training every layer in a large model from scratch, it's as if we have already trained the bottom layers 95% of where they need to be, and **only really need to train the top layer**, with a bit of tweaking going on in the lower levels to accomodate our task.

**5) Fine-tuning XLNet model**


**n-1) References**

The source code is written in Python 3 using Colab and I have used multiple references to finish the task. All references have been cited and mentioned in Colab code cells (src directory). 

**n) Acknowledgment**

I would like to acknowledge the role of Google Colab platform in this assessment for providing me with free GPUs, which was a must for fine-tuning the XLNet models.

