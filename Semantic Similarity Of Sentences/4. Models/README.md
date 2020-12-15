# Machine Learning and Deep Learning Models

## Loading Data

We read the data from file and use sqllite to store the data into sqltable,

Sqllite is one og the most used embedded data based in the world used in Android, Iphones, macbooks, etc.

What is the target to achive here is that I can work with different kinds of file formats be it csv or database files as it will never be fixed in the real world senarious.

We can use SQL quiers in pythons inbuild sqllite.

Random splitting is used here as was discussedin train test formulation has we have ni timestamp based features to do time based splitting which could have been more better

## Random Model for base line of logloss

As we have logloss as metric of evaluation, we know the min logloss is 0 but we don't know what is the maximum logloss as it is [0,inf) so we build a random model for worst case of logloss given the data.

We can just use that as a base score.

so now the range is narrowed doen to [0,random_model_score)

Got a score(logloss) of 0.8872
