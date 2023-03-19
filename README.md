# Sentiment Analysis of Tweets

## About the project

This project aims to build a model to accurately predict the sentiment of tweets. Naive Bayes Classifier, Logistic Regression, RoBERTa, and a combination of multiple LSTM models are the four techniques we apply for the project.


## Overview

LSTM_models.py (LSTM Neural Networks Models) and run.ipynb the final notebook that generates the submissions, are the primary script/notebook for this project. We explored a number of classification techniques, including Naive Bayes, Logistic Regression, and RoBERTa (for the short datasets owing to a lack of resources), however the combination of LSTM neural networks produced the best accuracy for us. For the purpose of completeness, the other ML implementations are provided in this repository; read the README for additional information.

LSTM_models.py : is a script that trains the model using the preprocessed training dataset and generates predictions after preprocessing.py has been executed.
run.ipynb: The final notebook contains the preprocessing, implementation, and fitting phases for each model, as well as the creation of the submission file that we post to aicrowd.

All other and helpers scripts are stored in sc/ directory.

## Dependencies
To run our code from scripts or even simpler by running the run.ipynb file you will need to install the following libraries:

- wordninja
- emot
- contractions
- spacy
- nltk
- simpletransformers
- transformers
- tokenizers

The scripts and pynotebook assume that the train pos full and train neg full, as well as the 1.9GB of pretrained Glove embeddings as glove.twitter.27B.200d.txt, which you can download by the following commands,

```bash
$ wget https://nlp.stanford.edu/data/glove.twitter.27B.zip -O glove-stanford/glove.twitter.27B.zip
$ unzip glove-stanford/glove.twitter.27B.zip -d glove-stanford/
```
are under the  data/ directory because we weren't able to import the full dataset to github. 


## Structure
```bash
├── submission_last.csv                    : contains the last submission file that is generated by run.ipynb.
├── README.md                              : The README guideline and explanation for our project.
|
├── Analysis of the data
│   ├── Exploration of the data.ipynb      : contains the data analysis of the tweets before and after preprocessing.
|
├── notebooks
│    ├── roberta.ipynb                     : contains the training of RoBERTa mdoels using the small tweet dataset using the preprocessed training set.
|    ├── run.ipynb
|    ├── train_embeddings_and_logistic_regression.ipynb :contains the training of embeddings using different approaches and train a logistic model using training set.
|
├── src
│   ├── helpers.py                         : script containing helpers method.
│   ├── preprocessings.py                  : script containing our methods to preprocess tweets .
│   ├── Models                             : contains our model implementation.
|       ├── LSTM_models.py                 : contains the implementation of 6 LSTM models and the XGB classifier using the preprocessed training set.
|       ├── Naïve_Bayes_Classifier.py      : contains the implementation of Naive Bayes Classifier using the preprocessed training set.
|       ├── RoBERTa.py                     : contains the construction of RoBERTa mdoels using the small tweet dataset using the preprocessed training set.
|       ├── logistic_regression.py         : contains the implementation of logistic regression model using the preprocessed training set.
|
├── data
│   ├── test_data.txt                      : Twitter test dataset, containing 10,000 unlabeled tweets.
│   ├── train_neg.txt                      : Twitter training dataset, containing 100.000 negative tweets.
│   ├── train_pos.txt                      : Twitter training dataset, containing 100,000 positive tweets.
|
```
## DEEPER OVERVIEW

The data for this project consists of two sets of 1,250,000 tweets, one with positive emotions and one with negative emotions.
## Preprocessing phase
```bash
Casefolding
Remove the single letters
Lemmatization
Remove stopwords
Removing numbers as well the numbers within words by possible typos .
Expand English contraction
Manually expand some patterns
Remove English punctuation
Highlight sentiment words as positive and negative using two dataset(for additional information you can see the notebook)
Remove the hashtag symbol and split the mergedwords in hashtags
Transform emoticons into tokens/words
```

## Embeddings
As you can check in the notebook "train embeddings and logistic regression.ipynb," our initial approach for the embeddings was to train and build our embeddings over our training set using various approaches like Word2Vec, Doc2Vec, FastText, or even GLoVe. However, in the end, we used the pretrained GloVe embeddings trained on 4 billion tweets, with 200 dimension embedding

## Final Model
For our final submission, we used six different LSTM models, some of which included convolutional layers and other dense layers. However, all of the models were built and trained for six epochs with a batch size of 1024, and the size of the embeddings was set to match that of the pretrained Glove embeddings. The results may be seen on aicrowd under the aymeric bacuet account (after some changes in the preprocessing step) or even under the lstojollari account (86,3%), which shows that we were able to achieve an accuracy of 87%.

Evaluation
We have evaluated our models using the Accuracy and F1 score metrics.

## How to use run.ipynb

To use the trained model to classify new tweets, follow the instructions in the run.ipynb file.
