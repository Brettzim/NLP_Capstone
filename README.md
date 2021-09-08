# NLP_Capstone

## Overview

This repository analyzes data in the form of Tweets about hurricanes to create a natural language processing classification model capable of predicting whether the sentiment of a Tweet is that of expressing danger, an emergency, or relief/aid. Due to target class imbalance, the goal of my model is to have a high F1 score. This will be the metric I go by to determine whether predictions are meaningful. 

By using different machine learning techniques, I am capable of interpreting how a Tweet should be perceived by the reader during a live event like a hurricane

## Business Problem

This model may be used by individuals stuck in a natural disaster that wants to get live updates in the area. 

## The Data

The Twitter dataset is from HumAID, which consists of around 15000 annotated tweets that has been collected during four major hurricanes: Harvey, Irma, Matthew, and Maria. The dataframe contains three columns

* tweet_id – a unique identifier for the poster of the Tweet
* tweet_text – The Actual Tweet itself
* class_label – The manually labeled sentiment class

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


## Analysis

I first created my baseline model with a dummy classifier. Due to the target class imbalance, the dummy was set to use the stratified strategy. 

The first simple model was a pipeline with a tfidf vectorizer and logistic regression. It performed very well so I wanted to see how tuning hyperparameters via a grid search would go.

My next model was a pipeline with a multinomial naïve bayes classifier. From the start, I liked the idea of using a naïve bayes classifier, so I went in on a grid search to get the optimal parameters for this type of model.

I then tried the tuned NB model on my data cleaned a couple of different ways. I used it on regular cleaned text, on stemmed text, and then on lemmatized text. As it turns out, the regular text produced the best scores by a small margin.

My next step is to move past grid search and try advanced prepackaged models. I went with XLNet via PyTorch.

## Conclusion
