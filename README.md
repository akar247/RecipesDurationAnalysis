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

<strong>Our cleaned dataset:</strong>

<br>

<iframe style="background: #E5D1CD;"
         src="assets/df_head2.html" width=800 height=800 frameBorder=1>
</iframe>

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

<strong>Count of Recipes with a Certain Number of Steps and Duration</strong>
<table border="1" class="dataframe">   <thead>     <tr style="text-align: right;">       <th>step_intervals</th>       <th>(0.999, 4.0]</th>       <th>(4.0, 5.0]</th>       <th>(5.0, 6.0]</th>       <th>(6.0, 8.0]</th>       <th>(8.0, 9.0]</th>       <th>(9.0, 10.0]</th>       <th>(10.0, 12.0]</th>       <th>(12.0, 14.0]</th>       <th>(14.0, 18.0]</th>       <th>(18.0, 93.0]</th>     </tr>     <tr>       <th>minute_intervals</th>       <th></th>       <th></th>       <th></th>       <th></th>       <th></th>       <th></th>       <th></th>       <th></th>       <th></th>       <th></th>     </tr>   </thead>   <tbody>     <tr>       <th>(-0.001, 10.0]</th>       <td>4.698</td>       <td>4.689</td>       <td>4.684</td>       <td>4.681</td>       <td>4.665</td>       <td>4.630</td>       <td>4.581</td>       <td>4.617</td>       <td>4.656</td>       <td>4.759</td>     </tr>     <tr>       <th>(10.0, 15.0]</th>       <td>4.645</td>       <td>4.642</td>       <td>4.622</td>       <td>4.629</td>       <td>4.621</td>       <td>4.681</td>       <td>4.594</td>       <td>4.701</td>       <td>4.702</td>       <td>4.564</td>     </tr>     <tr>       <th>(15.0, 25.0]</th>       <td>4.625</td>       <td>4.598</td>       <td>4.614</td>       <td>4.649</td>       <td>4.644</td>       <td>4.577</td>       <td>4.634</td>       <td>4.637</td>       <td>4.619</td>       <td>4.649</td>     </tr>     <tr>       <th>(25.0, 30.0]</th>       <td>4.577</td>       <td>4.523</td>       <td>4.638</td>       <td>4.611</td>       <td>4.632</td>       <td>4.589</td>       <td>4.640</td>       <td>4.655</td>       <td>4.616</td>       <td>4.681</td>     </tr>     <tr>       <th>(30.0, 35.0]</th>       <td>4.618</td>       <td>4.550</td>       <td>4.573</td>       <td>4.609</td>       <td>4.593</td>       <td>4.625</td>       <td>4.627</td>       <td>4.609</td>       <td>4.629</td>       <td>4.668</td>     </tr>     <tr>       <th>(35.0, 45.0]</th>       <td>4.571</td>       <td>4.546</td>       <td>4.577</td>       <td>4.624</td>       <td>4.581</td>       <td>4.587</td>       <td>4.598</td>       <td>4.619</td>       <td>4.614</td>       <td>4.630</td>     </tr>     <tr>       <th>(45.0, 55.0]</th>       <td>4.605</td>       <td>4.623</td>       <td>4.598</td>       <td>4.614</td>       <td>4.565</td>       <td>4.595</td>       <td>4.619</td>       <td>4.592</td>       <td>4.618</td>       <td>4.680</td>     </tr>     <tr>       <th>(55.0, 70.0]</th>       <td>4.651</td>       <td>4.591</td>       <td>4.595</td>       <td>4.603</td>       <td>4.608</td>       <td>4.643</td>       <td>4.600</td>       <td>4.575</td>       <td>4.637</td>       <td>4.608</td>     </tr>     <tr>       <th>(70.0, 120.0]</th>       <td>4.583</td>       <td>4.642</td>       <td>4.617</td>       <td>4.634</td>       <td>4.648</td>       <td>4.614</td>       <td>4.634</td>       <td>4.614</td>       <td>4.623</td>       <td>4.651</td>     </tr>     <tr>       <th>(120.0, 1440.0]</th>       <td>4.513</td>       <td>4.567</td>       <td>4.533</td>       <td>4.552</td>       <td>4.591</td>       <td>4.592</td>       <td>4.624</td>       <td>4.584</td>       <td>4.646</td>       <td>4.659</td>     </tr>   </tbody> </table>

<br>
<br>

Although this pivot table is very large, it does reveal some key aspects of the dataset to us. The pivot table shows us how often a certain pairing of cooking duration (index) and number of steps (column) for a recipe takes. We can use this to understand the frequency in which a small number of steps recipe of high cooking duration can take place. It is a more quantitative way of looking at the data illustrated by the first bivariate plot above. 

<br>
<br>

<strong>Average Rating of Recipes with a Certain Number of Steps and Duration</strong>
<table border="1" class="dataframe">    <thead>      <tr style="text-align: right;">        <th>step_intervals</th>        <th>(0.999, 4.0]</th>        <th>(4.0, 5.0]</th>        <th>(5.0, 6.0]</th>        <th>(6.0, 8.0]</th>        <th>(8.0, 9.0]</th>        <th>(9.0, 10.0]</th>        <th>(10.0, 12.0]</th>        <th>(12.0, 14.0]</th>        <th>(14.0, 18.0]</th>        <th>(18.0, 93.0]</th>      </tr>      <tr>        <th>minute_intervals</th>        <th></th>        <th></th>        <th></th>        <th></th>        <th></th>        <th></th>        <th></th>        <th></th>        <th></th>        <th></th>      </tr>    </thead>    <tbody>      <tr>        <th>(-0.001, 10.0]</th>        <td>4.697591</td>        <td>4.688950</td>        <td>4.684050</td>        <td>4.681141</td>        <td>4.665074</td>        <td>4.630320</td>        <td>4.581278</td>        <td>4.616916</td>        <td>4.656139</td>        <td>4.759218</td>      </tr>      <tr>        <th>(10.0, 15.0]</th>        <td>4.644595</td>        <td>4.641828</td>        <td>4.621687</td>        <td>4.629146</td>        <td>4.620964</td>        <td>4.681142</td>        <td>4.594191</td>        <td>4.701465</td>        <td>4.702122</td>        <td>4.564014</td>      </tr>      <tr>        <th>(15.0, 25.0]</th>        <td>4.625323</td>        <td>4.597852</td>        <td>4.613715</td>        <td>4.649018</td>        <td>4.644401</td>        <td>4.576617</td>        <td>4.634405</td>        <td>4.636828</td>        <td>4.618853</td>        <td>4.649240</td>      </tr>      <tr>        <th>(25.0, 30.0]</th>        <td>4.577133</td>        <td>4.523450</td>        <td>4.637632</td>        <td>4.610962</td>        <td>4.632499</td>        <td>4.588864</td>        <td>4.639699</td>        <td>4.655316</td>        <td>4.615830</td>        <td>4.681089</td>      </tr>      <tr>        <th>(30.0, 35.0]</th>        <td>4.617714</td>        <td>4.550049</td>        <td>4.573294</td>        <td>4.608581</td>        <td>4.592896</td>        <td>4.625405</td>        <td>4.626785</td>        <td>4.608538</td>        <td>4.629388</td>        <td>4.668249</td>      </tr>      <tr>        <th>(35.0, 45.0]</th>        <td>4.570829</td>        <td>4.546187</td>        <td>4.577294</td>        <td>4.623955</td>        <td>4.580561</td>        <td>4.586825</td>        <td>4.597617</td>        <td>4.619128</td>        <td>4.614107</td>        <td>4.630323</td>      </tr>      <tr>        <th>(45.0, 55.0]</th>        <td>4.604569</td>        <td>4.623060</td>        <td>4.597770</td>        <td>4.614312</td>        <td>4.565035</td>        <td>4.594741</td>        <td>4.618589</td>        <td>4.592197</td>        <td>4.618144</td>        <td>4.680084</td>      </tr>      <tr>        <th>(55.0, 70.0]</th>        <td>4.650563</td>        <td>4.591420</td>        <td>4.595263</td>        <td>4.603422</td>        <td>4.607877</td>        <td>4.642839</td>        <td>4.599820</td>        <td>4.574830</td>        <td>4.637467</td>        <td>4.608026</td>      </tr>      <tr>        <th>(70.0, 120.0]</th>        <td>4.582917</td>        <td>4.642091</td>        <td>4.617224</td>        <td>4.633922</td>        <td>4.648394</td>        <td>4.614256</td>        <td>4.633772</td>        <td>4.614396</td>        <td>4.622920</td>        <td>4.650864</td>      </tr>      <tr>        <th>(120.0, 1440.0]</th>        <td>4.513094</td>        <td>4.566683</td>        <td>4.532794</td>        <td>4.551563</td>        <td>4.590504</td>        <td>4.592298</td>        <td>4.624165</td>        <td>4.583869</td>        <td>4.646041</td>        <td>4.658942</td>      </tr>    </tbody>  </table>

<br>
<br>

The next pivot table has the same index and columns, but the values are now the average ratings for each of those values. This table contains information for the average rating for a recipe that has x amount of steps and takes y amount of minutes to cook. From this, we can look at the distribution of ratings relative to step size and duration.

<br>
<br>

</center>


</p>

---

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

The <code>description<code> column in this dataset is likely NMAR. While it is possible that descriptions may be missing because the title is self-explanatory, there are descriptions that have nothing to do with the title or the food item itself. This implies that descriptions aren't missing dependent on the 'name' column, and it likely isn't dependent on other columns. They could be missing dependent on themselves because the owner of the recipe felt that they couldn't think of a description that warranted writing it in the first place. The owner felt that there was nothing important to say about the recipe, so there was no need to write a description. The missingness of description is dependent on the descriptions themselves.


<br>
<br>


Second, <strong>Missing Dependency</strong>:

<br>
<br>


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

 <center><i>Is their a relationship between cooking duration and average rating? </i></center>

 <br>
 <br>

 We conducted a permutation hypothesis test focusing on the relationship between cooking duration and recipe rating. 

<br>
<br>

<h3> <strong>Null</strong> </h3>


<strong>Null Hypothesis</strong>: 
<br>

&emsp;The average rating of a recipe is not related to the cooking duration of that recipe.

<br>
<br>

<strong>Choosing the Null</strong>: 
<br>

&emsp;We chose this null hypothesis because it assumes there is no relationship between these two variables, which is what we are testing to reject, which is good for answering our question.

<br>
<br>

<h3> <strong>Alternate</strong> </h3>


<strong>Alternate Hypothesis</strong>: 
<br>

&emsp;The average rating of a recipe decreases the longer the cooking duration of that recipe.

<br>
<br>

<strong>Choosing the Alternative</strong>: 
<br>

&emsp;We chose this alternative because it matches our intuition that people who have spent longer cooking a recipe may be more cynical or harsh towards the recipe because of the time they've invested, whereas people cooking shorter recipes won't be as harsh when rating it since they didn't lose as much time.

<br>
<br>

<h3> <strong>Test Statistic</strong> </h3>

<br>

<strong>Test Statistic</strong>: 
<br>

&emsp;The test statistic we decided to use was the difference in average cooking duration for low rated recipes on average [1, 3.5) and high rated recipes on average [3.5, 5]

<br>
<br>

<strong>Choosing the Test Statistic</strong>: 
<br>

&emsp;Using the difference in mean cooking times is a valid test statistic because cooking duration is a numerical distribution. We divided the averages between low and high rated recipes to see if the cooking durations were different dependent on average rating.

<br>
<br>

<h3> <strong>Assumptions and Results</strong> </h3>

<br>

<strong>Significance Level</strong>: 
<br>

&emsp;We chose our significance level to be 0.05 since this is the standard level for hypothesis tests that do not require extreme accuracy. 

<br>
<br>

<strong>Conclusion</strong>: 
<br>

&emsp;Our resulting p-value was 0.00.

<br>
<br>

&emsp;Since our p-value is less than our stated significance value, we reject the null hypothesis. There is evidence that is not consistent with our null hypothesis that average rating and cooking duration are not related.


</p>

<br>

---

<br>
<br>

<center>

<h2><i>That is all!</i></h2>

</center>