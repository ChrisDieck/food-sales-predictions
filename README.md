
**Author**: Christopher Dieck

### Business problem:

The business is trying to find out how they can increase sales between the different types of stores and want to know what the important features are that affect their sales.

### Project Goal:

Our goal for this analysis is to identify which features of the dataset are most important in predicting future sales and to build a machine learning model that can predict future sales using those features.


### Data:

- Source: 
    - https://drive.google.com/file/d/1syH81TVrbBsdymLT_jl2JIf6IjPXtSQw/view?usp=sharing
- Original/Up-to-date Source: 
    - https://datahack.analyticsvidhya.com/contest/practice-problem-big-mart-sales-iii/#About

#### **Target:**
- Item Outlet Sales
    -Sales of the product in the particular store
    - Written in 1000's of dollars

#### **Features:**
- **Item Identifier** [Not used in model]
    - Unique ID for an individual item
- **Outlet Identifier** [Not used in model]
    - Unique ID for the individual outlet
- **Outlet Establishment Year** [Not Used in model]
    - The year the outlet was established
- **Item Weight**
    - Weight of product
- **Item Fat Content**	
    - Whether the product is low fat or regular
- **Item Visibility**
    - The percentage of total display area of all products in a store allocated to the particular product
- **Item Type**	
    - The category to which the product belongs
- **Item MRP**
    - Maximum Retail Price (list price) of the product
- **Outlet Size**	
    - The size of the store in terms of ground area covered
- **Outlet Location Type**	
    - The type of area in which the store is located
- **Outlet Type**	
    - Whether the outlet is a grocery store or some sort of supermarket



**Missing Values**
- There were many missing values within the Item Weight and Outlet Size columns. In order to preserve the shape of the skewed data, I imputed the missing values for Item Weight with the median and I imputed the missing values for Outlet Size with the most frequent value(median for categorical data).



## Methods
- The features, Outlet Identifier and Outlet Establishment Year were completely removed from the dataset as they were deemed not suitable for predicting sales. Item Identifier was only removed for machine learning preprocessing because it is not useful for predicting values, but it is useful to identify the best selling items in data exploration.
    - Outlet Size and Outlet Location Type were ordinal encoded
    - The rest of the categorical data was converted to numerical values and the numerical data was scaled for the linear regression model

- Two Different machine learning models were used to see which model best predicts future sales:
    - Linear Regression
    - Random Forest
- Both models were evaluating using R-squared scores and RMSE scores to identify the amount of error.
- There were several aspects of the dataset that potentially made it difficult to produce a model that could reach an R-squared score above 60%.
    - A correlational heatmap showed that only one feature had a moderate correlation with sales while the rest were fairly weak.
    - The dataset provided was relatively small with roughly 8,500 entries and very few relavent features

## Results

### Linear Regression R-Squared Scores
<img src=https://github.com/ChrisDieck/food-sales-predictions/blob/main/lin_reg_R2.png>

### Linear Regression RMSE
<img src=https://github.com/ChrisDieck/food-sales-predictions/blob/main/lin_reg_RMSE.png>

- As shown, the linear regression model performed terribly with an R2 score of only 57% and an RMSE of $1,094. This means that only 57% of the variances can be accounted for with this model and the model has numerous large errors within it. 

### Random Forest R-Squared Scores
<img src=https://github.com/ChrisDieck/food-sales-predictions/blob/main/random%20forest%20R2.png>

### Random Forest RMSE
<img src=https://github.com/ChrisDieck/food-sales-predictions/blob/main/random%20forest%20RMSE.png>

- When compared to the linear regression model, the Random forest performed about 3-4% better for the R2 score and a lower RMSE of $1,046. With that said, these results show that this model is still not very useful for legitimate sales predictions, which could be caused by the aspects mentioned in the "Methods" section above.

## Most Useful Data Visualizations
### Correlational Heatmap
<img src=https://github.com/ChrisDieck/food-sales-predictions/blob/main/Heatmap%20image.png>

- This heatmap shows that the two variables with the stronget correlations to item outlet sales are Item MRP (moderate) and item visibility (weak, but our second strongest correlation). The rest of the variables, unfortunately, have extremely weak correlations to sales.

### Scatterplot of Item MRP and Sales
<img src=https://github.com/ChrisDieck/food-sales-predictions/blob/main/Item%20MRP%20and%20Sales.png>

- This scatterplot shows a clear and steady increase of sales as the material requirements planning increases for items. This is our best indicator for making sales predictions compared to the rest of our variables.

### Scatterplot of Item Visibility and Sales
<img src=https://github.com/ChrisDieck/food-sales-predictions/blob/main/Item%20Visibility%20and%20Sales.png>

- This scatterplot shows us that there is a sudden drop-off of sales after visibility reaches about 0.18%.
This trend in the data seems counter-intuitive to what one might expect, and may be worth looking further into.
Also, with this variable having the second highest correlation with sales, it should be our second best variable for predicting future sales.

### Boxplot of Outlet Types and Sales
<img src=https://github.com/ChrisDieck/food-sales-predictions/blob/main/Distribution%20of%20Sales%20Based%20on%20Outlet%20Types.png>

- This distribution shows that Type 3 supermarkets have the highest median sales at $3,365 and the highest spread, while grocery stores have the lowest median sales at $257 with the lowest spread. Type 1 and Type 2 supermarkets are fairly similar.
    - Note: There also appears to be many outliers in this data.

## Recommendations:
- Using the random forest model, the company can make predictions on future sales in each of their stores.
- Using this information, the company can make changes to increase sales such as opening more of the high selling outlet types.
- Additionally, it is highly recommended to do further research as to why sales significantly decrease after item visibility reaches about 0.18%.


## Limitations & Next Steps
The biggest limitations with this project was having such a limited dataset and features with low correlational values. Both of these most likely contributed to the low scores for the models. The next step should be to pull more types of information to have more data that could, in hopes, relate more towards outlet sales.

### For further information

For any additional questions, please contact christopherjdieck@gmail.com
