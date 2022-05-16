# Concrete-strength----regression
![output](https://user-images.githubusercontent.com/79353291/168518515-5afbe493-ebfc-4c15-8d9b-ad2a071f2627.png)
# Analysis objectives
* Predict the compressive strength of concrete based on its age and ingredients
* Compare the performance of regression algorithms such as: linear regression, lasso regression, ridge regression, k nearest neighbors, decision tree, random forest, support vector machine, and xgboost.
* The metric that will be used to identify the best perfroming model is the cross validation MAE.
* We will also use other metrics such as MSE, MAE, and R2 on train and test sets in order to detect overfitting.
* We will compare the performance of each model before and after hyperparameter tuning
# Dataset that will be utilized
* [link for the dataset](https://archive.ics.uci.edu/ml/datasets/concrete+compressive+strength)
* [link for the notebook](https://github.com/raminstad/Concrete-strength----regression/blob/main/Final.ipynb)
# Exploratory data analysis
* Descriptive statistics
* Heatmap of correlation
* Boxplots
* Jointplots
* Pairplots
* QQ-plots
* Regression analysis
### Regression analysis
* In this step I fit a linear regression using the statsmodels package and I used the whole dataset for this part, the reason is that this is a data mining process and we want to find any hidden layer and patterns in the dataset.
* Summary of the model:
![Screen Shot 2022-05-15 at 9 25 22 PM (3)](https://user-images.githubusercontent.com/79353291/168519678-8e2a7d10-5b54-4806-928e-492284ccf7ae.png)

* R-squared is 0.60 which means that our predictors explain 60% of the variance of our target variable, which is a reasonable amount.
* P-value of the F-statistics is < 0.05 meaning that our predictors as a whole are good predictors
* P-value of each predictor is < 0.05 and that means they are significant, the only ones that are not < 0.05 are fine and coarse agrregates
* In conclusion of this model we can see that we are almost ready for building ML models and start making pipelines, but before we can visualize this model
*  ![output](https://user-images.githubusercontent.com/79353291/168520160-420e7ac8-5f25-4c8f-a0fb-fd432f9fd576.png)
#### Intepreting the diagnostic plots above
##### Residuals vs Fitted:
The red line(Loess curve) helps us assess linearity and if the line is mostly straight and cuts across the graph around y=0, the relationship between input and output is linear, for this example we can conclude that the relationship is almost linear.
To assess the equality of the variance we can look at the distribution of the points and we can see that the distribution is almost the same all across the graph, therefore the variance is equall.
<br>
##### Normal QQ-plot:
We can see that our model is normally distributed meaning that the coefficient estimates are affected, and the coefficient hypothesis tests is more trustworthy because the standard errors of the t-tests will not be too small.
<br>
##### Scale location:
We can see this plot is the same as residuals vs fitted and the only difference is that the residuals on the y axis are standardized.
<br>
##### Residuals vs Levarage:
This plolt shows the outliers on Y given X, and it measures the cooks distance, we can see the graph is not showing any major outliers.
