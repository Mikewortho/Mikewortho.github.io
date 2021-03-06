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

![Churn Or Not]({{site.baseurl}}/assets/img/churnvnchurn.jpg)

As we can see from the above boxplots, differences emerge between the two groups of churned and non-churned users.Generally, churned users have added less friends, added lesser songs to playlist, witnessed lesser errors which could be due to lesser engagement, given lesser thumbs up, thumbs down , asked for less help and listened to lesser songs. We can therefore utilise these observations when creating features for our model.


# Feature Engineering
Upon conclusion of the exploratory data analysis I decided that the following 7 features would allow us to create a powerful predictive model; as follows:

1.Time spent by users of both groups listening songs

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn2.jpg)

>The aforementioned is likely to be one of the most indicative features - the hypothesis here being the more the user listens to music and makes use of their subscription service the more likely they are to remain.

2.Number of thumbs up

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn3.jpg)

>With this feature it will be interesting to see if we can see a correlation between the users level of enjoyment for the artists/songs and remaining an active subscriber.

3.Number of thumbs down

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn4.jpg)

>Similarly to the previous feature - if a user has a large distaste for the artists and songs he has so far heard, will this cause him to have a higher chance of leaving the streaming platform?

4.Number of songs played

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn5.jpg)

>Here we would expect the non-churned user to have recorded a significantly higher number of plays. The theory being that higher engagement = higher product affinity = more chance of remaning an active subscriber.

5.Number of songs listened per session per user

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn6.jpg)

>Much akin to the previous feature - the more time per session indicates the user is having fun with the product each and every time they use it. Higher affinity = more chance of remaning an active subscriber.

6.Number of days since registration

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn7.jpg)

>This I beleive would be interesting to see - as it would be potentially be quite a powerful indicator for our models if churn users have such stark differnce to non-churn users. 

7.Number of added friends

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn8.jpg)

>Much akin to the first engineered feature. I beleive this will be a very indicative feature, the more added friends indicates a willingness to share their excitement about the product with those closest to them. Thus shows a higher affinity for the product from the user. As such high affinity to a product would usually indicate non-churn, in contrast low levels of affinity would indicate churn.


# Modelling
After creating the features, I aggregated all of them at userId level. Next, before training the model, it was necessary to put all the features into vectors. When putting data into vectors, it was possible that some features may be string types and as such should be checked and converted to float if necessary.

Furthermore, although it does not affect tree based models, standardization is important for linear models. As such I decided to standardize the data.

Then , the data was ready to be split into a training and validation set. 90% for training and 10% for validation.
Finally the data was ready to be presented to our three chosen classification models:
Logistic Regression, Decision Tree Classifier and Random Forest Classifier.

>The Cross-Validator method was implemented within each - allowing us the functionality to test out various hyper-parameters and automatically select the best fit.


# Results
In our dataset, churned users(23%) are lesser in number than non-churned users(77%). Due to the imblanaced nature of the data using accuracy as an evaluation metric, will not give good performance, because the models will tend to over-fit to the “non-churn” category. Instead, a more relevant evaluation metric is known as the F1 score.The F1 score gives a balanced score between precision and recall. It can be defined as follows:

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn9.jpg)

Among the 3 models, the following are the obtained F1 score for each model.

Logistic Regression ( F1 Score : 0.766)

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn10.jpg)

Decision Tree Classifier ( F1 score : 0.642 )

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn11.jpg)

Random Forest Classifier (F1 score : 0.858)

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn12.jpg)

I had anticipated a straight shootout between Logistic Regression and Random Forest Classifier for this particular project. This is due to the fact that we would have expected the random forest classifier to beat the decison tree classifier as decision trees are quite prone to overfitting and on an imbalanced dataset this presents issues. Ideally, we would like to minimize both error due to bias and error due to variance. Enter random forests. Random forests mitigate this problem well. A random forest is simply a collection of decision trees whose results are aggregated into one final result. Their ability to limit overfitting without substantially increasing error due to bias is why they are such powerful models.

As we can see this has been proven with the Random Forest Classifier performing the best - with an F1 Score of 0.858. As such we chose this model to move forward for hyperparameter tuning.

We chose to tune on the following variation of parameters:
* Max Depth = [5,8]
* Min Instances Per Node = [1,4]
* Num Trees = [20,40]

![Hyper]({{site.baseurl}}/assets/img/hyper.jpeg)

As you can see from the above code snippet - the optimal model suggested:
* Max Depth = [5]
* Min Instances Per Node = [1]
* Num Trees = [20]

However the optimal model did not manage to improve the results, as such the scores associated with the final output being recorded as follows:

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn12.jpg)

Perhaps a larger gridsearch of possible parameter variations in the future may provide more fruitful results, however this is for another re-visit of the project.

# Conclusion
During this project we have worked through a variety of issues, loading and cleaning the dataset - checking for missing and null values and dealing with them appropirately. We then performed our exploratory data analysis which included a correlation analysis of the variables allowing us to percieve which variables would would have significant impact within our final model choices. Furthermore, we directly compared variables of 'churn' and 'non-churn' users to illustrate key variables which would be useful during our feature engineering. From this we managed to engineer 7 variables ready to input into the models. After lengthy research into viable classification models it was decided a direct comparison of 3 models would be an interesting choice: Logistic Regression, Decision Tree Classifer and Random Forest Classifier were selected. Of the 3 base models the Random Forest Classifier performed the best and as such was chosen to tune the hyperparameters further. Thus providing us with our final Random Forest Classifier.

Upon final exploration of the model coefficients the most powerful feature turned out to be: Number of active days. Something we had suspected in our exploratory data analysis.

![PrintSchema EDA]({{site.baseurl}}/assets/img/churn13.jpg)

This model can be used by the company to flag users who are more likely to churn and thus ,entice them with special offers and discounts in order to retain them. The above analysis can be more robust when used on the complete dataset. Moreover, adding more feautures may or may not improve our analysis, this is another avenue for exploration. To formally conclude, I enjoyed all aspects of this project, data preprocessing, exploratory analysis, feature engineering, modelling and then hyperparameter tuning. During this project I have enhanced my skillset with PySpark. There is also still many aspects to improve or further investigate - why not explore some of the below:

* Creating more features
* Training on a larger dataset, by deploying on cloud(AWS, IBM cloud)
* Tuning more variations of hyperparameters

For complete analysis visit: https://github.com/Mikewortho/SparkifyCustomerChurn :)

<a href='https://ko-fi.com/N4N31LFEY' target='_blank'><img height='36' style='border:0px;height:36px;' src='https://cdn.ko-fi.com/cdn/kofi1.png?v=2' border='0' alt='Buy Me a Coffee at ko-fi.com' /></a>
