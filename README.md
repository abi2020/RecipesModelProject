By Abishek Siva
## Framing the Problem

**Prediction Problem**: I will try to predict the `rating` for a certain recipe - this will be a multi-class classification problem.

**Response Variable**: `rating`

**Features**: `minutes`, `n_steps`, and `n_ingredients`

**Reason**: I chose this response variable since it combines various factors like steps, ingredients, and time to understand what influences ratings. Regression analysis on the rating can help identify the relative importance of each of these factors in determining overall recipe satisfaction. This form of analysis is particularly helpful for chefs, bloggers, and companies to create recipes that not only taste good but also match the preferences of their audience. Understanding what influences a recipe's rating allows for targeted improvements and recommendations that cater to the preferences of the target audience.

**Metric**: Since this is a classification problem we will choose precision and F-1 score. Precision allows us to determine how well our model fits the dataset while ensuring that we don't miss recommending a good recipe (reduce false negatives). F-1 score will also incorporate recall, and allow us to get a more holistic view of the model. Additionally, since there is an overwhelming amount of 4 and 5 star reviews, accuracy will not be a helpful metric.

**Data Known at Time of Prediction**: A person who is about to review a recipe will have access to the `minutes`, `n_steps`, and `n_ingredients` for the said recipe. However, they will not have access to their `review`, which is a written response of how they feel about the recipe. Thus, all the features in this model will will be available at the time of prediction.

**Data Cleaning**: I started off with two datasets: one for `recipes` and one for `interactions`. I then merged the two dataframes using the `id` feature. I then replaced all missing values with `0`. I also set the index of the dataframe to be the recipe `id`. Finally, I only selected the columns that I will be using in the analysis, which is `minutes`, `n_steps`, `n_ingredients`, and `rating`. I also dropped any rows that were missing the `rating` feature to simplify the analysis.

**Head of Cleaned Data Frame**:

|   minutes |   n_steps |   n_ingredients |   rating |
|:----------|:----------|:----------------|:---------|
|        40 |        10 |               9 |        4 |
|        45 |        12 |              11 |        5 |
|        40 |         6 |               9 |        5 |
|        40 |         6 |               9 |        5 |
|        40 |         6 |               9 |        5 |

## Baseline Model

**Model Description**: This model is a Decision Tree Classifier that has three features: `minutes`, `n_steps`, and `n_ingredients`. All three features are quantitative values, so I did not one-hot encode any of them. I did not do any transformations to the features for the baseline model.

**Performance** <br>
Classification Report for Train Data:

| index        |   precision |   recall |   f1-score |       support |
|:-------------|------------:|---------:|-----------:|--------------:|
| 1.0          |    0.545455 | 0.118681 |   0.194946 |   2275        |
| 2.0          |    0.56068  | 0.120627 |   0.198539 |   1915        |
| 3.0          |    0.597938 | 0.111617 |   0.188117 |   5716        |
| 4.0          |    0.655546 | 0.133639 |   0.222018 |  29849        |
| 5.0          |    0.796582 | 0.982564 |   0.879852 | 135757        |
| accuracy     |    0.789222 | 0.789222 |   0.789222 |      0.789222 |
| macro avg    |    0.63124  | 0.293426 |   0.336694 | 175512        |
| weighted avg |    0.760298 | 0.789222 |   0.729136 | 175512        |

Classification Report for Test Data:

| index        |   precision |     recall |   f1-score |      support |
|:-------------|------------:|-----------:|-----------:|-------------:|
| 1.0          |   0.109375  | 0.0123023  | 0.0221169  |   569        |
| 2.0          |   0.047619  | 0.00437637 | 0.00801603 |   457        |
| 3.0          |   0.0748299 | 0.00748299 | 0.0136054  |  1470        |
| 4.0          |   0.275122  | 0.0378067  | 0.0664781  |  7459        |
| 5.0          |   0.777347  | 0.976181   | 0.865491   | 33923        |
| accuracy     |   0.761589  | 0.761589   | 0.761589   |     0.761589 |
| macro avg    |   0.256859  | 0.20763    | 0.195142   | 43878        |
| weighted avg |   0.652174  | 0.761589   | 0.681257   | 43878        |


**Analysis of Performance**: We can see that our model perfoms better on the training data versus the test data. We can also see that in the test data, the precision is much lower for star ratings of 1-4. This means that our model is predicting the most common rating of 5 too often. This is why the accuracy scores for both models are somewhat similar. Thus, there is definitely room for improvement in this model.

## Final Model

**Added Features**: One of the features I added was a Quantile Transformation on the `minutes` feature. This is because there tended to be some very obvious outliers (values longer than an entire day) which were skewing the data. A quantile transformation is ideal for reducing the impact of marginal outliers. Additionally, I applied a standard scaler on the `n_steps` and `n_ingredients`features. This would ensure that both features will have a mean of 0 and a standard deviation of 1. Scaling ensures that all features contribute equally to the model fitting process. Without scaling, features with larger magnitudes might dominate the learning process. 

**Description of Modeling Algorithm**: I decided to change to a Random Forest Classifier for the final model since that would involve several different Decision Trees. By doing so, a RFC is able to capture complex relationships in the data by combining the strengths of mutiple trees. A RFC are less sensitive to changes in the training data, and thus are less likely to result in significant changes in the ensemble's predictions. 

**Hyperparameter Tuning**: I did a grid search to determine the ideal `max_depth` for the Random Forest (7 levels). 

**Performance** <br>
Classification Report for Train Data:

| index        |   precision |    recall |   f1-score |       support |
|:-------------|------------:|----------:|-----------:|--------------:|
| 1.0          |    0.643636 | 0.0773263 |   0.138066 |   2289        |
| 2.0          |    0.772152 | 0.0657682 |   0.121212 |   1855        |
| 3.0          |    0.714556 | 0.0664323 |   0.121563 |   5690        |
| 4.0          |    0.712579 | 0.109809  |   0.190294 |  29870        |
| 5.0          |    0.792159 | 0.991289  |   0.880607 | 135808        |
| accuracy     |    0.789587 | 0.789587  |   0.789587 |      0.789587 |
| macro avg    |    0.727016 | 0.262125  |   0.290348 | 175512        |
| weighted avg |    0.773951 | 0.789587  |   0.720806 | 175512        |

Classification Report for Test Data:

| index        |   precision |     recall |   f1-score |      support |
|:-------------|------------:|-----------:|-----------:|-------------:|
| 1.0          |   0.0441176 | 0.00516351 | 0.00924499 |   581        |
| 2.0          |   0.1       | 0.00779727 | 0.0144665  |   513        |
| 3.0          |   0.101695  | 0.00809717 | 0.015      |  1482        |
| 4.0          |   0.258702  | 0.0369773  | 0.0647059  |  7437        |
| 5.0          |   0.775858  | 0.975727   | 0.864389   | 33865        |
| accuracy     |   0.759766  | 0.759766   | 0.759766   |     0.759766 |
| macro avg    |   0.256074  | 0.206752   | 0.193561   | 43878        |
| weighted avg |   0.647842  | 0.759766   | 0.6789     | 43878        |


**Analysis of Performance**: We can see that our final model is more precise at individual ratings compared to the baseline model. This is important since our baseline model was initially highly influenced by the unbalanced nature of the training data (there were way more 4 and 5 star ratings). Additionally, we can see that the overall F-1 score has gone up for most of the categories, which again shows that the model is doing a better job of predicting the right rating. However, we still see that the model performs much better on the training data than it does on the test data. The best way to fix this issue would be to train the model on an alternate data set where the ratios of every rating were more similar.

## Fairness Analysis

**Group X**: 5 star ratings

**Group Y**: 1 star ratings

**Evaluation Metric**: Precision

**Null Hypothesis**: The model has the same precision for 5-star rated recipes and 1 star rated recipes. Any difference in precision is due to chance.

**Alternate Hypothesis**: The model's precision for 5-star rated recipes and 1 star rated recipes is different.

**Test Statistic**: Absolute difference in the precisions

<iframe src="assets/proj5.html" width=800 height=600 frameBorder=0></iframe>
