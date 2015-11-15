---
title       : Yelp Challenge Project
subtitle    : Capstone Project - Coursera Data Science Specialization
author      : David Álvarez
job         : 
framework   : impressjs        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax, bootstrap]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
--- 
# Yelp Challenge Project
## Review Rating Prediction
Author: *David Álvarez*



--- .slide x:1000 y:0 scale: 1

# Yelp Challenge data description

The Yelp company gathers reviews from users attending to restaurants, clinics and other services.

Each review contains a star rating that is given by a user to the rated business.

![Yelp Logo](assets/yelp-logo.jpg)

# Project description

Can we predict the rating of a review looking at its text?

We present the implementation of **a prediction function for star-rating based on machine learning**

--- .slide x:1000 y:2000 scale:2
# Exploratory analysis

The data used for this project is available [here](https://d396qusza40orc.cloudfront.net/dsscapstone/dataset/yelp_dataset_challenge_academic_dataset.zip):











<img src="assets/fig/text_length-vs-star_rating-1.png" title="plot of chunk text_length-vs-star_rating" alt="plot of chunk text_length-vs-star_rating" style="display: block; margin: auto;" />


```r
ct <- cor.test(log(textLengths), stars)
```

Since the p-value of the correlation test is 0, there is no relation between text length and rating. 

--- .slide x:6000 y:6000 scale:5 rot:45
# Prediction modelling

1) Split texts into sentences.  

2) Clean stopwords, numbers, punctuation, word sufixes and sort words without duplicates.  
3) Count words + sentence rating:  




```
##           word count stars avg.stars
## 4975   horribl    24    28  1.166667
## 5260    orbitz     6     7  1.166667
## 3     favorite  1496  6488  4.336898
## 94   delicious  1573  6648  4.226319
```

4) Prediction of a sentence is a weighted sum: 

$$predict(sent) \gets \frac{\sum_{w\in sent}w.count * w.avgStars}{\sum_{w \in sent} w.count}$$

--- .slide x:4000 y:1500 scale:1 rot:200
# Results and Discussion











Predictions errors have $\mu$ = -0.0067505 and $\sigma$=1.3158128. 

RSME is 1.3158202. 

Prediction model tends to be *too optimistic*.

<img src="assets/fig/error_histogram-1.png" title="plot of chunk error_histogram" alt="plot of chunk error_histogram" style="display: block; margin: auto;" />

**Improvements**: gather sets of words or sentences, cross validation, `tm` package, etc.

#### Further info, in https://github.com/davizuku/datascience-capstone
