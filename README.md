Report on how the duration of a recipe is (based on number of steps, number of ingredients, time till completion) affects its average rating.




## <strong>Getting the Data</strong>

<p>

The dataset we used came from [food.com](https://dsc80.com/project3/recipes-and-ratings/food.com), which offered a vast number of recipes and ratings associated with each recipe based off individual users. There were two datasets initially, the raw recipes info stored in <code>RAW_recipes.csv</code> and the reviews / ratings associated with each recipe was stored in <code>RAW_interactions.csv</code>. 

<br>
<br>

Our initial formatting of the data was to left merge the recipes and interactions datasets on the <code>id</code> column of the recipes and the <code>recipe_id</code> column of the interactions. Furthermore, we changed all ratings of value 0 to np.NaN values since ratings are supposed to be values from 1 - 5 so 0 was an invalid value for ratings and should not be considered in our analysis. We compute the average rating of each recipe and stored it into the merged dataframe as <code>rating_average</code>.

<br>
<br>

Once we had formatted the dataframe and were able to take a thorough look into the dataset, we decided that the question we could ask from this dataset is:


<center><b> What is the Relationship Between Cooking Duration and Average Rating? </b></center>


<br>

The key reason why you should be interested in our analysis of this dataset is because we analyze the true reasons behind lower ratings of recipes. Through our analysis one will understand the objective reasoning behind a recipe's rating and can align that to their own preferences in order to choose better recipes to pursue. 

<br>
<br>

For the purposes of this analysis we will be taking a holistic approach of considering all the columns in our data analysis but for the purposes of our question the relevant columns are:

<br>
<br>

&emsp; 1. <code>name</code> : The recipe name as denoted by the user who submitted the recipe

<br>

&emsp; 2. <code>minutes</code> : The time it takes (in minutes) to prepare a recipe

<br>

&emsp; 3. <code>n_steps</code> : The number of steps outlined in a recipe

<br>

&emsp; 4. <code>n_ingredients</code> : The number of ingredients required to prepare a recipe

<br>

&emsp; 5. <code>rating_average</code> : The average rating of each recipe by all users that submitted the 
recipe

<br>


</p>

<br>

---

<br>

### <strong>Cleaning and EDA (Exploratory Data Analysis)</strong>

<P>



The process of cleaning our dataset goes as follows:

<br>
<br>

&emsp; 1. Correcting column data types

<br>

&emsp;&emsp; - The columns <code>tags</code>, <code>nutrition</code>, <code>ingredients</code>, and <code>steps</code> were all lists that were considered strings. We converted them to list types. 

<br>

&emsp;&emsp; - We converted the <code>submitted</code> and <code>date</code> columns to datetime values. 

<br>

&emsp;&emsp; - We converted <code>user_id</code> and <code>recipe_id</code> to numeric types (int).

<br>
<br>

&emsp; 2. Removing extreme values

<br>

&emsp;&emsp; - We remove cooking times that were longer than 24 hours. 


<br>
<br>
    
&emsp;&emsp; Our reasoning for this was because we wanted to have a realistic dataset in the sense that were recipes that the everyday person would challenge themselves with. We felt like recipes that would take longer than 24 hours would require a commitment that was only present among chefs that do this for a living rather than a hobby or pastime. Since we are considering the ratings of these recipes we felt that these instances wouldn't reflect the general population's rating since they would find harder and challenging steps much easier since they are much more seasoned in this field. 

<br>
<br>

<strong>Our cleaned dataset</strong>

<br>

<iframe style="background: #E5D1CD;"
         src="assets/df_head.html" width=500 height=300 frameBorder=1>
</iframe>


| name                                 |     id |   minutes |   contributor_id | submitted           | tags                                                                                                                                                                                                                        | nutrition                                    |   n_steps | steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | description                                                                                                                                                                                                                                                                                                                                                                       | ingredients                                                                                                                                                                    |   n_ingredients |          user_id |   recipe_id | date                |   rating_individual | review                                                                                                                                                                                                                                                                                                                                           |   rating_average | missing_rating   |
|:-------------------------------------|-------:|----------:|-----------------:|:--------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------|----------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|-----------------:|------------:|:--------------------|--------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------:|:-----------------|
| 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27 00:00:00 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings'] | [138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]     |        10 | ['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat ', 'stirring frequently ', 'until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs ', 'sugar ', 'cocoa powder ', 'vanilla extract ', 'espresso ', 'and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean ', 'about 25 to 30 minutes', 'remove from the oven and cool completely before cutting']                                                | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour'] |               9 | 386585           |      333281 | 2008-11-19 00:00:00 |                   4 | These were pretty good, but took forever to bake.  I would send it ended up being almost an hour!  Even then, the brownies stuck to the foil, and were on the overly moist side and not easy to cut.  They did taste quite rich, though!  Made for My 3 Chefs.                                                                                   |                4 | False            |
| 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11 00:00:00 | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                               | [595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0] |        12 | ['pre-heat oven the 350 degrees f', 'in a mixing bowl ', 'sift together the flours and baking powder', 'set aside', 'in another mixing bowl ', 'blend together the sugars ', 'margarine ', 'and salt until light and fluffy', 'add the eggs ', 'water ', 'and vanilla to the margarine / sugar mixture and mix together until well combined', 'add in the flour mixture to the wet ingredients and blend until combined', 'scrape down the sides of the bowl and add the chocolate chips', 'mix until combined', 'scrape down the sides to the bowl again', 'using an ice cream scoop ', 'scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', 'bake for 10 - 15 minutes or until golden brown on the outside and soft & chewy in the center', 'serve hot and enjoy !'] | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                    |              11 | 424680           |      453467 | 2012-01-26 00:00:00 |                   5 | Originally I was gonna cut the recipe in half (just the 2 of us here), but then we had a park-wide yard sale, & I made the whole batch & used them as enticements for potential buyers ~ what the hey, a free cookie as delicious as these are, definitely works its magic! Will be making these again, for sure! Thanks for posting the recipe! |                5 | False            |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30 00:00:00 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray ', 'set aside', 'in a large bowl mix together broccoli ', 'soup ', 'one cup of cheese ', 'garlic powder ', 'pepper ', 'salt ', 'milk ', '1 cup of french onions ', 'and soy sauce', 'pour into baking dish ', 'sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly ', 'about 10 more minutes']                                                                                                                                                                                                                                                                                                                      | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |  29782           |      306168 | 2008-12-31 00:00:00 |                   5 | This was one of the best broccoli casseroles that I have ever made.  I made my own chicken soup for this recipe. I was a bit worried about the tsp of soy sauce but it gave the casserole the best flavor. YUM!                                                                                                                                  |                5 | False            |
|                                      |        |           |                  |                     |                                                                                                                                                                                                                             |                                              |           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                   |                                                                                                                                                                                |                 |                  |             |                     |                     | The photos you took (shapeweaver) inspired me to make this recipe and it actually does look just like them when it comes out of the oven.                                                                                                                                                                                                        |                  |                  |
|                                      |        |           |                  |                     |                                                                                                                                                                                                                             |                                              |           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                   |                                                                                                                                                                                |                 |                  |             |                     |                     | Thanks so much for sharing your recipe shapeweaver. It was wonderful!  Going into my family's favorite Zaar cookbook :)                                                                                                                                                                                                                          |                  |                  |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30 00:00:00 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray ', 'set aside', 'in a large bowl mix together broccoli ', 'soup ', 'one cup of cheese ', 'garlic powder ', 'pepper ', 'salt ', 'milk ', '1 cup of french onions ', 'and soy sauce', 'pour into baking dish ', 'sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly ', 'about 10 more minutes']                                                                                                                                                                                                                                                                                                                      | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |      1.19628e+06 |      306168 | 2009-04-13 00:00:00 |                   5 | I made this for my son's first birthday party this weekend. Our guests INHALED it! Everyone kept saying how delicious it was. I was I could have gotten to try it.                                                                                                                                                                               |                5 | False            |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30 00:00:00 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray ', 'set aside', 'in a large bowl mix together broccoli ', 'soup ', 'one cup of cheese ', 'garlic powder ', 'pepper ', 'salt ', 'milk ', '1 cup of french onions ', 'and soy sauce', 'pour into baking dish ', 'sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly ', 'about 10 more minutes']                                                                                                                                                                                                                                                                                                                      | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 | 768828           |      306168 | 2013-08-02 00:00:00 |                   5 | Loved this.  Be sure to completely thaw the broccoli.  I didn&#039;t and it didn&#039;t get done in time specified.  Just cooked it a little longer though and it was perfect.  Thanks Chef.                                                                                                                                                     |                5 | False            |

<br>



<br>
<br>

For our <strong>EDA</strong>, we focused on 3 main forms of analysis, univariate, bivariate, and aggregates. 

<br>
<br>


&emsp; <strong>1. Univariate Analysis:</strong>

<br>
<br>

    For our univariate analysis we create multiple distributions of the relevant columns of our dataset. This allowed us to easily view the spread, mins, maxes, and skew of the values for each column of data. We created these distributions for the cooking times, number of steps in recipes, number of ingredients in recipes, and the average ratings of recipes. The plots are shown below. 

<br>
<br>

<center>

<iframe src="assets/univariate_times.html" width=600 height=400 frameBorder=1></iframe>

<br>
<br>

From this distribution we notice that there is a massive range of times for which recipes are made, even when we narrow down the times to less than a day, however the greatest number of recipes occur when the duration is about an hour or less (~ 72 minutes)

<br>
<br>

<iframe src="assets/univariate_steps.html" width=600 height=400 frameBorder=1></iframe>

<br>
<br>

Similarly to the distribution of cooking duration, the number of stpes has a very positively skewed graph where most recipes have it's number of steps between 5 - 10 with the overwhlming majority as recipes with less than 20 steps. 

<br>
<br>

<iframe src="assets/univariate_ingred.html" width=600 height=400 frameBorder=1></iframe>

<br>
<br>

The distribution for the number of ingredients is actually relatively normal with the exception for a couple of outlier recipes that contain more than 25 recipes. Other than these cases, the distribution is centered around 10 ingredients for a recipe. 

<br>
<br>

<iframe src="assets/univariate_ratings.html" width=600 height=400 frameBorder=1></iframe> 

<br>
<br>

This distribution illustrates a very interesting aspect of the data where the average ratings is strongly negatively skewed with the majority of the ratings being greater than a 4.5. We have found this interesting simply due to the general idea that the more likely people to leave reviews and ratings when optional is the population of people that have strong dissatisfaction of a product or service. 

<br>
<br>

</center>

<br>
<br>

&emsp; <strong>2. Bivariate Analysis:</strong>

<br>
<br>

    For our bivariate analysis we wanted to understand the relationship between key quantitative values within our dataset. The graphs of these relationships allowed us to understand the rough association between two variables and gave us better insight on how the increase / decrease of minutes or steps might affect other variables. The plots are shown below. 

<br>
<br>

<center>

<iframe src="assets/bivariate_mins_steps.html" width=600 height=400 frameBorder=1></iframe>

<br>
<br>

This plot illustrates the relationship between the number of steps a recipe has and the average duration (in minutes) that recipe takes. From this graph we are able to tell that there is a positive relationship between the two variables (increasing the number of steps of a recipe increases that recipes duration) except for a gap in the data where there are no recipes of 45 - 75 steps. 

<br>
<br>

<iframe src="assets/bivariate_mins_ingred.html" width=600 height=400 frameBorder=1></iframe>

<br>
<br>

The plot of the number of ingredients against the average duration of a recipe is similar to the previous graph excep its domain is much smaller. It also does not seem to have as much of a linear relationship as it could be a quadratic relationship as the average duration sharply increases when there are 20 - 25 ingredients in the recipe. 

<br>
<br>

<iframe src="assets/bivariate_mins_ratings.html" width=600 height=400 frameBorder=1></iframe>

<br>
<br>
<br>

</center>

&emsp; <strong>3. Aggregates:</strong>

<br>
<br>

    We also calculated some interesting aggregate values through pivot tables. This illustrated to us the general break down how often certain pairs of complexities occurred and if the average occurence of certain aggregates were ever out of the ordinary.

<br>
<br>

<center>

<iframe src="assets/pt_1.*" width=600 height=400 frameBorder=1></iframe>

<br>
<br>

Although this pivot table is very large, it does reveal some key aspects of the dataset to us. The pivot table shows us how often a certain pairing of cooking duration (index) and number of steps (column) for a recipe takes. We can use this to understand the frequency in which a small number of steps recipe of high cooking duration can take place. It is a more quantitative way of looking at the data illustrated by the first bivariate plot above. 

<br>
<br>

</center>


</p>

---

<br>
<br>
<br>

## <strong>Assessment of Missingness</strong>

<br>
<br>

<p>

To assess the types of missingness present in our data we conducted two forms of analysis:
<br>
<br>

<ol type="1">
  <li>Not Missing at Random:
    <ol type='i'>
        <li> 
            We analyzed the relevant columns in our dataset to find a a column with missing values that were independent of the rest of the data except for its own value.
        </li>
    </ol>
  </li>
</ol>

<br>

<ol start="2">
  <li>Missing Dependency:
    <ol type='i'>
        <li>
            Utilizing permuation tests were able to locate a column that showed cleared evidence for having missingness dependent on a column and independent missingness dependent on another column. 
        </li>
    </ol>
  </li>
</ol>

<br>
<br>

First, <strong>NMAR</strong>:

<br>
<br>

The "description" column in this dataset is likely NMAR. While it is possible that descriptions may be missing because the title is self-explanatory, there are descriptions that have nothing to do with the title or the food item itself. This implies that descriptions aren't missing dependent on the 'name' column, and it likely isn't dependent on other columns. They could be missing dependent on themselves because the owner of the recipe felt that they couldn't think of a description that warranted writing it in the first place. The owner felt that there was nothing important to say about the recipe, so there was no need to write a description. The missingness of description is dependent on the descriptions themselves.


<br>
<br>


Second, <strong>Missing Dependency</strong>:


</p>


<br>
---
<br>

## <strong>Hypothesis Testing</strong>

<br>

<p>

To answer our question: 
<br>
<br>

 <center><i>Is their a relationship between cooking duration and average rating> </i></center>

 <br>
 <br>
 
 we conducted a permutation test


 We conducted a permutation hypothesis test focusing on the relationship between cooking duration and recipe rating. 

<br>
<br>

### <strong>Null</strong>

<br>

<strong>Null Hypothesis</strong>: 
<br>

&emsp;The average rating of a recipe is not related to the cooking duration that recipe.


<strong>Choosing the Null</strong>: 
<br>

&emsp;We chose this null hypothesis because it assumes there is no relationship between these two variables, which is what we are testing to reject, which is good for answering our question.

<br>

### <strong>Alternate</strong>

<br>

<strong>Alternate Hypothesis</strong>: 
<br>

&emsp;The average rating of a recipe decreases the longer the cooking duration of that recipe.

<br>

<strong>Choosing the Alternative</strong>: 
<br>

&emsp;We chose this alternative because it matches our intuition that people who have spent longer cooking a recipe may be more cynical or harsh towards the recipe because of the time they've invested, whereas people cooking shorter recipes won't be as harsh when rating it since they didn't lose as much time.

<br>

### <strong>Test Statistic</strong>

<br>

<strong>Test Statistic</strong>: 
<br>

&emsp;The test statistic we decided to use was the difference in average cooking duration for low rated recipes on average [1, 3.5) and high rated recipes on average [3.5, 5]

<br>

<strong>Choosing the Test Statistic</strong>: 
<br>

&emsp;Using the difference in mean cooking times is a valid test statistic because cooking duration is a numerical distribution. We divided the averages between low and high rated recipes to see if the cooking durations were different dependent on average rating.

<br>

### <strong>Assumptions and Results</strong>

<br>

<strong>Significance Level</strong>: 
<br>

&emsp;We chose our significance level to be 0.05 since this is the standard level for hypothesis tests that do not require extreme accuracy. 

<br>

<strong>Conclusion</strong>: 
<br>

&emsp;Our resulting p-value was 0.00.

<br>

&emsp;Since our p-value is less than our stated significance value, we reject the null hypothesis. There is evidence that is not consistent with our null hypothesis that average rating and cooking duration are not related.


</p>

<br>

---

<br>
<br>

<center>

# <i>That is all!</i>

</center>