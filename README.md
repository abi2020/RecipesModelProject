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
|----------:|----------:|----------------:|---------:|
|        40 |        10 |               9 |        4 |
|        45 |        12 |              11 |        5 |
|        40 |         6 |               9 |        5 |
|        40 |         6 |               9 |        5 |
|        40 |         6 |               9 |        5 |

|   minutes |   n_steps |   n_ingredients |   rating |
|-----------|-----------|-----------------|----------|
|        40 |        10 |               9 |        4 |
|        45 |        12 |              11 |        5 |
|        40 |         6 |               9 |        5 |
|        40 |         6 |               9 |        5 |
|        40 |         6 |               9 |        5 |

## Baseline Model

Classification Report for Train Data:
              precision    recall  f1-score   support

         1.0       0.70      0.07      0.13      2322
         2.0       0.71      0.08      0.14      1906
         3.0       0.74      0.07      0.13      5696
         4.0       0.71      0.11      0.19     29969
         5.0       0.79      0.99      0.88    135619

    accuracy                           0.79    175512
   macro avg       0.73      0.26      0.29    175512
weighted avg       0.77      0.79      0.72    175512

Classification Report for Test Data:
              precision    recall  f1-score   support

         1.0       0.08      0.01      0.02       548
         2.0       0.02      0.00      0.00       462
         3.0       0.09      0.01      0.02      1476
         4.0       0.25      0.04      0.07      7338
         5.0       0.78      0.97      0.87     34054

    accuracy                           0.76     43878
   macro avg       0.24      0.21      0.19     43878
weighted avg       0.65      0.76      0.68     43878