![house-sale-1200xx1200](https://user-images.githubusercontent.com/102948566/178131259-b3957525-9944-4150-9609-30812c8d3ab0.jpg)

# Ames Housing Price Prediction

We are a team of property agents, who aims to help give better recommandation to our customers with the help of machine learning. There are incentive in the housing market for people to profit from asymmetric information by under/over-quoting buyers/sellers. 
By adopting a data driven approach to housing prices, we can help customers have better idea of the prices of their houses, or houses they are looking to buy. 

With the opening of borders and the reintroduction of inter-state travel, there is a greater need for our advise. We not only forecast predicted house values, but also important areas of improvement that homeowners 
can undertake to boost their prospects of obtaining a higher price when they are looking to sell their houses.


## Background

Americans are concerned about the purchasing and selling of homes since properties are generally expensive, and relocating for business or personal reasons is typical in countries as vast as the United States.
Immigrants and emigrants in Ames, Iowa, are no exception. People are concern with buying and selling of houses at a fair price, but the current market which hold high assymmetric information makes it hard to do so.
## Research
1) Floor-to-lot ratio is ratio of your house total circumference divided by the total square feet of your lot, and it is usually considered when pricing a house. (https://www.investopedia.com/terms/f/floor-area-ratio.asp)

2) lot frontage means the horizontal distance between the side lot lines measured along the front lot line but where the front lot line is not a straight line, or where the side lot lines are not parallel.
   (https://www.gimme-shelter.com/frontage-50043/) 

3) When determining the market worth of your property, size is a key factor to consider, as a larger home can increase its value. The price per square foot of a home is calculated by dividing the sales price by the
   square footage of the home. Let's say a house with 2,000 square feet sells for 200,000 dollar. It would cost 100 dollar per square foot. 
(https://www.opendoor.com/w/blog/factors-that-influence-home-value#:~:text=When%20estimating%20your%20home's%20market,foot%20house%20sold%20for%20%24200%2C000.)

## Data 

| Feature                 | type  | Description                                            |
|---                      |---    |---                                                     |
|df_allcat                | float | dataframe including all categorical data               |   
|df_nocat                 | float | dataframe including all Numerical data                 |
|df_allcat_or             | float | dataframe including all ordinal categorical data       |
|df_allcat_nor            | float | dataframe including all norminal categorical data      |

## EDA Findings

1) Quality of the house has the strongest correlation with Sale Price
2) Suprisingly, the condition of the house is not as strongly correlated to Sale Price as the Quality of the house is. Moreso, it is weakly correlated
3) The external quality is the second strongest correlated features with saleprice

(Refer to presentation for a more comprehensive details on insights)

## EDA Findings

1) Quality of the house has the strongest correlation with Sale Price
2) Suprisingly, the condition of the house is not as strongly correlated to Sale Price as the Quality of the house is. Moreso, it is weakly correlated
3) The external quality is the second strongest correlated features with saleprice

(Refer to presentation for a more comprehensive details on insights)

## Treatment of Missing Value
1) Iterative Imputer (linear regression) for numeric features
2) KNN for categorical features


## Finding of Correlation
1) Spear Man correlation for numeric features
2) Kendall for ordinal categorical features
3) 1 way annova for norminal categorical features
## Model

Linear Regression RSME (cross validation - 10 fold) = -5.0108066630854163e+17
Linear Regression RSME test = -26054.752646329184

Linear regression model is expected to be very bad as one hot ending introduces a lot of collinearity and also, a lot of potention weakly correlated features that hard to hand pick. This score can be significantly improve
with the implimentation of methods like R1/R2 regulation, wrapper methods, and/or backward elimination for feature selection. Skewness can also be further processed with polynomials for better score.

Ridge Regression RSME (cross validation - 10 fold) = -31280.787158659572
Ridge Regression RSME test = -25606.953646229184

Ridge regression model is expected to be better then linear regression as impact of the bad features (for eg, the onesintroduced by one hot encoding) on the test reults are reduced by the lambda
Difference in test and train score shows that the model is slightly underfitted.
Best Model is expectedly lasso regression for the aforementioned reasons. It is therefore, choosen for the test set

Lasso Regression RSME (cross validation - 10 fold) = -31280.787158659572
Lasso Regression RSME test = -25606.953646229184

|Model            | RMSE               | Performance             |
| --------------- | ------------------ | ----------------------- |
|Linear Regression|-26054.752646329184 | Baseline model          |
|Ridge Regression |-25606.953646229184 | Worst Performing Model  |
|Lasso Regression |-25606.953646229184 | Best Performing Model   |


## Kaggle Submission

|model            |RSME score         | 
| --------------- | ----------------- |
|Lasso Regression |-23568.20961       | 

## Conclusion

Lasso regression on train set (-25562.717227000587), is slightly underfitted as compared to the prediction on the test set (-23568.20961).
Underfitting happens when my model is too simplistic, which could be due to a lack of training time, input features, or regularization. When a model is underfitted, it is unable to identify the main trend in the data, 
leading to training errors and poor model performance. A model cannot be used for classification or prediction if it does not generalize adequately to new data. The ability to apply machine learning 
algorithms every day to make predictions and classify data is ultimately due to the generalization of a model to fresh data. My model's underfitting is likely due to high bias and low variance.
## Limitation and Future Works

1) not using more powerful feature selection tools to further strengthen the model (for eg. lasso, wrapper methods, and/or backward elimination)
2) not using more powerful tool to handle skewed variables (for eg, polynomials)
3) not using hyper patametrization to optimally tune the models before running
