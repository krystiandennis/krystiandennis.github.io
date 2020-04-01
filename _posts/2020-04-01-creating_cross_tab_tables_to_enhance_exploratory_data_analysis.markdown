---
layout: post
title:      "Creating Cross tab Tables to Enhance Exploratory Data Analysis"
date:       2020-04-01 15:46:31 -0400
permalink:  creating_cross_tab_tables_to_enhance_exploratory_data_analysis
---


For my Capstone Project at Flatiron School's Online Data Science Boot Camp, I created a model that will predict whether a customer will book with Marriott Hotels directly, or with an online travel agency, based on tweet sentiment. The project was a massive undertaking, and truly did require me to call on every skill I'd learned during the boot camp.
It also made me learn a few new tricks, too! So far, I had never created a cross tab table. I wanted to create a percent stacked bar graph, which I'd also never done, so I needed to calculate the percentage of positive, neutral and negative tweets across all six classes of tweets.

```
all_data['Sentiment_Type'] = all_data['Sentiment_VADER'].apply(lambda x: 'Positive' if x > 0 else
                          ('Negative' if x < 0 else 'Neutral'))
```

once I created the sentiment type variable I created a cross tab table the showed these counts.

```
print('Count by Sentiment Type\n')
counts = pd.crosstab(index=all_data["Sentiment_Type"], 
                            columns=all_data["Class"],
                             margins=True)   # Include row and column totals
counts.columns = ["Booking.com","Expedia","Luxury","Premium","Priceline","Select","row_total"]
counts.index= ["Negative","Neutral","Positive", "col_total"]
counts
```

![](https://imgur.com/U3MSLnu.jpg)
Jazzed up output using PowerPoint

Next, I needed to convert these counts into percentages. To do that, I divided all of the counts by the column total.

```
print('Percentge of Tweet Sentiment Type\n')
counts/counts.ix["col_total"]
```

![](https://i.imgur.com/qiSbEis.png)
Jazzed up output using PowerPoint

Once I had the percentage of tweet sentiment by class, I could create a percent stacked bar graph.

```
pos = np.array([70.54, 58.22, 58.43, 55.56, 58.25, 54.97])
neu = np.array([22.27, 31.31, 32.58, 23.42, 21.36, 27.51])
neg = np.array([7.19, 10.47, 8.99, 21.03, 20.39, 17.53])
classes = ['Luxury', 'Premium', 'Select-Service', 'Expedia', 'Priceline', 'Booking.com']
ind = [x for x, _ in enumerate(classes)]
total = pos + neu + neg
proportion_pos = np.true_divide(pos, total) * 100
proportion_neu = np.true_divide(neu, total) * 100
proportion_neg = np.true_divide(neg, total) * 100
plt.rcParams['figure.figsize'] = [20, 12]
plt.bar(ind, pos, width=0.8, alpha=0.7, label='Positive Tweets', color='#9D33FF', bottom=proportion_neu+proportion_neg)
plt.bar(ind, neu, width=0.8, alpha=0.7, label='Neutral Tweets', color='#33FF9D', bottom=proportion_neg)
plt.bar(ind, neg, width=0.8, alpha=0.7, label='Negative Tweets', color='#FF9D33')
plt.xticks(ind, classes, fontsize=18)
plt.ylabel("Percentage of Tweets\n", fontsize =20)
plt.xlabel("\nClasses", fontsize =20)
plt.title('Distribution of Sentiment by Classes\n', fontsize = 24)
plt.ylim=1.0
plt.legend(loc='best',fontsize = 20)

# rotate axis labels

plt.setp(plt.gca().get_xticklabels(), rotation=45, horizontalalignment='right')
plt.show()
```

The code above created the following Percent Stacked Bar Graph, my first ever!
![](https://imgur.com/Aad9nZ2.jpg)

Looks good to me! I want to show the corresponding percentage in the future, and even graduate to making interactive plots using plotly. I'm off to a good start. I learned so many mew skills during my capstone project, and in the Flatiron School Boot Camp overall. Glad I could share with you how to create a graph like this for your projects.
