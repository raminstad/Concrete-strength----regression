# Concrete-strength----regression
![kisspng-cement-mixers-concrete-finisher-clip-art-cement-5acc1179519000 4040089215233232573341](https://user-images.githubusercontent.com/79353291/168522077-25f1c007-5c9b-4c09-b385-e4f4cb77849d.jpg)
* [link for the notebook](https://github.com/raminstad/Concrete-strength----regression/blob/main/Final.ipynb)
# Analysis objectives
* Predict the compressive strength of concrete based on its age and ingredients
* Compare the performance of regression algorithms such as: linear regression, lasso regression, ridge regression, k nearest neighbors, decision tree, random forest, support vector machine, and xgboost.
* The metric that will be used to identify the best perfroming model is the cross validation MAE.
* We will also use other metrics such as MSE, MAE, and R2 on train and test sets in order to detect overfitting.
* We will compare the performance of each model before and after hyperparameter tuning
# Dataset that will be utilized
* [link for the dataset](https://archive.ics.uci.edu/ml/datasets/concrete+compressive+strength)

# Potential packages
* Pandas
* Numpy
* Matplotlib
* Seaborn
* Statsmodel
* Sklearn
# Exploratory data analysis
* Descriptive statistics
* Heatmap of correlation
* Boxplots
* Jointplots
* Pairplots
* QQ-plots
* Regression analysis
# Data preprocessing
* Drop duplicates
* Min Max Scaler
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

# Model construction
* We strat by making pipelines including the minmax scaler and the estimator on each pipeline and fit each model
* Reason for using pipeline is to chain multiple process together, and also pipelines prevent data leackage when we are working with scalers
* We predict on train and test sets to detect overfitting
* We perform crossvalidation to detect overfitting and use it as the main score for model performance
* ![output](https://user-images.githubusercontent.com/79353291/168520717-c298cd21-c715-414e-95ea-cab2f384cf7b.png)
* We can see that the top left graph is the MSE on train vs test, top right is MAE train vs test, bottom left is R2 on train vs test, and bottom right is cross validation MAE.
* Models that are overfitting are all of our tree based algorithms which are decsion tree, random forest, and xgboost
* We can see how low the MAE is on the training set vs test set and also cross validation of those model is much higher than predicting on train set
### Hyperparameter Tuning
* We use gridsearch on knn, ridge, lasso, and decision tree
* We use randomized gridsearch on random forest, svm, and xgboost
* We only predict on the test set this time and also perform cross validation on each tuned model and compare the cross validation of pre tune and post tune models
* ![output](https://user-images.githubusercontent.com/79353291/168521270-9dc17dff-6fa4-4d32-8050-964145bfeaa9.png)
* We can see all of our models except knn had improvements after tuning
#### Voting regressor 
* In order to further tune our model, we can use an ensemble method were we can mix our top performing tuned models which are random forest, svm, and xgboost
*  Fine tune the voting regressor using gridsearch
*  Best parameters are weight of 1 to random forest and svm, and weight of 5 to xgboost
*  We were able to get the best model with the lowest cross validation MAE using this model
* ![output](https://user-images.githubusercontent.com/79353291/168521662-57a51635-0e61-4c08-ab3b-2c83bd66542a.png)
###### Best model
* Voting regressor with the cross validation score of 2.89
