# Recommendation System

| Week | 세미나 | 과제 |커리큘럼 내용 |
| ------ | -- | -- |----------- |
| 1주차 | ☑️ | ☑️ | iOS 기초, H.I.G를 통한 컴포넌트의 이해, 화면 전환 |
| 2주차 | ☑️ | ☑️ | Autolayout을 통한 기초 UI구성, Scroll View의 이해 |
| 3주차 | ☑️ | ☑️ | TableView, CollectionView, 데이터 전달 방식 |
| 4주차 | ☑️ | ☑️ | Cocoapods & Networking + 솝커톤 전 보충 세미나 |
| 5주차 |  |  |디자인 합동 세미나 |
| 6주차 |  |  |서버 합동 세미나 + 솝커톤  |
| 7주차 |  |  |클론 코딩을 통한 실전 UI 구성, Animation, 통신 보충  |
| 8주차 |  |  |e기획 경선 + 앱잼 전 보충

# Objective

This recommendation system is made to help users, based on user ratings on each food item, select the best fit for themselves and to stimulate sales and increase profits

# Summary

The problem we are going to solve is how to help users select products which they may like and to make recommendation to stimulate sales and increase profits. Firstly, we decided to choose the Amazon Fine Food Reviews dataset which consists of 568,454 food reviews Amazon users left up to October 2012 as our dataset. Secondly, our recommendation system is based on users rating prediction. We assume that users tend to like the products that have a score of greater than 4 and we will consider the highest 5 scores product as our recommendation candidates. Thirdly, we implemented several algorithms to predict the scores of each product for each user.

In this report we implemented the following models to build a recommendation system based on data from Amazon Fine Food Reviews : Matrix Factorization, SVD, Random Forest and Times Series. Our main assumption is that for a certain user, the higher review score is, the more likely the article should be recommended. We tried to compare different methods to establish a more reasonable and reliable system. Performances of the models are evaluated using MSE for the score and Confusion Matrix for recommendation or not. Below is the architecture of our recommendation system.

# Dataset

Amazon Fine Food Review
https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews

This dataset consists of reviews of fine foods from amazon. The data span a period of more than 10 years, including all ~500,000 reviews up to October 2012. Reviews include product and user information, ratings, and a plain text review. It also includes reviews from all other Amazon categories.

# Dataset Description

- Reviews from Oct 1999 - Oct 2012
- 568,454 reviews
- 256,059 users
- 74,258 products
- 260 users with > 50 reviews


# Data columns (10 columns)

- Id: row ID
- productId: Unique identifier for the product
- UserId: Unqiue identifier for the user
- ProfileName: Profile name of the user
- HelpfulnessNumerator: Number of users who found the review helpful
- HelpfulnessDenom: Number of users who indicated whether they found the review helpful or not
- Score: Rating between 1 and 5
- Time: Timestamp for the review
- Summary: Brief sumary of the review
- Text: Text of the review


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

| |
| --- |
|
**Data(dataset)**
 |
| Data – It preprocesses the input data set and returns the values of z, total\_u, total\_p, pid2PID, train, test, table, raw\_data. |
| Parameters:: |
| **dataset : String_, default = None_**** The path to the data file the user wants to use. Features that are not needed do not need to be deleted separately. ![](RackMultipart20221203-1-vhq3rt_html_4211d3a63e2d7c66.png)** |
| Methods:: |
| data\_clean(df, features, m) Select datadata\_clean\_sum(df, features, m) Count data for data\_clean |


#

| |
| --- |
|
content\_recommender(productid, n\_of\_recomm)
 |
|
content\_recommender – When you search for a product, it recommends the top N products that are similar to it with Tfid vectorizer and cosine similarity algorithm.
 |
| Parameters:: |
| productid : String_, default = None_ID of the product to target
**n\_of\_recomm : Int_, default = None_** Number of similar products to be recommended ![](RackMultipart20221203-1-vhq3rt_html_8823e05746748c48.png)
 |
| **Returns::** |
| **data.loc[sim\_scores.index][['ProductId','Text']] : DataFrame**Index, id, text of TOP N similar products |


|
 |
| --- |
|
svdrec(table, factors)
 |
|
svdrec – When you search for a user, it recommends the top N products that are similar to it with svd algorithm.
 |
| Parameters:: |
|
**table : Array_, default = table_** An array form of a matrix for items recommended by the user in the past. **factors : int_, default = table_** An integer factor value required for SVD algorithm. ![](RackMultipart20221203-1-vhq3rt_html_337745938fba90ae.png)
 |
| Returns:: |
| **pred\_mat : Array** Using the SVD algorithm, the empty place of the existing matrix is filled and predicted matrix. |
| **Methods::** |
| Calculate\_mse(x) Calculate mse and print train, test errordawcm(y\_dred, y\_test=test, title='') plot the confusion matrixRec(result, uid, n, rawId=False) Recommend product ID with userID |







|
MF1(data, factors, maxIter, LRate, GD\_end, plot)
 |
| --- |
|
 |
|
MF1 – When you search for a user, it recommends the top N products that are similar to it with matrix factorization algorithm.
 |
| Parameters:: |
| **data : Array_, default = z_** An array form of a matrix for items recommended by the user in the past. **factors : Int_, default = 30_** An integer factor value required for matrix factorization algorithm. **maxIter : Int_, default = 100_** Maximum number of trainings to apply to gradient descent. **LRate : Float_, default = 0.02_** learning rate of trainings to apply to gradient descent. **GD\_end : Float_, default = 1e-3_** The threshold at which gradient descent will stop. **plot : Boolean_, default = False_** Whether or not to plot the results. ![](RackMultipart20221203-1-vhq3rt_html_186d848740a29718.png) |
| Returns:: |
| **P.dot(Q.T) : Array**Using the matrix factorization algorithm, the empty place of the existing matrix is filled and predicted matrix. |
| **Methods::** |
| Calculate\_mse(x) Calculate mse and print train, test errordawcm(y\_dred, y\_test=test, title='') plot the confusion matrixRec(result, uid, n, rawId=False) Recommend product ID with userID |





| |
| --- |
|

# **Analysis Results**


#### **Recommender with Cosine similarity**
 ![](RackMultipart20221203-1-vhq3rt_html_a76e368b3f92ab80.png)
This is the result of running the recommendation system with the product ID and N related to dog food as 20. TOP1 is dog food, and TOP2 is a good recommendation for similar products for dog snacks.









#### **SVD**
![](RackMultipart20221203-1-vhq3rt_html_c9a52ae395ab2164.png)In our recommendation system, we have such a matrix which has many scores from the users to the items. We hope to predict the targeted users' score to other unevaluated items and then recommend the items with the highest five scores. The advantage of SVD is that: users' score matrix is a sparse matrix, so we can map the original data into a Low-dimensional space and then calculate the similarity of different items. This can help us reduce calculation complexity.So, the results are neither good nor bad.


#### **Matrix Factorization**
 ![](RackMultipart20221203-1-vhq3rt_html_d32bc90bc26362ef.png)Latent factor models are an alternative approach that tries to explain the ratings by characterizing both items and users on, say, 20 to 100 factors inferred from the ratings patterns. For products, the discovered factors might measure obvious dimensions such as candy vs drinks, or adult food vs children's; For users, each factor measures how much the user likes the product that score high on the corresponding movie factor. Using latent factor model, we transform the way to calculate the similarity of users and products. The features become more stable and condense.

The MF gives a very good prediction: the train set MSE is 0.03542 and the test set MSE is 0.03385. While both MSEs are equally small, thus no overfitting problem occurs. In addition, as image shows that the number of latent factors significantly affect.
![](RackMultipart20221203-1-vhq3rt_html_7d076ef594028c2f.png)As the number of latent factors increase, the MSE decreases. And MSE converges around n=20. |
