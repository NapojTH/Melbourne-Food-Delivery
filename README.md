# Melbourne-Food-Delivery project (This project is a part of FIT5196 Data Wrangling unit)
## Summary

This assignment consists of data cleansing and exploratory data analysis on the Melbourne food delivery datasets including dirty dataset, missing-value
dataset and the dataset consisted outlier in delivery charge.

(for more detail of procedure please look through the jupyter notebook file)


Here is the summary of this project result :

### Dirty dataset 
Severals detection approachs for uncleaned data such as identifying unique in value, comparison of the correctness between dataset, solving linear equation with numpy
packages, using pandas to identify error in data pattern between columns and using graphs (networkx packages) to calculate delivery distance. The following belows is all the errors found within the dataset:

1. Carrier_vehicle column got some wrong spelling name (the first letter should be capitalised) data, which leads to 5 unique value (the correct unique value for the column are 3 values). 
2. Some value of customer_lat and customer_lon column were switched
3. Date column got a variety of format (the correct format is Year-Month-Date)
4. Some data within Is_peaktime column did not match the appropriate time( 0 on the peak time(12:00-13:59:59 and 18:00-19:59:59) or 1 on the non peak time(neither 12:00-13:59:59 nor 18:00-19:59:59))
5. Some data within Is_weekend column did not match the approapriate date
6. After applying the vehicle speed (Bike = 12 kilometers/hours, Car = 25 kilometers/hours, and Motorbike = 30 kilometers/hour) of each vehcle to calculate the delivery time, there were some errors in delivery time column.
7. Once the each items prices in shopping_cart were caluculated, it seems that there were errors between the coupon_discount column and order_price column

All of the following errors are fixed with the data manipulation of pandas and netowrkx graph/node calculation between customer node and restaurant node to calculate shortest distance.

#### Improvement:
To improve the following task result, the comparison of multiple dataset must be performed (compare both the error-free column and error column with another dataset). Despite the fact some errors are identified, I did not find some errors which result in some errors in content. For example, we can compare the order_id, customer_lat, and customer_lon column between dirty and missing-value datset to detect some errors within the content.


### Missing-value dataset
On this dataset, the missing values are detected by using the info commands of pandas. All the missing values are found in the following columns: Shortest_distance, Restaurant ratings and Delivery charges column.

These missing values is imputed or replaced by the following procedures:

1. Shortest_distance: The missing value within this column was be replaced by using networkx graph for nodes between restaurant location and customer location calculation
2. Restaurant rating: The NLTK sentimentanalyser was used for getting an average of compund polarity score and apply the rating calculation formula (10 * (avergae polarity score + 0.9623)/ 2)
3. Delivery Charge: Dropping the missing value of the column and creating another dataframe. Then, fitting that dataframe without missing value to the linear regression model.Then, using that model to predict the value and impute the predicted value

#### Improvement: 
No need for improvement

### Outlier dataset
On this dataset, two outlier detection approachs were used for identified and removed outlier on the delivery charges columns as the following:

1. Box-plot on the delivery charges: The value which higher/lower than upper/lower boundary of boxplot is considered outlier and remove
2. Box-plot of residual: Using the linear regression to create a model. Then, subtracting the observed value and predicted value to calculate residual. After that the boxplot method is applied similar to the residual and the same procedual as the first approach was performed

Once these approaches were done, they will be used for fitting in the new linear regression model and compare each model performace based on the r-square value.
Here is the result:

1. Box-plot on delivery charges r-square: 0.774
2. Box-plot on the residual of delivery charge r-square: 0.958

#### Improvement:
I should include more outlier detection approach such as local outlier factor or other approachs on the dataset since the value for this task is multivariate.


