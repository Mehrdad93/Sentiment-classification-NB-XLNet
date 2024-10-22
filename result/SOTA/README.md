## NLP State-Of-The-Art (SOTA) model: XLNet

- The SOTA (fine-tuned XLNet-base) model can be here: 

> https://drive.google.com/file/d/16NriGqdPSeJ9-cap-9w1TlZpYC4aWkHW/view?usp=sharing

- To load the saved model on Python, use the code below:

`model.load_state_dict(torch.load(filepath))`

------------------------

**1) SOTA for sentiment classification**

Finding a proper SOTA for sentiment classification task was the first step to be done. For that purpose, I have looked up the *NLP-progress* website and some other novel literatures in NLP area: http://nlpprogress.com/english/sentiment_analysis.html

As you can see in the link above, **[XLNet (Yang et al., 2019) model](https://github.com/zihangdai/xlnet)** shows promising results for both fine-grained as well as binary classification problems on all IMDb, Yelp, and SST datasets.

Here is another useful document for comparing the accuracy of XLNet-base and -large models and other sota models such as BERT and RoBERTa: https://www.cs.princeton.edu/courses/archive/spring20/cos598C/lectures/lec5-pretraining2.pdf

<img src="https://github.com/Mehrdad93/Chata-assessment/blob/main/result/SOTA/image/picking_sota.png" width="500"/>

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

**4) Fine-tuning pre-trained XLNet model**

Thankfully, the huggingface pytorch implementation includes a set of interfaces designed for a variety of NLP tasks. Though **these interfaces are all built on top of a trained model**, each has different top layers and output types designed to accomodate their specific NLP task.

In this task `XLNetForSequenceClassification` was used. This is the normal XLNet model with an added single linear layer on top for classification that we will use as a sentence classifier. As we feed input data, the entire pre-trained XLNet model and the additional untrained classification layer is trained on our specific task. Rather than training every layer in a large model from scratch, it's as if we have already trained the bottom layers 95% of where they need to be, and **only really need to train the top layer**, with a bit of tweaking going on in the lower levels to accomodate our task.

There are a few different pre-trained XLNet models available. In this work **`xlnet-base-cased`** used, which means the version that has both upper and lowercase letters ("cased") and is the smaller version of the two ("base" vs "large"). Due to the new GPU limitations on Colab `xlnet-large-cased` is not feasible. However, I have tried to load and finetune the large XLNnet model with lower batch and epoch numbers which led to a very poor accuracy (will be shown later in this page).

For the purposes of fine-tuning, the authors recommend the following hyperparameters in the following ranges (broken down by which NLP dataset they are applied to):

<img src="https://github.com/Mehrdad93/Chata-assessment/blob/main/result/SOTA/image/hyper_par_xlnet.png" width="500"/>

**Side Note:** Classes (in our case: ratings) should start from 0 (0:4) not 1! Not knowing that while using `transformers` library in Python would raise error in the optimization part.

**5) Training loss**

The XLNet fine-tuned model's training loss over all batches can be seen below. As you can see, training loss is fluctuating quite a lot, however, the loss trend is promising and in each epoch we can see the loss gets smaller and smaller. 

Number of training epochs = 4
batch size = 32

<img src="https://github.com/Mehrdad93/Chata-assessment/blob/main/result/SOTA/image/train_loss_xlnet.png" width="750"/>

**6) Prediction and evaluation on dev set**

Here is the classification report on development set (unseen dataset with ratings):

<img src="https://github.com/Mehrdad93/Chata-assessment/blob/main/result/SOTA/image/xlnet_model_report.png" width="500"/>

**7) Hyperparameter vs. Accuracy**

Using the same GPU (Tesla T4) and RAM (12 G), I have fine-tuned our sota model with variety of hyperparameters to find the best set of them. Here is the my findings:

`xlnet-base-cased`

| Accuracy | Batch Size | Epoch | Learning Rate | Data Cleaning |
| :-----: | :-----: | :----: | :-------: | :-------: |
| **0.79** | 32 | 4 | 3e-5 | No |
| 0.78 | 48 | 4 | 3e-5 | No |
| 0.78 | 32 | 6 | 3e-5 | No |
| 0.78 | 32 | 6 | 5e-5 | No |
| 0.78 | 32 | 4 | 1e-5 | No |
| 0.78 | 32 | 4 | 3e-5 | **Yes** |
| 0.21 | 32 | 4 | **4e-4** | No |

As shown in table above, changing batch size and epoch as long as they are in the recommended ranges (published by author of XLNet paper), the overall accuracy will not change significantly. However, learning rate can play an important role on the accuracy if changes by an order of magnitude. 

Another interesting result is that adding emoji removal function to our pre-processing part does not affect the overall accuracy since the pre-trained model is crazy huge!

`xlnet-large-cased`

| Accuracy | Batch size | Epoch | Learning Rate |
| :-----: | :----: | :----: | :-------: |
| 0.75 | 8 | 4 | 3e-5 |

Reason for the lower accuracy in large model can be the small number of batches due to the GPU usage limitations.
Going over 8 batchese is also computationally very expensive and with the new Google Colab policy almost impossible!

**8) References**

The source code is written in Python 3 using Colab and I have used multiple references to finish the task. All references have been cited and mentioned in  the source code (colab code cells). Please look at the `src` directory. 

**9) Acknowledgment**

I would like to acknowledge the role of Google Colab platform in this assessment for providing me with free GPUs, which was a must for fine-tuning the XLNet models.

