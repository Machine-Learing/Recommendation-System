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

|	|
| :- |
|<p></p><p>**Data(dataset)**</p><p></p>|
|Data – It preprocesses the input data set and returns the values of z, total\_u, total\_p, pid2PID, train, test, table, raw\_data.|
|**Parameters::**|
|<p>**dataset : String*, default = None***</p><p>The path to the data file the user wants to use. Features that are not needed do not need to be deleted separately.![](Aspose.Words.ec69fc15-75be-4c9e-82fc-52419fed1ab1.013.png)</p>|
|**Methods::**|
|<p>data\_clean(df, features, m)                Select data</p><p>data\_clean\_sum(df, features, m)           Count data for data\_clean</p>|

|<p></p><p><h1></h1></p>|
| :- |

|	|
| :- |
|<p></p><p>**content\_recommender(productid, n\_of\_recomm)**</p><p></p>|
|<p></p><p>content\_recommender – When you search for a product, it recommends the top N products that are similar to it with Tfid vectorizer and cosine similarity algorithm.</p><p></p>|
|**Parameters::**|
|<p>**productid : String*, default = None***</p><p>ID of the product to target </p><p></p><p>**n\_of\_recomm : Int*, default = None***</p><p>Number of similar products to be recommended </p><p>![](Aspose.Words.ec69fc15-75be-4c9e-82fc-52419fed1ab1.014.png)</p><p></p>|
|**Returns::**|
|<p>**data.loc[sim\_scores.index][['ProductId','Text']] : DataFrame**</p><p>Index, id, text of TOP N similar products</p>|

||
| :- |
|<p></p><p>
 **svdrec(table, factors)**</p><p></p>|
|<p></p><p>svdrec – When you search for a user, it recommends the top N products that are similar to it with svd algorithm.</p><p></p>|
|**Parameters::**|
|<p></p><p>**table : Array*, default = table***</p><p>An array form of a matrix for items recommended by the user in the past.</p><p>**factors : int*, default = table***</p><p>An integer factor value required for SVD algorithm.</p><p>![](Aspose.Words.ec69fc15-75be-4c9e-82fc-52419fed1ab1.015.png)</p><p></p>|
|**Returns::**|
|<p>**pred\_mat : Array**</p><p>Using the SVD algorithm, the empty place of the existing matrix is filled and predicted matrix.</p>|
|**Methods::**|
|<p>Calculate\_mse(x)                  Calculate mse and print train, test error</p><p>dawcm(y\_dred, y\_test=test, title=’‘)  plot the confusion matrix</p><p>Rec(result, uid, n, rawId=False)      Recommend product ID with userID</p>|

 **MF1(data, factors, maxIter, LRate, GD\_end, plot)**</p><p></p>|
| :- |
||
|<p></p><p>MF1 – When you search for a user, it recommends the top N products that are similar to it with matrix factorization algorithm.</p><p></p>|
|**Parameters::**|
|<p>**data : Array*, default = z***</p><p>An array form of a matrix for items recommended by the user in the past.</p><p>**factors : Int*, default = 30***</p><p>An integer factor value required for matrix factorization algorithm.</p><p>**maxIter : Int*, default = 100***</p><p>Maximum number of trainings to apply to gradient descent.</p><p>**LRate : Float*, default = 0.02***</p><p>learning rate of trainings to apply to gradient descent.</p><p>**GD\_end : Float*, default = 1e-3***</p><p>The threshold at which gradient descent will stop.</p><p>**plot : Boolean*, default = False***</p><p>Whether or not to plot the results.</p><p>![](Aspose.Words.ec69fc15-75be-4c9e-82fc-52419fed1ab1.016.png)</p>|
|**Returns::**|
|<p>**P.dot(Q.T) : Array**</p><p>Using the matrix factorization algorithm, the empty place of the existing matrix is filled and predicted matrix.</p>|
|**Methods::**|
|<p>Calculate\_mse(x)                  Calculate mse and print train, test error</p><p>dawcm(y\_dred, y\_test=test, title=’‘)  plot the confusion matrix</p><p>Rec(result, uid, n, rawId=False)      Recommend product ID with userID</p>|

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
