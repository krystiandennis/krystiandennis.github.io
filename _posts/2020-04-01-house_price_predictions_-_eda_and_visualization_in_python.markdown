---
layout: post
title:      "House Price Predictions - EDA and Visualization in Python"
date:       2020-04-01 20:07:48 +0000
permalink:  house_price_predictions_-_eda_and_visualization_in_python
---


To be honest, visualizations are the main reason I chose to become a data scientist. I confess, I never read an article. I go straight to the infographics. They tell the whole story. If I can "see" the data, I can understand it.

For my first data science project for Flatiron School Online Data Science Boot camp, I analysed a data set for home sales in King County, Washington. The data set included information for sales between Sept. 2014-Sept. 2015. We were given information like square footage of living space, number of bedrooms, and even longitude and latitude for over 21,000 homes.

![](https://imgur.com/MQJtXPc.jpg)

Home for sale in King County, WA from point2homes.com

I followed the [CRISP](https://www.ibm.com/support/knowledgecenter/en/SS3RA7_15.0.0/com.ibm.spss.crispdm.help/crisp_overview.htm) method for data mining and first took a look at my data set to make sense out of it. Once I had cleaned the data and completed feature engineering, I used Matplotlib and Seaborn to create visualizations of the dataset. I used pairplots, scatterplots, heatmaps, catplots and regplots to name a few. I am brand new to this, so I played around to find what worked best to accurately represent the data. I also played around colors and learned about html hex strings and matplotlib colormaps.
For my exploratory data analysis (EDA) I chose three variables from the dataset and examined how they affect the sales prices of homes.

**1. How does square footage affect sales price?**

In the dataset, there were several measures of square footage includes in the variables. I used the 'sqft_living' variable because it includes both above ground and basement square footage. I used a regplot for this visualization.

![](https://i.imgur.com/z8AYE20.png)

![](https://i.imgur.com/qp2958q.png)
Not only did I find out that 'sqft_living' seems to have a strong linear relationship with 'price', but I used two html hex string colors. The data points are #FF69B4, also known as hot pink! My regression line is #00FFFF, or cyan.

**2. How does grade relate to price?**

The King County government created a grading system to rank all the home sales in the county. I used a catplot to see how this grading system affected the sales price of homes.

![](https://i.imgur.com/QSjwGoI.png)

![](https://i.imgur.com/Q7fTqDq.png)

Fortunately, Seaborn knows my heart. This catplot is rainbow colored all by itself. I can also see a clear linear relationship between 'grade' and 'price'. If a home received a grade of less than 6, it did not sell for over $100,000.

**3. How do longitude and latitude impact price?**

I used a scatterplot to visualize the connection between 'lat', 'long' and 'price'. This virtually allowed me to see how location in King County is reflected in the sales price of a home.

![](https://i.imgur.com/KiSuEJn.png)

![](https://i.imgur.com/fwrg1qN.png)

From the scatterplot, I can see that homes located in northeastern King county tend to have a higher sales price, as most of the purple and red data points are in the top half of the plot. It was later confirmed by correlation and regression that 'lat' has a stronger impact than 'long' on sales price. I also changed the matplotlib colormap to "gist_ncar". The vivid color array allows for the difference in price point to be clearly seen.

Using Matplotlib and Seaborn to create visualizations of the dataset helped me get an understanding of how the predictor variables impact price. The visualizations helped me to answer important questions about the dataset and determine which variables to include for analysis.
