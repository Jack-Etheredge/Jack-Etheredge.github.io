---
layout: post
title: Project Guten-Bag-of-Words
subtitle: project blog post
thumbnail-img: assets/images/patrick-tomasso-71909-unsplash.jpg
---
[Project Gutenberg][gutenberg_link] is a wonderful service providing free access to books with expired copyrights. However, very little information beyond the author and title are typically available through the site. This motivated me to use unsupervised machine learning in the form of natural language processing (NLP), dimensionality reduction, and clustering to generate genre groupings, make similar book recommendations, and visualize narrative patterns for these books.

I made a dash app that performs several functions using the [Project Gutenberg][gutenberg_link] books:
- Suggests 5 books in the same subgenre
- Gives you words that are associated with that subgenre (loosely; it's based on that maximum topic in the cluster, whereas a cluster is a more direct approximation of subgenre)
- Shows a sentiment trajectory of the narrative, which is an approximation of Vonnegut's story arcs (actually an older idea that was further popularized by Vonnegut)
- Shows topic change over the course of the narrative and gives a "complexity" score based on the cosine distances between these topics

During the topic modeling for the app, here are some different things I tried and their effects:
* Dealing with contractions:
  - I found it odd and concerning to get "'t" in my vocab list, so I expanded contractions with a dictionary.
* Lemmatization vs not:
  - Lemmatization works well for both topic modeling and sentiment analysis
  - I found stemming too aggressive, so I didn't play with it much. If that was a big mistake, dear reader, please let me know.
* Countvectorizer vs TF-IDF:
  - I had better luck with TF-IDF, because it weights less common words more heavily.
* Maxdf vs stopwords:
  - I found that when I compared assigning stop words vs updating maxdf to be a bit stricter, those words were removed by maxdf anyway.
  - For me, the take home message is that it's easier, more effective, and more efficient to play with maxdf than to try adding a bunch of specific stop words.
* LDA vs NMF:
  - When reading about these two topic modeling methods in papers, it seems that LDA would work better, since it's basically just NMF with the Dirichlet prior.
  - That said, I tried both and had better luck with NMF.
  - It's not an apples to apples comparison, in truth, however, since LDA assumes
* Number of topics
  - My original intuition was to bloat up the number of topics to a really high number (~100) to give clustering some serious granularity to deal with.
  - I found that this was a bit too much, however. Once you get to really high dimensionality, everything seems equally (super far) away.
  - Instead, after trying a few topic numbers, it seems that around 25 topics was roughly ideal both for comparing books and for comparing sentences within books.
* Number of clusters
  - This one was a bit less optimized, but I went with 20 clusters. I think a bit fewer would work better to define sub-genres for Sci-Fi and Fantasy novels, but more is probably better once I eventually bring in all of the books on Gutenberg (>57000 English books).
* Different clustering types (Kmeans vs spectral)
  - I was surprised to get better performance out of Kmeans clustering than Spectral clustering, since spectral clustering is more flexible with respect to the patterns that it can cluster.

You can see the app here: [http://flask-env.svfvjqygqf.us-east-1.elasticbeanstalk.com/](http://flask-env.svfvjqygqf.us-east-1.elasticbeanstalk.com/).
You can see the R and Python notebooks as well as the code for the dash app here: [Github](https://github.com/Jack-Etheredge/Project-guten-bag-of-words/).

Next steps:
- Get a domain for the app or figure out how to run it on [http://jacketheredge.com](http://jacketheredge.com).
- Blog post about how to get the dash app deployed on AWS Elastic Beanstalk (I hit a few snags I'd like to spare people)
- Expand the books visualized to all the books (currently "just" ~2000 books from sci-fi and fantasy)
- Use word2vec to pull out archetypal characters (hero/protagonist, anti-hero, villain/antagonist, etc)

## Improving my past projects:
- For the Steam linear regression project, I predicted the overall review number rather than peak concurrent users. My predictive power is much greater in log space. I can predict with 85% accuracy the number of users in log space if we include the percentage of positive reviews and the metacritic score (which are the top coefficients). I retain 65% accuracy for predicting the number of users in log space when these features are not included. As such, we can dig into the coefficients and determine what types of games are most likely to be successful before they have any reviews.

[gutenberg_link]: www.gutenberg.org/
