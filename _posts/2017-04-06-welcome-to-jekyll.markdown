---
layout: post
title: "Sparkify - Customer Churn Prediction Using Apache Spark"
date: 2020-01-19 20:58:20
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. 

# Add post description (optional)
img: sparkify.jpeg
---

Customers are the lifeblood for any business organisation. All businesses are dependent on customers . In today’s hyper-competitive world , it is very crucial for businesses to strive towards keeping their products relevant in order to keep customers happy. Organisations are increasingly following the “customer obsession” mantra.

It is well known statistic that, acquiring a new customer can cost approximately five times more than retaining an existing customer. Also, retaining existing customers can increase profitability significantly. The increased cost is due to spending that the company has to do on market research , lead generation advertising, follow up , direct sales and many other such activities. Thus companies find retaining customers more valuable than acquiring new ones. Though, acquiring new customers never hurts !In such a scenario, predicting customer behavior in advance ,helps companies flag customers, who are more likely to leave.



# Problem Statement
In this project, we have to create a model which proactively predict customers who are more likely to churn. The data contains behavioral information of users from a fictitious music app company , Sparkify. Predicting such customers well in advance, will help in targeting them with incentives and offers , in order to retain them.In this analysis, I built the model using a subset of the data(~128 MB) .I have used PySpark , which allows us to work with RDDs in Python language.

# Exploratory Data Analysis
In the data preprocessing step, I find explore the meaning of every column and search for any missing values. The printSchema function helps us view the various columns and its types.

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn1.jpg)

On further investigation, I find that there are null values for userId and sessionId columns. These values were null because the user was either logged out or not registered on the app. Null values for these columns are not helpful in our analysis, so I remove them.Further, I analysed various behavioral differences between the churn and non-churn user group. This was an important step before finalizing the features that I would be using for modelling purpose.

# Feature Engineering
I came up with following 7 features, to create our prediction model

1.Time spent by users of both groups listening songs

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn2.jpg)

2.Number of thumbs up

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn3.jpg)

3.Number of thumbs down

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn4.jpg)

4.Number of songs played

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn5.jpg)

5.Number of songs listened per session per user

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn6.jpg)

6.Number of days since registration

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn7.jpg)

7.Average number of active days

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn8.jpg)

Looking at the above features, we can observe significant behavioral differences between the churn and non-churn group.

# Modelling
After creating the features, I aggregated all of them at userId level. Then , I split the dataset into training and validation set.
I split the data into 2 parts : 90% for training and 10% for validation
Then I used the Cross-Validator method because it helps us try out various hyper-parameters and automatically select the best ones.
I trained 3 models : Logistic Regression, Decision Tree Classifier and Random Forest Classifier.

# Evaluation
Among the 3 models I trained , following are the obtained F1 score for each model. In our dataset, churned users(23%) are lesser in number than non-churned users(77%). Using accuracy as evaluation metric, will not give a good performance, because any model predicting “no-churn” will have good accuracy . Instead, I use F1 score as the evaluation metric. F1 score gives a balanced score between precision and recall. F1 score is defined as :

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn9.jpg)

F1 score
Logistic Regression Model ( F1 Score : 0.766)

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn10.jpg)

Decision Tree Classifier( F1 score : 0.642 )

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn11.jpg)

Random Forest Classifier (F1 score : 0.858)

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn12.jpg)

# Conclusion
Finally, I decided to go with Random Forest Classifier model as it gave the best F1 score. I also looked at the feature importances. The most important feature turned out to be : Number of active days.

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn13.jpg)

This model can be further improved by:
* Creating more number of features
* Training on a larger dataset, by deploying on cloud(AWS, IBM cloud)
* Tuning more number of hyperparameters

For complete analysis visit: https://github.com/Mikewortho/SparkifyCustomerChurn :)
