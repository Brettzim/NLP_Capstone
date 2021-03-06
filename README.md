# NLP Text Classification on Twitter Data During Natural Disasters

![Natural Disaster](https://upload.wikimedia.org/wikipedia/commons/0/04/Hurricane_Isabel_from_ISS.jpg)

## Table of Contents
* [Repository Structure](#Repository-Structure)
* [Overview](#Project-Overview)
* [Use Case](#Use-Case)
* [The Data](#The-Data)
* [Data Cleaning](#Data-Cleaning)
* [Analysis](#Analyis)
* [Conclusions](#Conclusion)

## Repository Structure
```
.
├── data
│   └── datasets-from-Humaid-and-Twitter
├── output
│   └── classified-documents
├── README.md
├── interface.md
├── models.ipynb
├── visualizations.ipynb
└── twint_scraper.md
```
## Project Overview

This repository analyzes data in the form of Tweets about hurricanes to create a natural language processing classification model capable of predicting whether the sentiment of a Tweet is that of expressing danger, an emergency, or relief/aid. Due to target class imbalance, the goal of my model is to have a high F1 score. This will be the metric I go by to determine whether predictions are meaningful. 

By using different machine learning techniques, I am capable of interpreting how a Tweet should be perceived by the reader during a live event like a hurricane

## Use Case

This model may be used by individuals stuck in a natural disaster that wants to get live updates in the area. To run, either download a pickled model from my [Dropbox](https://www.dropbox.com/sh/c8kl6xjvpytoh3o/AABBHBs0w8qE3_B7bZi_KHZla?dl=0), Or create your own with models.ipynb. Then, run interface.ipynb and make sure it is using the correct NLP model. Now, modify the Twint scraper for topic of Tweets and the notebook should output 4 documents on seperated Tweets by topic.

## The Data

The Twitter dataset is from [HumAID](https://crisisnlp.qcri.org/humaid_dataset.html), which consists of around 15000 annotated tweets that has been collected during four major hurricanes: Harvey, Irma, Matthew, and Maria. The dataframe contains three columns

* tweet_id – a unique identifier for the poster of the Tweet
* tweet_text – The Actual Tweet itself
* class_label – The manually labeled sentiment class

## Data Cleaning

The target classes in the provided datasets consists of following humanitarian categories on the left. These nine classes were then condensed by me into the four classes on the right:

Humaid Targets | My Targets
------------ | -------------
Displaced people and evacuations 		    |Relief
Rescue volunteering or donation effort 	|Relief
Caution and advice 				              |Danger
Infrastructure and utility damage		    |Danger
Injured or dead people 	 		            |Danger
Requests or urgent needs			          |Emergency
Not humanitarian				                |Other
Other relevant information			        |Other
Sympathy and support			              |Other

Fitting these targets together left me with a class imbalance. To mitigate this and pad the emergency class, I used Twint to scrape emergency related tweets made during Hurricane Sandy to add to the dataset.

The text preprocessing Steps taken are as follows:

* Removing Twitter specific embedded text like mentions, Retweets, Links, Videos, and Hashtags
* Tokenizing sentences into lists of words
* Lower casing all letters in the dataset
* Removing stop words that  do not add meaning to a sentence. Words “like the, and, at”
* Removing punctuation and symbols
* Stemming or lemmatizing words to their root

## Analysis

My baseline model was a dummy classifier. Due to the target class imbalance, the dummy was set to use the stratified strategy. 

The first simple model was a pipeline with a tfidf vectorizer and logistic regression. It performed very well but there were signs of overfitting. So re worked the model by tuning hyperparameters via a grid search.

My next model was a pipeline with a multinomial naïve bayes classifier. From the start, I liked the idea of using a naïve bayes classifier, so I went in on a grid search to get the optimal parameters for this type of model.

I then tried the tuned NB model on my data cleaned a couple of different ways. I used it on regular cleaned text, on stemmed text, and then on lemmatized text. As it turns out, the regular text produced the best scores by a small margin.

Up to this point, I vectorized my text with a TFIDF Vectorizer. I wanted to try the same with a Word2Vec Vectorizer

My next step is to move past grid search and try a prepackaged models. I went with [RoBERTA by Facebook](https://ai.facebook.com/blog/roberta-an-optimized-method-for-pretraining-self-supervised-nlp-systems/).

Pickled models can be accessed from [Dropbox](https://www.dropbox.com/sh/c8kl6xjvpytoh3o/AABBHBs0w8qE3_B7bZi_KHZla?dl=0)


## Conclusion

In conclusion after testing a manipulating different kinds of models, I was impressed with RoBERTa's performance. Even though it performed the best, the robustness of the modelmade it run considerably slower than even the complex naive bayes model I developed. Due to the extreme training time, there is still more to look at when it comes to hyperparameter tuning on RoBERTa. For now, the users choice of text classification model is situational for speed vs accuracy.

