### Semantic Sentence Similarity

## 1. Business Problem

Given two questions Q1 and Q2,  suppose that the wording of the Q2 is different but the semantic intent is completly the same.Q1 is already answered questions stored in the database and Q2 is the new Question asked by the user so as the intent of Q1 and Q2 is the same, we can show the answer of Q1 without waiting for the responses of the Q2 and suggest the same and thereby imporving the costumer experence of the platform.

So We need to devlop a machine learning Algorithm to identify duplicate/semantically similar questions.

### 1.1 Description

Quora is a place to gain and share knowledge—about anything. It’s a platform to ask questions and connect with people who contribute unique insights and quality answers. This empowers people to learn from each other and to better understand the world.

Over 100 million people visit Quora every month, so it's no surprise that many people ask similarly worded questions. Multiple questions with the same intent can cause seekers to spend more time finding the best answer to their question, and make writers feel they need to answer multiple versions of the same question. Quora values canonical questions because they provide a better experience to active seekers and writers, and offer more value to both of these groups in the long term.

Credits: Kaggle

Problem Statement

Identify which questions asked on Quora are duplicates of questions that have already been asked.
This could be useful to instantly provide answers to questions that have already been answered.
We are tasked with predicting whether a pair of questions are duplicates or not.

So the problem statement is to find which of the sentences/questions asked were semantically similar.

At that time Quora used a Random Forest model to do the same.

### 1.2 Sources/Useful Links

Source : https://www.kaggle.com/c/quora-question-pairs

### 1.3 Real world/Business Objectives and Constraints

1. The cost of a mis-classification can be very high. Suppose that the 2 questions are not duplicates/semantically similar but the machine learning algorithm it would be a very costly thing for the platform cause the users will most likely be humans and they can Identify very fast that the context of question and answer is different and the platform might lose some users.
2. You would want a probability of a pair of questions to be duplicates so that you can choose any threshold(say 0.8 this is completly upon expermentation) of choice.
3. No strict latency concerns but it should be done within min.
   Interpretability is partially important.

## 2. Machine Learning Probelm

### 2.1 Data

#### 2.1.1 Data Overview

- Data will be in a file Train.csv
- Train.csv contains 5 columns : qid1, qid2, question1(text), question2(text), is_duplicate(binary variable)
- Size of Train.csv - 60MB
- Number of rows in Train.csv = 404,290

### 2.2 Mapping the real world to an ML problem

#### 2.2.1 Type of Machine Learning Problem

It is a binary classification problem, for a pair of questions we need to predict if they are duplicate or not. 

#### 2.2.2 Performance Metric

Metric(s):

1. log-loss :

We just do not want the 0 or 1 value but we want the probability of the questions being duplicate or not.

https://www.kaggle.com/wiki/LogarithmicLoss

2. Binary Confusion Matrix

From Binary Confusion Matrix we can do Precission, Recall, TPR,FPR,FNR,TNR so that we understand whats happning in more detail

### 2.3 Train and Test Construction

We split the data by randomly splitting the data in the ratio of 70:30 or 80:20.

But if we had a time stamp for the database we could have done time based splitting as it would have been much better as the time stamp as matters in the context/types of qestions asked like politics.
