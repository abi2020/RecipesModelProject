By Abishek Siva
## Framing the Problem

**Prediction Problem**: I will try to predict the `rating` for a certain recipe - this will be a multi-class classification problem.

**Response Variable**: `rating`

**Features**: `minutes`, `n_steps`, and `n_ingredients`

**Reason**: I chose this response variable since it combines various factors like steps, ingredients, and time to understand what influences ratings. Regression analysis on the rating can help identify the relative importance of each of these factors in determining overall recipe satisfaction. This form of analysis is particularly helpful for chefs, bloggers, and companies to create recipes that not only taste good but also match the preferences of their audience. Understanding what influences a recipe's rating allows for targeted improvements and recommendations that cater to the preferences of the target audience.

**Metric**: Since this is a classification problem we will choose precision and F-1 score. Precision allows us to determine how well our model fits the dataset while ensuring that we don't miss recommending a good recipe. F-1 score will also incorporate recall, and allow us to get a more holistice view of the model. Additionally, since there is an overwhelming amount of 4 and 5 star reviews, accuracy will not be a helpful metric.

**Data Cleaning**
I started off with two datasets: one for `recipes` and one for `interactions`. I then merged the two dataframes using the `id` feature. I then replaced all missing values with `0`. I also set the index of the dataframe to be the recipe `id`. Finally, I only selected the columns that I will be using in the analysis, which is `minutes`, `n_steps`, `n_ingredients`, and `rating`.

Head of Cleaned Data Frame:

|   minutes |   n_steps |   n_ingredients |   rating |
|:----------|:----------|:----------------|:---------|
|        40 |        10 |               9 |        4 |
|        45 |        12 |              11 |        5 |
|        40 |         6 |               9 |        5 |
|        40 |         6 |               9 |        5 |
|        40 |         6 |               9 |        5 |

## Baseline Model

Classification Report for Train Data:

|   precision |    recall |   f1-score |   support |
|------------:|----------:|-----------:|----------:|
|    0.703252 | 0.0745047 |   0.134735 |      2322 |
|    0.710145 | 0.0771249 |   0.139139 |      1906 |
|    0.735294 | 0.0702247 |   0.128205 |      5696 |
|    0.709706 | 0.107845  |   0.187237 |     29969 |
|    0.791182 | 0.991528  |   0.880097 |    135619 |

Classification Report for Test Data:

|   precision |     recall |   f1-score |   support |
|------------:|-----------:|-----------:|----------:|
|   0.0793651 | 0.00912409 | 0.0163666  |       548 |
|   0.0204082 | 0.0021645  | 0.00391389 |       462 |
|   0.0909091 | 0.00880759 | 0.0160593  |      1476 |
|   0.248881  | 0.037885   | 0.0657599  |      7338 |
|   0.779749  | 0.973278   | 0.865831   |     34054 |