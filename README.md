# Recommendation System



# Objective

This recommendation system is made to help users, based on user ratings on each food item, select the best fit for themselves and to stimulate sales and increase profits

# Summary

The problem we are going to solve is how to help users select products which they may like and to make recommendation to stimulate sales and increase profits. Firstly, we decided to choose the Amazon Fine Food Reviews dataset which consists of 568,454 food reviews Amazon users left up to October 2012 as our dataset. Secondly, our recommendation system is based on users rating prediction. We assume that users tend to like the products that have a score of greater than 4 and we will consider the highest 5 scores product as our recommendation candidates. Thirdly, we implemented several algorithms to predict the scores of each product for each user.

In this report we implemented the following models to build a recommendation system based on data from Amazon Fine Food Reviews : Matrix Factorization, SVD, Random Forest and Times Series. Our main assumption is that for a certain user, the higher review score is, the more likely the article should be recommended. We tried to compare different methods to establish a more reasonable and reliable system. Performances of the models are evaluated using MSE for the score and Confusion Matrix for recommendation or not. Below is the architecture of our recommendation system.

# Dataset

Amazon Fine Food Review
https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews


# Dataset Description

- Reviews from Oct 1999 - Oct 2012
- 568,454 reviews
- 256,059 users
- 74,258 products
- 260 users with > 50 reviews


# Data columns (10 columns)

- Id
- ProductId
- UserId
- ProfileName
- HelpfulnessNumerator
- HelpfulnessDenominator
- Score (1~5)
- Time
- Summary
- Text

### We used 'ProductId', 'UserId', 'Score' and 'Text'


# Recommendation System

## Models

### 1. Distance Based (Content-based)

Get the similarity between the given product and other products. Set the similarity as a standard and get n products
![content](https://user-images.githubusercontent.com/87661298/204401976-cd62a800-065e-48cb-9dcc-f644901e60b3.png)


### 2. SVD

Use a matrix with scores from users about items. Then predict the target user score to unevaluated items and recommend the highest estimated scored items.
![SVD](https://user-images.githubusercontent.com/87661298/204401403-8f5731c6-a28d-43ea-a5c1-e3aeab5ec86e.png)


### 3. Matrix Fatorization

Split the rating matrix which are ratings that user gave to items, into 'user latent matrix' and 'item latent matrix'. First initialize with random values. By using Gradient Descent method, minimize the error and update weight. Recommend the final top n items.
![MF](https://user-images.githubusercontent.com/87661298/204401425-e7b4f591-ab3a-4338-bb0d-9f6dd6a3e8b7.png)
***
![그림1](https://user-images.githubusercontent.com/87661298/204401649-f6d29064-128e-4d75-9d81-b7887b1a3e94.png)

# Function Definition
