---
layout: post
title: Fifa 19 Analysis
date: 2020-01-18 21:32:20 +0000
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: eafifa.jpeg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [FIFA,Analysis,Sports]
---
FIFA 19 is a football simulation video game developed by EA Vancouver as part of Electronic Arts’ FIFA series. As a football fan and game player, I wrote this blog post to perform some data exploration on FIFA 19 Player Dataset from Kaggle.
The dataset contains information of all 18207 players from the latest edition FIFA 19. There are 89 attributes including personal information like age, name, nationality, photo, club, wage, etc, and also player skill information like ball control, dribbling, crossing, finishing, GK skills and etc.

I will focus on the three questions below:
Q1: What’s the ratio of total wages/ total potential for clubs. Which clubs are the most economical ？
Q2: What’s the age distribution like? How is it related to the player’s overall rating?
Q3: How is a player’s skill set influence his potential? Can we predict a player’s potential based on his skills’ set?

## Q1: What’s the ratio of total wages/ total potential for clubs. Which clubs are the most economical ？
First I would like to look at the data at the clubs’ level. There is a total of 651 clubs collected and on average 27.6 players for each club. So which of the clubs are richest among them and which are more cost-effective？
To find answers to the first question, we can take a look at the wage/potential ratio for each club. The higher the ratio is, the more willingly a club spends money on high potential players.
On average, clubs spend €140 on wage for every potential of their players. So for a common player with 50 potential, his club will pay €7000 every year.

![Top 10 Clubs]({{site.baseurl}}/assets/img/download.jpeg)

But it’s obvious that ‘Giant’ clubs are willing to pay much more on their players. Take Real Madrid for example, they have the highest ratio here even after Christiano Ronaldo transferred to Juventus. And this ‘money policy’ ensure them to stay very competitive: three times EUFA Champions League title in a row, king of Europe.

![Top 10 Economical]({{site.baseurl}}/assets/img/top10econ.jpeg)

But when I take a look at bottom of ratio list, it’s a surprise that some club names are quite familiar to us. Like AEK Athens, Dynamo Kyiv, Shakhtar Donetsk, they all made impressive performance on UEFA Champions League. My guess is that bad economic situation in their countries leads to low wage for players.

## 2. What’s the age distribution like? How is it related to the player’s overall rating?
![Age Distributions]({{site.baseurl}}/assets/img/agedistribution.jpeg)

From the above plot, we can see that most players are between 20–26 years old. And players’ number starts to decrease after 26 years old and speed up after 30. The reason behind this could be that many young players didn’t get enough opportunities to prove themselves and give up their dream as a football player.

When a football player reaches their late 20s, they have gained enough experience and reaches the peak of their rating. The golden era of a football player’s career starts here and ends when his age reaches 35. At this age, his physical body condition drops quickly so as for average rating. As a result, they retire as a professional football player. But many of them stay active in the field of football, in the name of the coach, management role, and etc.
There are also quite a few numbers of players with age over 37, 38 years old. This is quite a surprise especially their rating still can remain quite high. We should pay respect to their undying love for football.

## 3. How is a player’s skill set influence his potential? Can we predict a player’s potential based on his skills’ set?
At last, I wonder if there might factors that determine a player’s potential so I built a model to help us in predict the player’s potential. I have used all of the player’s skill features as well as features like age. The model performs quite well since the r2 score is 0.87 on the test set.

![Coefficients]({{site.baseurl}}/assets/img/coefficients.jpeg)

As shown above, the potential of a player is mainly determined by his ball control, reaction, and age. Young players with excellent ball control and fast reactions tend to give us an outstanding performance in a football match.

## Conclusion
In this blog post, we explored FIFA 2019 player dataset from Kaggle and got some interesting findings.
We found that money plays a crucial part in a club’s performance. The ‘Giant’ clubs are willing to spend much more money on their players.

There were quite a few football players didn’t continue their career after 26 years old. This is quite a cruel number which reflects how competitive this profession is. But there was also player even more than 40 years old. True love prevails!
Ball control, reaction, and age are the main attributes determine a player’s potential. So if you are playing FIFA 19 and try to get some potential players for your own club, focus on these three.

To see more about this analysis, see the link to my Github available here.
