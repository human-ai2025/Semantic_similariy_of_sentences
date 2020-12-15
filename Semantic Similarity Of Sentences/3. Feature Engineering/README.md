# Feature Extraction

We build features from initial set of measured data and derive features intended to be informative and non-redundant.

## Definations of terms

1. Token:- Lets take a question/string and say the words are W1, W2, W3, W4, W2, W3, seperated by tokens. So the tokens are the set of tokens are  {W1,W2,W3,W4} and the sequence of tokens are {W1,W2,W3,W4,W2,W3}.
2. Stop words:- The words inluded as per NLTK library like of,if,etc ...
3. Word:- Any token which isn't a stop word.

## Features

### Common words

1. CWC_MIN:- It is the ratio of the common word count to min length of word count of Q1 and Q2. common_word_count/min(len(Q1_words),len(Q2_words)).
2. CWC_MAX:-It is the ratio of the common word count to max length of word count of Q1 and Q2. common_word_count/max(len(Q1_words),len(Q2_words))

The two features took the ratio of common word count in minimum and maximum.

### Common Stopwords

1. CSC_MIN:-It is the ratio of the common stopwords count to min length of stopword count of Q1 and Q2. common_stopword_count/min(len(Q1_stopwords),len(Q2_stopwords)).
2. CSC_MAX:-It is the ratio of the common stopwords count to max length of stopword count of Q1 and Q2. common_stopword_count/max(len(Q1_stopwords),len(Q2_stopwords)).

These two features took the ratio of common stop words count in minimum and maximum

### Common Tokens

1. CTC_MIN:-It is the ratio of the common Tokens count to min length of tokens count of Q1 and Q2. common_stopword_count/min(len(Q1 Tokens),len(Q2 Tokens)).
2. CTC_MAX:-It is the ratio of the Tokens  count to max length of tokens count of Q1 and Q2. common_stopword_count/max(len(Q1_Tokens),len(Q2_Tokens)).

These two features took the ratio of common tokens count in minimum and maximum

### Last Word or First Word

1. First_word_eq:- Check if first word of both the questions are equal or not. Its a boolean value indicator
2. Last_Word_eq:-Check if last word of both the questions are equal or not. Its a boolean value indicator

These two features can be helpful to find similar questions by narrowing down the huge pool of options.

### Length features

1. abs_len_diff:- The absolute length difference between the length of q1 tokens and q2 tokens
2. mean_length_diff:- average token length of Q1 and Q2

Many times similar sentences/questions are of same lengths too.

### Fuzzwuzzy based features

This library was devloped such that given two sentences, measure some sort of similarity between the sentences based on the words in the sentences.

Refer:-https://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/

1. fuzz_ratio:-Suppose we have two sentences. One way to check the similarity is by edit distance i.e. by addiding or deleting or shifting of alphabet. The edit function score is small if we can construct a new sentence from original sentence making a very few edits. So if the number of ways we can do the edit function is very low then the similarity must be very high.
2. Fuzz_partialRatio:- the ratio doesn't work very well when we have a substring missing but we humans mean the same thing a sentence like New York Yankees and simply Yankees even though they both mean the same thing. So if a substring matches this function should give a high score.
3. Token_sort_ratio:- When we make the substings in a different positions we get a differnt score even thos they are the same. So what tokens sort will do is, it will take a sentence, break up the sentence into indivisual tokens and sort them. After that take fuzz ratio and find the token sort ratio.
4. Token_set_ratio:- When the two sentences are the same but of different length then we find out the sorted intersection of tokens (T0),  sorted intersection of tokens + sorted rest of words of Q1(T1) and sorted intersection of tokens + sorted rest of the words o Q2(T2). find the fuzz ratio of (t0,t1), (t1,t2) and (t0,t2) and find give the highest output.

### LCS

LCS_ratio:- ratio of length of longest common substring to min kength of token count of Q1 and Q2.

## Analysis of features extracted

### Word cloud

Often times in machine learning NLP classifications problems, there are certain words which will occur more in label 0 compared to label 1 and vice versa and word cloud is the perfect way to visually see the same thing.


The size of the word in the word cloud resembels the frequency.

So we see words like Donald Trump, best way occur, etc most often in the  duplicate pairs compared to words like India, difference, etc occur most often in non duplicate pairs.

We can do some feature engieering based on this like BOG, TFIDF, w2vtfidf, etc.

### Pair Plot

Observations:

1. More of class label 1 occuring when ctc min is larger
2. csc min and ctc min has partially seperability.
3. csc min and token sort ratio has partial seperability
4. When token sort ratio is lower, there is a bigger chance of the questions being not duplicates.

### Token Sort Ratio(Feature)

#### PDF:-

See can see that class 1 points tends to have a larger value of token sort ratio compared to class 0 points.

#### Violin Plot:-

The violin plot shows the there is some seperability between class 1 and class 0 points in the token sort ratio feature as the plots dont fully overlap.

### Fuzz Ratio (Feature)

#### PDF:-

When we have a larger value of fuzz ratio we see that more points belong to class 1 compared to class 0

#### Violin Plot

The violin plots are not completly overlapping which shows that it has some seperability.



# TFIDF Weighted Word Vectors

From word cloud we saw that some words occur more in class 1 compared to class 0 and vice versa. 

Like some of the political names like Clinton, Trump, etc occured more for duplicate pairs and some words like India, difference occured more for Non duplicate points. 

So constructing text based words features can be benificial.

We willbe using Glove insted of W2V to calculate the w2v representatios of the text.


TFIDF is calculated from the sklearn libraries 

For W2v we use glove model which comes packed with spacy library  spacy pretrained and calculate the tfidf weighted w2v by just multiplying the vec value and the idf value.
