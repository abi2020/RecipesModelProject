By Abishek Siva
## Framing the Problem

**Prediction Problem**: I will try to predict the `rating` for a certain recipe - this will be a regression problem.

**Response Variable**: `rating`

**Features**: `minutes`, `n_steps`, and `n_ingredients`

**Reason**: I chose this response variable since it combines various factors like steps, ingredients, and time to understand what influences ratings. Regression analysis on the rating can help identify the relative importance of each of these factors in determining overall recipe satisfaction. This form of analysis is particularly helpful for chefs, bloggers, and companies to create recipes that not only taste good but also match the preferences of their audience. Understanding what influences a recipe's rating allows for targeted improvements and recommendations that cater to the preferences of the target audience.

**Metric**: Since this is not a classification problem, we can not use accuracy of F-1 score to evaluate the model. Instead, Root Mean Square Error (RMSE) and the R^2 score seem like ideal choices. RMSE shows how well the model's predictions align with the true values, with lower values indicating better performance. Also, RMSE is in the same units as the response variable, which makes it better than Mean Squared Error. Additionally, R^2 score for the model will tell us how much of the variance in the response variable is explained by our model.

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
