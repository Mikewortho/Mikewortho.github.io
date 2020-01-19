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


You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
