Report on how the complexity of a recipe is (based on number of steps, number of ingredients, time till completion) affects its average rating.




### **Getting the Data**

<p>

The dataset we used casme from [food.com](https://dsc80.com/project3/recipes-and-ratings/food.com), which offered a vast number of recipes and ratings associated with each recipe based off individual users. There were two datasets initially, the raw recipes info stored in `RAW_recipes.csv` and the reviews / ratings associated with each recipe was stored in `RAW_interactions.csv`. 

<br>
<br>

Our initial formatting of the data was to left merge the recipes and interactions datasets on the `id` column of the recipes and the `recipe_id` column of the interactions. Furthermore, we changed all ratings of value 0 to np.NaN values since ratings are supposed to be values from 1 - 5 so 0 was an invalid value for ratings and should not be considered in our analysis. We compute the average rating of each recipe and stored it into the merged dataframe as `rating_average`.

<br>
<br>

Once we had formatted the dataframe and were able to take a thorough look into the dataset, we decided that the question we could ask from this dataset is:


<center><b> What is the Relationship Between Cooking Complexity and Average Rating? </b></center>

<center> Complexity depended on a recipe's number of steps, number of ingredients, and cooking duration </center>

<br>

The key reason why you should be interested in our analysis of this dataset is because we analyze the true reasons behind lower ratings of recipes. Through our analysis one will understand the objective reasoning behind a recipe's rating and can align that to their own preferences in order to choose better recipes to pursue. 

<br>
<br>

For the purposes of this analysis we will be taking a holistic approach of considering all the columns in our data analysis but for the purposes of our question the relevant columns are:

<br>
<br>

&emsp; 1. `name` : The recipe name as denoted by the user who submitted the recipe

<br>

&emsp; 2. `minutes` : The time it takes (in minutes) to prepare a recipe

<br>

&emsp; 3. `n_steps` : The number of steps outlined in a recipe

<br>

&emsp; 4. `n_ingredients` : The number of ingredients required to prepare a recipe

<br>

&emsp; 5. `rating_average` : The average rating of each recipe by all users that submitted the 
recipe

<br>


</p>

<br>

---

<br>

### **Cleaning and EDA (Exploratory Data Analysis)**

<P>



The process of cleaning our dataset goes as follows:

<br>
<br>

&emsp; 1. Correcting column data types

<br>
<br>

&emsp;&emsp; - The columns `tags`, `nutrition`, `ingredients`, and `steps` were all lists that were considered strings. We converted them to list types. 

<br>

&emsp;&emsp; - We converted the `submitted` and `date` columns to datetime values. 

<br>

&emsp;&emsp; - We converted `user_id` and  `recipe_id` to numeric types (int).

<br>
<br>

&emsp; 2. Removing extreme values
&emsp;&emsp; - We remove cooking times that were longer than 24 hours. 
    
&emsp;&emsp; Our reasoning for this was because we wanted to have a realistic dataset in the sense that were recipes that the everyday person would challenge themselves with. We felt like recipes that would take longer than 24 hours would require a commitment that was only present among chefs that do this for a living rather than a hobby or pastime. Since we are considering the ratings of these recipes we felt that these instances wouldn't reflect the general population's rating since they would find harder and challenging steps much easier since they are much more seasoned in this field. 


<br>
<br>

For our EDA, we focused on 3 main forms of analysis, univariate, bivariate, and aggregates. 

<br>
<br>


#### &emsp; 1. Univariate Analysis:

<br>
<br>

    For our univariate analysis we create multiple distributions of the relevant columns of our dataset. This allowed us to easily view the spread, mins, maxes, and skew of the values for each column of data. We created these distributions for the cooking times, number of steps in recipes, number of ingredients in recipes, and the average ratings of recipes. The plots are shown below. 

<br>
<br>

<center>

<iframe src="assets/univariate_times.html" width=600 height=400 frameBorder=1></iframe>

<br>
<br>

<iframe src="assets/univariate_steps.html" width=600 height=400 frameBorder=1></iframe>

<br>
<br>

<iframe src="assets/univariate_ingred.html" width=600 height=400 frameBorder=1></iframe>

<br>
<br>

<iframe src="assets/univariate_ratings.html" width=600 height=400 frameBorder=1></iframe> 

<br>
<br>

</center>

<br>
<br>

#### &emsp; 2. Bivariate Analysis:

<br>
<br>

    For our bivariate analysis we wanted to understand the relationship between key quantitative values within our dataset. The graphs of these relationships allowed us to understand the rough association between two variables and gave us better insight on how the increase / decrease of minutes or steps might affect other variables. The plots are shown below. 

<br>
<br>

<center>

<iframe src="assets/bivariate_mins_steps.html" width=600 height=400 frameBorder=1></iframe>

<br>
<br>

<iframe src="assets/bivariate_mins_ingred.html" width=600 height=400 frameBorder=1></iframe>

<br>
<br>

<iframe src="assets/bivariate_mins_ratings.html" width=600 height=400 frameBorder=1></iframe>

<br>
<br>

</center>

#### &emsp; 2. Aggregates:

<br>
<br>

    We also calculated some interesting aggregate values through pivot tables. This illustrated to us the general break down how often certain pairs of complexities occurred and if the average occurence of certain aggregates were ever out of the ordinary.

<br>
<br>

<center>

<iframe src="assets/pt_1.html" width=600 height=400 frameBorder=1></iframe>

<br>
<br>

<iframe src="assets/pt_2.html" width=600 height=400 frameBorder=1></iframe>

<br>
<br>

</center>


</p>



