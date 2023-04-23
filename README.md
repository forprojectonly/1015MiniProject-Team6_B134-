# 1015MiniProject-Team6_B134

Welcome to Team 6's repository! 

**About:**

This mini project for SC1015(Introduction to Data Science and Artificial Intelligence) aims to analyse the relationship between audio features and popularity of tracks on youtube and spotify.

For a more detailed walkthrough, please view the source code in order from:

1.Data Extraction

2.Data Cleaning

3.Data Visualization

4.Linear Regression 

5.Decision Tree

6.Random Forest

7.Neural Network Regression


**Contributors**

Ooi Zi Xin, Chad Tan, Zhang Xinyang

**Problem Definition**

To Identify the relationship between a piece of music's audio features and its popularity on Spotify and Youtube.

**Variables Used**

Independent Variables: Spotify audio features including Danceability, Instrumentalness, Energy etc.

Dependent Variables: Mainly Stream (Spotify) and Views (Youtube), with Comments and Likes (Youtube) being considered as well

**Data Cleaning**

There were 3 main steps when cleaning the data.
1. Eliminate null values

Some rows lacked entries for metrics on both Spotify and Youtube. A handful of rows were missing audio features. These rows were systematically removed and dropped  from the dataset.

2. Eliminate non-music tracks

The dataset generated included non-musical tracks such as audiobooks and asmr tracks. These tracks were not relevant to our problem as we wanted to focus on musical tracks. As such, we briefly scanned through the dataset for keywords that indicated the presence of non-musical tracks. For instance, the word "Folge", German for Chapter, was a clear indicator that the associated row was for a German audiobook. These keywords helped us identify and remove these undesirable tracks. However, this method is highly qualitative and may not be comprehensive.

To account for rows that may have passed the qualitative filter, we also included a quantitative filter to sort out tracks that are unlikely to be musical tracks. Tracks that were longer than 10 minutes were removed, therefore increasing the likelihood that audiobooks and asmr tracks were removed. A downside to this additional approach was the removal of music compilations. However, considering that our problem statement required us to focus on individual works, the elimination of compilations is acceptable as it is not a singular work, but rather, a collection of them.

3. Eliminate outliers

Last but certainly not the least, the removal of outliers is an essential step when cleaning data. We employed Tukey's method of using the IQR to determine the range of acceptable values, and removed all outliers that lay outside this range. This step helped reduce the severe skewness in some of our columns.


**Data Exploration**

Basic data exploration was performed on the dataset. Some of the interesting results include:
- Correlations between Loudness and energy. However this correlation serves a limited purpose as it is between independent variables.
- Correlations between Likes, comments and Views. Similarly, this correlation serves limited purpose as it demonstrates that comments and likes are linked to the main dependent variable of views. As such, likes and comments could and were also use as dependent variables in our models.

Despite the identification of these relationships, our columns overall demonstrated poor linear correlation, with correlation coefficients close to 0. Although a logistic transformation of the Views and Streams columns improved the correlation, it was marginal as the coefficient only reached a value of 0.15 in relation to selected columns. Eventually, it was decided not to implement this transformation into the models.


Models Used
1. Linear Regression

Despite the poor linear correlation between our columns, we decided to give linear regression a try. As expected, the model performed poorly with R^2 values of close to 0. Attempts at transforming the columns using roots, logs and exponentials generally yielded worse results, with R^2 values dipping below 0. This meant the model was outperformed by a simple horizontal average line.

The poor performance of the model was expected, as our EDA has demonstrated that the columns were not linearly related.

2. Decision Tree

The poor performance of our linear model led us to consider non-linear models. The first model we tried was the Decision Tree. The decision tree model is a non-linear model that can handle complex relationships between features and target variables. The model works by recursively splitting the data based on the most significant feature until the target variable is predicted accurately.

When we applied the decision tree model to our dataset, we found that at a depth of 3, the model gave the highest R^2 value of 0.015. This indicates that the model explained only a small proportion of the variance in the target variable. However, when we increased the depth of the tree to 4 and 5, the R^2 values became negative, which means that the model performed worse than the mean of the target values. This indicates that the model is overfitting the data and cannot generalize to new data.

Overall, the results of the decision tree model were not satisfactory as it could not capture the complex relationships between the features and target variables in our dataset.


3. Random Forest

Since the decision tree model did not perform well, we tried the random forest model, which is an ensemble learning method that combines multiple decision trees to improve the predictive power.

When we applied the random forest model to our dataset, we obtained the following evaluation metrics:

Mean squared error: 197732548760391360.00

Coefficient of determination (R^2): 0.18

Explained variance score: 0.18

Maximum residual error: 9130671677.54

Median absolute error: 159719667.75

The R^2 value of 0.18 indicates that the random forest model can explain 18% of the variance in the target variable, which is a slight improvement over the decision tree model. However, the mean squared error is extremely high, indicating that the model has high prediction errors.

The maximum residual error and median absolute error are also quite high, which means that the model has difficulty accurately predicting extreme values. However, the explained variance score of 0.18 suggests that the model can capture some of the variation in the target variable, which could be useful for some applications.

Overall, the random forest model is an improvement over the decision tree model, but it still has limitations in accurately predicting the popularity of music tracks based on their audio features.


4. Neural Network Regression

We also tried using neural network regression to predict the popularity of music tracks based on their audio features. The neural network model is a powerful machine learning technique that can capture complex non-linear relationships between features and target variables.

However, when we applied the neural network model to our dataset, we obtained the following evaluation metrics:

Test loss: 2.728456357937152e+16

Test mean squared error: 2.728456357937152e+16

Test mean absolute error: 44969376.0

Test explained variance: 0.007524372541681405

R-squared: -0.058256867244613986

Mean absolute percentage error: Views 1.626201e+05, Comments inf, Likes 3.418453e+04

Root mean squared error: 165180382.32395783

Explained variance score: 0.007524372541681405

The results show that the neural network model performed poorly in predicting the popularity of music tracks based on their audio features. The test loss and mean squared error are extremely high, indicating that the model has very high prediction errors.

The R-squared value is negative, which means that the model cannot explain the variance in the target variable. Additionally, the mean absolute percentage error is also high, suggesting that the model has difficulty accurately predicting the popularity of music tracks.

Overall, the results of the neural network model are unsatisfactory, indicating that the model cannot accurately predict the popularity of music tracks based on their audio features.


5. Brief Summary of Models

In summary, we tried four different models to predict the popularity of music tracks based on their audio features: linear regression, decision tree, random forest, and neural network regression.

The linear regression model performed poorly, with an R^2 value close to 0, indicating that the model could not explain the variance in the target variable.

The decision tree model performed slightly better than the linear regression model, with an R^2 value of 0.015, but the model had difficulty capturing the complex relationships between features and the target variable.

The random forest model was an improvement over the decision tree model, with an R^2 value of 0.18, but the model still had high prediction errors and difficulty accurately predicting extreme values.

The neural network regression model performed the worst among the four models, with a negative R-squared value and extremely high prediction errors.

Overall, none of the four models were able to accurately predict the popularity of music tracks based on their audio features. This suggests that there may be other factors beyond audio features that contribute to the popularity of music tracks on platforms like Spotify and YouTube.


**Insights**

In general, the poor performances of the models are likely not due to the appropriateness of the model, but rather the definition of our problem. We chose a narrow definition of our problem statement, restricting us to audio features of the music. Our results show that audio features are poorly correlated to a song's popularity.

Such a result, while disappointing, is understandable. 

One of the reasons for this could be that non-musical factors such as marketing, artist popularity, and platform algorithms play a significant role in determining the popularity of a song. These factors are not captured in our dataset, and hence our models were unable to fully account for their impact. For example, a song released by a popular artist is likely to gain more attention and promotion compared to a song released by a less well-known artist, regardless of the musical attributes of the song. Similarly, the platform algorithms used by streaming services may prioritize certain songs based on their popularity or user preferences, further impacting their success.

Another factor that could be considered was the different music genres of our music. Different music genres have different audio features that are more popular among their respective audiences. Therefore, it's possible that the audio features that were analyzed were not appropriate for certain genres or that other features, specific to those genres, are more important. Furthermore, even within these genres, there exists a distribution for the popularity of songs. These songs are likely to share similar audio features, and as such, the differences in their popularity is proof that audio features may not be paticularly useful in determining the number of views and streams that a song can achieve.

**Learning Points**

However, this project was still extremely enriching and we learnt a lot through this process. We studied additional models such as neural networks, logistic regressions and random forests, as well as learnt the appropriate implementation of these models. There were also more practical learning points such as the use of API, as well as the treatment of raw data to suit our needs.

But, most importantly, we as a group learnt the importance of proper problem definition. The poor performance of our models can be in part attributed to the lack of consideration regarding the links between various variables. For future projects, a more in-depth qualitative analysis of our context and problem can help us implement better models.

Our group also had to change datasets midway through our project. A key issue arose when the data collected was found to be missing certain variables, as well as being of unidentifiable types. The failure to perform thorough checks initial data collection meant that there was insufficient time to recollect data from the original source as we were rate-limited. The building an initial and primitive model is therefore an important step that should be performed before large-scale data collection. It is also a good habit to read the json file thoroughly and identify any possible pitfalls that may lead to errors in data collection.


References
- https://spotipy.readthedocs.io/en/2.22.1/
- https://www.kaggle.com/datasets/salvatorerastelli/spotify-and-youtube

