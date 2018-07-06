---
layout: post
title: Steam Webscraping and Linear Regression Project
description: project blog post
image: assets/images/pic06.jpg
---

Tools used for webscraping: Python, pandas, Selenium, beautifulsoup, fuzzywuzzy.

Tools used for linear regression: Python, pandas, statsmodels, scikitlearn, matplotlib, seaborn.

The repository for this project is here: [https://github.com/Jack-Etheredge/Steam-Webscraping-Linear-Regression](https://github.com/Jack-Etheredge/Steam-Webscraping-Linear-Regression "Github Repo: Steam Webscraping and Linear Regression Project - Jack Etheredge")

I scraped Steam and steamDB data for every video game available for purchase through Steam and then performed linear regression to predict the number of concurrent users. This was done using Selenium and Python. Many Python packages were used including pandas, seaborn, stats models, scikitlearn, fuzzywuzzy.

I used a combination of Selenium webdriving and beautiful soup to scrape the data.

I've included the scraped data in the repo: [steam_games_dicts_selenium.json from Steam](https://github.com/Jack-Etheredge/Steam-Webscraping-Linear-Regression/master/steam_games_dicts_selenium.json) and [steam_users_table.csv from SteamDB](https://github.com/Jack-Etheredge/Steam-Webscraping-Linear-Regression/master/steam_users_table.csv).


# Variables collected for each videogame included:

Price

Discounted Price

Number of overall reviews

Number of recent reviews

Percentage of positive overall reviews

Percentage of positive recent reviews

ESRB Rating

User-defined tags

Genre(s)

Publisher(s)

Developer(s)

Release Date



# Linear regression:

I attempted to predict peak concurrent users scraped from SteamDB using these independent variables.

Linear regression models were made using ordinary least squares, select k-best features, and both lasso and ridge regularization.

Ultimately, ridge regularization performed the best so far.


I summarized the process of acquiring and modeling this data in [this talk](https://github.com/Jack-Etheredge/Steam-Webscraping-Linear-Regression/master/Steam_Linear_Regression.pdf).

It seems likely that the negative coefficients for oculus and VR user tags are due to the relatively low adoption of these types of games so far. There is still a high monetary barrier to entry for these games due to the cost of VR systems, particularly the oculus rift, and these systems are still relatively new for widespread adoption.

# Updates (06-07-18):
I've since updated this to use data from the entirety of Steam's videogame collection and predict the number of overall reviews (which I'm treating as a good proxy for the number of unique owners). I have 85% predictive power in log space and 65% predictive power is retained if I remove the Metacritic score and the percentage of reviews that are positive.

#### To do:

Add picture of plots.

Add the narrative from the presentation.

Upload an updated version of the talk.
