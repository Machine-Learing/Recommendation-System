# Recommendation System



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

#Function definition

:- |
**
|<p></p><p><h1>**content\_recommender(productid, n\_of\_recomm)**</h1></p><p></p>|
| :-: |
|<p></p><p>content\_recommender – When you search for a product, it recommends the top N products that are similar to it with Tfid vectorizer and cosine similarity algorithm.</p><p></p>|
|**Parameters::**|
|<p>**productid : String*, default = None***</p><p>ID of the product to target </p><p></p><p>**n\_of\_recomm : Int*, default = None***</p><p>Number of similar products to be recommended </p><p>![](Aspose.Words.0c3b5d30-4adb-4b9a-ae5c-05fbdaf1864a.002.png)</p><p></p>|
|**Returns::**|
|<p>**data.loc[sim\_scores.index][['ProductId','Text']] : DataFrame**</p><p>Index, id, text of TOP N similar products</p>|

|<p></p><p><h1>**svdrec(table, factors)**</h1></p><p></p>|
| :-: |
|<p></p><p>svdrec – When you search for a user, it recommends the top N products that are similar to it with svd algorithm.</p><p></p>|
|**Parameters::**|
|<p>**table : Array*, default = table***</p><p>An array form of a matrix for items recommended by the user in the past.</p><p>**factors : int*, default = table***</p><p>An integer factor value required for SVD algorithm.</p><p>![](Aspose.Words.0c3b5d30-4adb-4b9a-ae5c-05fbdaf1864a.003.png)</p><p></p>|
|**Returns::**|
|<p>**pred\_mat : Array**</p><p>Using the SVD algorithm, the empty place of the existing matrix is filled and predicted matrix.</p>|
|**Methods::**|

|calculate\_mse(x)|Calculate mse and print train, test error |
| :- | :- |
|drawcm(y\_pred,y\_test =test ,title=' ')|Plot the confusion matrix|
|Rec(result, uid, n, rawId=False)|Recommend product ID with userID|

||
| :- |

|<p></p><p><h1>**MF1(data, factors, maxIter, LRate, GD\_end, plot)**</h1></p><p></p>|
| :-: |
|<p></p><p>MF1 – When you search for a user, it recommends the top N products that are similar to it with matrix factorization algorithm.</p><p></p>|
|**Parameters::**|
|<p>**data : Array*, default = z***</p><p>An array form of a matrix for items recommended by the user in the past.</p><p>**factors : Int*, default = 30***</p><p>An integer factor value required for matrix factorization algorithm.</p><p>**maxIter : Int*, default = 100***</p><p>Maximum number of trainings to apply to gradient descent.</p><p>**LRate : Float*, default = 0.02***</p><p>learning rate of trainings to apply to gradient descent.</p><p>**GD\_end : Float*, default = 1e-3***</p><p>The threshold at which gradient descent will stop.</p><p>**plot : Boolean*, default = False***</p><p>Whether or not to plot the results.</p><p>![](Aspose.Words.0c3b5d30-4adb-4b9a-ae5c-05fbdaf1864a.004.png)</p><p></p>|
|**Returns::**|
|<p>**P.dot(Q.T) : Array**</p><p>Using the matrix factorization algorithm, the empty place of the existing matrix is filled and predicted matrix.</p>|
|**Methods::**|

|calculate\_mse(x)|Calculate mse and print train, test error |
| :- | :- |
|drawcm(y\_pred,y\_test =test ,title=' ')|Plot the confusion matrix|
|Rec(result, uid, n, rawId=False)|Recommend product ID with userID|

||
| :- |


