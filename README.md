# Term-Project
Machine-Learning Final Term Project - Recommendation System



# Objective

This recommendation system is made to help users, based on user ratings on each food item, select the best fit for themselves and to stimulate sales and increase profits


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

### Distance Based (Content-based)

Get the similarity between the given product and other products. Set the similarity as a standard and get n products
![content](https://user-images.githubusercontent.com/87661298/204401976-cd62a800-065e-48cb-9dcc-f644901e60b3.png)


### SVD

Use a matrix with scores from users about items. Then predict the target user score to unevaluated items and recommend the highest estimated scored items.
![SVD](https://user-images.githubusercontent.com/87661298/204401403-8f5731c6-a28d-43ea-a5c1-e3aeab5ec86e.png)


### Matrix Fatorization

Split the rating matrix which are ratings that user gave to items, into 'user latent matrix' and 'item latent matrix'. First initialize with random values. By using Gradient Descent method, minimize the error and update weight. Recommend the final top n items.
![MF](https://user-images.githubusercontent.com/87661298/204401425-e7b4f591-ab3a-4338-bb0d-9f6dd6a3e8b7.png)
***
![그림1](https://user-images.githubusercontent.com/87661298/204401649-f6d29064-128e-4d75-9d81-b7887b1a3e94.png)
