
# COOKIN CALORIES

by Jasmine & Shekar 

---

## Introduction

Our analysis explores which types of recipes are more likely to be high in calories and to predict recipe ratings. This information is valuable for individuals seeking tasty recipes that align with their dietary goals. By identifying these trends, we provide a useful tool for those looking for flavorful recipes that are also within their calorie limits. Calories are essential units of energy required for bodily functions.Our analysis helps people find diet-friendly and tasty recipes."

The two csv datasets we are working with are Raw Recipes and Raw Interactions. Raw_Recipes contains recipes and Raw_interactions contains the reviews and ratings submitted for the recipes in RAW_recipes. Both of the recipes are from Food.com.Food.com is a digital brand and media platform that features a large collection of recipes that are submitted, rated, and reviewed by foodies including home cooks, celebrity chefs, and shows. These data sets only contain data posted since 2008 



---

## Cleaning and EDA

There are 82782 rows and 12 columns in the Recipe dataset. Each row is a unique recipe.
**Recipes Dataset**

<p>'name' : Recipe Name <br>
'id' : Recipe ID <br>
'minutes' : minutes to prepare recipe <br>
'contributor_id' : user id who submitted recipe <br>
'submitted' : date recipe was submitted <br>
'tabs' - related tags for the recipe, generated by Food.com <br>
'nutrition' - Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value” <br>
'n_steps' - # of steps in recipe <br>
'steps' - text for recipe steps, in order <br>
'description' - user provided description <br>


</p>

There are  731927 rows and 5 columns in raw interactions. Each row is a review left by a user.
**Raw Interactions Dataset** 

'user_id' : User ID 

'recipe_id':Recipe ID 

'date' : Date of interaction 

'rating' : Rating given 

'review' : Review text 

**Average Rating**
We created an extra column with the average rating of recipes. This is useful in order to build our model and predict the ratings of foods. 

**Merged Datframe**
Both of the dataframes have common columns id and recipe id. In order to keep all the recipes, we merged left the two dateferames to show the corresponding rating and review for each unique recipe. 


**Duplicate columns**

Since the id and recipe id match up, we dropped the recipe column beccause it is uneccesssary to have duplicate values


**Extracting Nutrition Column** 
We discovered that the values in the list are actually strings. 
As a result, we converted the values into a list of floats and created individual columns for each value in the list. The added columns are 
calories, total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV) with float data type<br>



The columns relevant to our question are ['minutes','n_steps','n_ingredients','calories', 'sugar', 'protein',
       'total_fat', 'carbohydrates','rating','review','average_rating','ingredients'] 


**Cleaned DataFrame and Data Type With Relevant Columns**


|   minutes |   n_steps |   n_ingredients |   calories |   sugar |   protein |   total_fat |   carbohydrates |   rating | review                                                                                                                                                                                                                                                                                                                                           |   average_rating | ingredients                                                                                                                                                                    |
|----------:|----------:|----------------:|-----------:|--------:|----------:|------------:|----------------:|---------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        40 |        10 |               9 |      138.4 |      50 |         3 |          10 |               6 |        4 | These were pretty good, but took forever to bake.  I would send it ended up being almost an hour!  Even then, the brownies stuck to the foil, and were on the overly moist side and not easy to cut.  They did taste quite rich, though!  Made for My 3 Chefs.                                                                                   |                4 | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour'] |
|        45 |        12 |              11 |      595.1 |     211 |        13 |          46 |              26 |        5 | Originally I was gonna cut the recipe in half (just the 2 of us here), but then we had a park-wide yard sale, & I made the whole batch & used them as enticements for potential buyers ~ what the hey, a free cookie as delicious as these are, definitely works its magic! Will be making these again, for sure! Thanks for posting the recipe! |                5 | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                    |
|        40 |         6 |               9 |      194.8 |       6 |        22 |          20 |               3 |        5 | This was one of the best broccoli casseroles that I have ever made.  I made my own chicken soup for this recipe. I was a bit worried about the tsp of soy sauce but it gave the casserole the best flavor. YUM!                                                                                                                                  |                5 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |
|           |           |                 |            |         |           |             |                 |          | The photos you took (shapeweaver) inspired me to make this recipe and it actually does look just like them when it comes out of the oven.                                                                                                                                                                                                        |                  |                                                                                                                                                                                |
|           |           |                 |            |         |           |             |                 |          | Thanks so much for sharing your recipe shapeweaver. It was wonderful!  Going into my family's favorite Zaar cookbook :)                                                                                                                                                                                                                          |                  |                                                                                                                                                                                |
|        40 |         6 |               9 |      194.8 |       6 |        22 |          20 |               3 |        5 | I made this for my son's first birthday party this weekend. Our guests INHALED it! Everyone kept saying how delicious it was. I was I could have gotten to try it.                                                                                                                                                                               |                5 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |
|        40 |         6 |               9 |      194.8 |       6 |        22 |          20 |               3 |        5 | Loved this.  Be sure to completely thaw the broccoli.  I didn&#039;t and it didn&#039;t get done in time specified.  Just cooked it a little longer though and it was perfect.  Thanks Chef.                                                                                                                                                     |                5 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |
                                                                       

**Relevant Columns Data Type**

| Column Name    | Data Type   |
|:---------------|:------------|
| minutes        | int64       |
| n_steps        | int64       |
| n_ingredients  | int64       |
| calories       | float64     |
| sugar          | float64     |
| protein        | float64     |
| total_fat      | float64     |
| carbohydrates  | float64     |
| rating         | float64     |
| review         | object      |
| average_rating | float64     |
| ingredients    | object      |






**The whole Dataframe data type**

| Column Name    | Data Type   |
|:---------------|:------------|
| name           | object      |
| id             | int64       |
| minutes        | int64       |
| contributor_id | int64       |
| submitted      | object      |
| tags           | object      |
| nutrition      | object      |
| n_steps        | int64       |
| steps          | object      |
| description    | object      |
| ingredients    | object      |
| n_ingredients  | int64       |
| user_id        | Int64       |
| date           | object      |
| rating         | float64     |
| review         | object      |
| average_rating | float64     |
| calories       | float64     |
| total_fat      | float64     |
| sugar          | float64     |
| sodium         | float64     |
| protein        | float64     |
| saturated fat  | float64     |
| carbohydrates  | float64     |






**Univariate Analysis**
We looked at the distribution of number of steps('n_steps') and 
the distribution of number of ingredients('n_ingredients') 

This is a distribution of the number of steps in recipes.The distributionn has a bell shaped curved and is skewed right  with the max count of n_steps being 7. This means that most recipes have 
7 steps .

<br>

<iframe
  src="assets/update.html"
  width="600"
  height="400"
  frameborder="0"
></iframe>

This is a count of n_ingredients
<iframe
  src="assets/un2_analysis.html"
  width="600"
  height="400"
  frameborder="0"
></iframe>
<br>
The distribution has a bell shaped curve and is is skewed right. The max count is at 8. This means that most recipes has 8 steps. 


**Bivariate Analysis**
We looked at the relationship between number of steps
and the amount of protein and the number of ingredients and the the number
of steps and the number of ingredients <br>

For the  number of steps and the amount of protein there seems no be no correlation and a weak relationship. There is an apparent outlier of 4356  of protein and 4 steps. The points are mainly clustered below 1000 for protein. 

<iframe
  src="assets/un3_analysis.html"
  width="600"
  height="400"
  frameborder="0"
></iframe>


This is the box plot of n_steps and n_ingredients
<iframe
  src="assets/box.html"
  width="600"
  height="400"
  frameborder="0"
></iframe>

There are many apparent outliers. A general pattern is that as n_ingredients increases, the range of steps increases. The boxplot with the greatest range
is at 30 ingredients. 


**interesting aggregate**<br>
The average,min, and max sugar content of a recipe based on the amount of steps in the recipe.<br>


|   n_steps |   ('mean', 'sugar') |   ('max', 'sugar') |   ('min', 'sugar') |
  |----------:|--------------------:|-------------------:|-------------------:|
|         1 |             64.0372 |               2360 |                  0 |
|         2 |             67.5614 |               4005 |                  0 |
|         3 |             60.2696 |               3537 |                  0 |
|         4 |             60.8759 |              16901 |                  0 |
|         5 |             54.3202 |              14495 |                  0 |



---

## Assessment of Missingness

**Missingness of 'Description'** <br>
The column 'description' is NMAR because the user might have submitted
the recipe on a mobile device like an Iphone. Since it's a smaller screen, it's harder to write out a description. As a result, it takes more time to
write one. Therefore, the individual may choose not to include a description<br>

'Description' can become a MAR missingness if we add a new column with boolean statements of whether or not they are on a mobile device. There may be no description if the value is true. <br>

There is more than one column that has nan values. However, columns with 
only one row of nan values don't have a significant impact on our 
analysis. We assume that ratings of 0 are replaced with nan because it 
may impact the average rating. Nan is not included when calculating mean.This
is more appropriate in cases where the values are not known or the true rating is not actually bad<br>

**'Rating' Missingness** <br>
**Missingness of rating based on the number of steps** <br>

*Null Hypothesis* : The distribution of 'n_steps' when 'rating' is missing is the same as the distribution of 'n_steps' when 'rating' is not missing.
 <br>
*Alternative Hypothesis* - The distribution of 'n_steps' is different when 'rating' is missing compared to when 'rating' is not missing. <br>
*observed statistic* - absolute difference between the average 'n_steps' when 'rating' is missing and the average 'n_steps' when 'rating' is not missing. <br>

<iframe
  src="assets/missingness4.html"
  width="600"
  height="400"
  frameborder="0"
></iframe>

The mean is about the same because they are both cerntered around the same place but have different shape. 

<iframe
  src="assets/missingness3.html"
  width="600"
  height="400"
  frameborder="0"
></iframe>


After conducting a permutation test to shuffle the missingness of rating 1000 times and geting 1000 simulating results about the absolute difference, we got a p-value of
0.0. Our significance level is 0.05. Because 0.0 < 0.05, we reject the null hypothesis that the distribution of  n_steps when rating is missing is the same as the distribution of the minutes when rating is not missing. Based on our p-value and results, rating is MAR because it's missingness is dependent on the number of steps it takes to prepare the food.


**Missingness of Rating Based on Minutes** <br>
*null hypothesis*: the distribution of the minutes when rating is missing is the same as the distribution of the minutes when rating is not missing 

*alternative hypothesis*: the distribution of the minutes when rating is missing is different from the distribution of the minutes when rating is not missing <br>
*observed statistic*: the absolute difference between minutes mean of these two distributions. <br>

<iframe
  src="assets/missingness2.html"
  width="600"
  height="400"
  frameborder="0"
></iframe>

The observed absolute difference is 51.45. Most of the points are to the left of the observed absolute difference point,

<iframe
  src="assets/missingness1.html"
  width="600"
  height="400"
  frameborder="0"
></iframe>

<p> After conducting a permutation test to shuffle the missingness of rating 1000 times and 1000 simulating results about the absolute difference, we got a p-value of
0.117. Our significance level is 0.05. Because 0.117> 0.05, we fail to reject the null hypothesis that the distribution of the minutes when rating is missing is the same as the distribution of the minutes when rating is not missing. Based on our p-value and results, rating is MCAR because it's missingness is not dependent on the amount of minutes it takes to prepare the food. <br> 




---
## Hypothesis Testing <br>


**Question: Do fancier recipes have a greater average amount of calories?** <br>

fancy:
  more than 15 ingredients<br>
regular: 
  less than or equal to 15 ingredients<br>

*null hypothesis*: There is no difference in the number of calories between fancy recipes  and regular recipes <br>

*alternative hypothesis* : Fancier recipes have a greater average of calories
than regular recipes <br>

Since we are dealing with numerical values: 
*observed test statistic* : The observed difference between the average number of calors of fancier and regular recipes. <br>

<p>We decided to create a new column called 'ingred_gt_10' that includes
boolean statements of whether the recipe needs more than in 10 ingredients.
We also included another column called 'shuffled_ingred_gt_10' to shuffle 
our values and conduct a permutation test. <br>



We conducted a permutation test 10000 times and found that the p_value to be 0.178 with a significance level of  0.05 <br>


<iframe
  src="assets/hypthesis.html"
  width="600"
  height="400"
  frameborder="0"
></iframe>

<br>

**conclusion** <br>
<pr>Because 0.178> 0.05, we fail to reject the hypothesis that there is a difference between the number of calories in fancy and regular recipes. This means that there is no significant difference in the average number of calories between fancier and regular recipes. There are many factors that can contribute to calories of a recipe. This may include the preparation process
of the recipe and the type of ingredients it is made of. This can effect the amount of calories in a recipe. <br>






---
## Framing a Prediction Problem <br>


**Question: Can we Predict the Rating of a Recipe?** <br>
<pr>
What we wanted to do was create a machine learning model that would use other variables available to us in the data to estimate how good a meal was. Since food is very subjective and varies from person to person, we figured that there must be other ways besides a rating to tell if a recipe is going to turn out well. A rating is the best way to guess this, but other factors must contribute a role to how good the food is. We wanted to engineer an algorithm that gives us a pretty good prediction of the rating, and a regression was the best way of doing this. We will be able to use any column in the dataframe for our model except the rating of course. The test statistic to be chosen is R^2. For my model, the test statistic chosen is r^2. This makes sense and it what we want since we want a correlation coefficient of how accurate our model can get when predicting the rating scores of given recipes. The correlation coefficient will determine how similar the data points on our training are to the test set. <br>


**Question: Baseline Model** <br>
<pr>
Our model is a DecisionTree Regression model with 20 steps. I later change this to 174 steps after tuning the hyperparameter, but in my base model it is 20. I only have a few features right now which are minutes, and all the nutrition. I am using a quantile transformer on the minutes column, and a standard scaler on all the nutrition info like calories, sugar, sodium, protein, etc. All the data I have in this model right now, 8 variables and 2 features, is quantitative. They are all numbers which allows me to use simple transformers on them without any encoding. In the final model, I have 2 more quantitative variables which are the number of ingredients and the number of steps, but I also have 2 columns of nominal data, which are ingredients and reviews. These are nominal since they are categorical data that cannot be ordered. In the final model, I convert this into quantitative data that I can use by identifying if certain key terms is in the data. Right now, my model is not good. I only have 2 features which produce an absolute value R^2 score of only 0.12. This does not show any correlation and my model cannot predict the scores at this point. <br>


**Question: Final Model** <br>
<pr>
I chose a Decision Tree Regressive model since there was a lot of data, and Decision Trees are relatively fast at sifting through a lot of data and a lot of variables. They make good and fast choices about using certain features, meaning they are ideal for what I wanted to do.

The features I included in my model are: all of the nutrition info. I included this simply because the data was available. Each category in the nutrition doesn't affect the model too much, but at the end of the day, this is a huge bulk of data and it makes sense why rating would be affected by the nutrition info. Meals that are tastier (have more sugar and fat) may get a better review. Since I just wanted to include this data in my model, but I was not sure the relationship of each category, I just used the standard scaler transformer. 

I then used a QuantileTransformer on the ingredients and steps columns. It makes sense to me that meals that have more ingredients and steps longer usually taste better than small recipes, but small recipes are quicker and easier to make. This felt like a gradual trend to me, where small, medium, and large recipes are different, but I wasn't too sure about this prediction. Therefore, I went with a quantile transformer with 3 quantiles to try and predict that column. I did not tune this hyperparamter, however 3 quartiles felt like good separation. There would still be noticeable categories for each quantile and the model wouldn't be skewed that much because of this since the data points wouldn't be changing too much.

For the minutes column, I used a Binarizer. Again, with the same principle as the ingredients and steps columns, I thought that recipes with a longer prep time would taste better but may be harder to make. With this, I felt that the data was more one sided towards longer recipes being higher rated since prep time is not too bad of a downside when compared to tasty food. Therefore, I used a binarizer, to make the feature be more powerful. After binarizing, Low values would appear much different than high values to the model, which would make the feature have more influence. I set the threshold as 30 minutes. I ran a small for loop to iterate over i values from 0-60. This was to tune for the threshold hyperparameter. Values around 30 minutes performed the best so that is why I chose 30 minutes.

Finally, I implemented FunctionTransformers. I originally wanted to one-hot-code the review and ingredients columns, but couldn't since the data was in lists. One-hot-coding the ingredients in each list and words in each review would be too much for the model to perform in a timely manner, and it would most likely overfit the data, so instead I used custom helper functions that checked if a row contained certain values in these columns. I used a function transformer for 7 small helper functions I made. In the review column, I checked to see if a review had the words "good", "great, "amazing", or "delicious". In the ingredients column, I applied a different function transformer to see if "butter", "sugar", or "cheese" was in the list of ingredients since everyone loves these things. 

Since I applied different transformers to different columns, I used a column transformer and put all my other transformers inside of it.

I tuned the max depth hyper parameter for the decision tree and iteratively ran a for loop to get the best max-depth. I simply just ran a for loop, creating and scoring each pipeline for each max depth value, ranging from 1 to 200. 200 iterations was a bit extra, especially because it took a while to run, but I wanted to be as accurate as possible.

Compared to my original model, my final model is much better. With an average absolute value test R^2 score of around 0.65, my model is much better at predicting the rating of recipes. This means that there is a trend that I am able to slightly generate with my model. As opposed to my original model which was not accurate at all, my final model icorporates more features and is able to predict data petter<br>

---

