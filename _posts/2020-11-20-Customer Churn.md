---
title:  "Customer Churn"
category: posts
date: 2020-11-20
header:
  teaser: "images/churn.png"
excerpt: The purpose of this project is to create a model to predict which customers are likely to churn, as well as the causes for the churn.
---

| ![PNG](/images/churn.png)|

Link to full [code](https://github.com/twrobbins/Github-Files-Updated/blob/main/DSC680-Applied%20Data%20Science/Project%203/DSC680-Customer%20Churn-Final.ipynb)


### Abstract
Customer churn refers to the rate at which customers leave a company or service.  Churn could be caused for many different reasons and churn analysis helps to identify the cause and timing of the churn, opening up opportunities to implement effective retention strategies.  A predictive churn model looks at customer activity from the past and checks to see who is active after a certain time and identify the steps and stages when a customer is leaving a service or product.  In this study, I plan to create a predictive churn model to predict which customers are likely to churn, as well as the causes for the churn.

Keywords:  customer churn, customer segmentation, telecommunications, 


### Introduction
Customer churn is the tendency of customers to abandon a brand and stop being a paying client of a particular business.  The percentage of customers that discontinue using a company’s products or services during a particular time period it called customer churn rate.  Churn rate is a health indicator of a busines whose customers are subscribers and paying for services on a recurring basis, such as in the telecommunications industry.  Although some natural churn is inevitable, having a higher churn rate can be a sign that a business is doing something wrong.  

There are many things that companies may do wrong.  For example, if customers aren’t given easy-to-understand information about product usage they may choose to cancel.  In addition, lifetime customers may feel unappreciated because they don’t get as many bonuses as new ones.  In general, it ‘s the overall customer experience that defines brand perception and influences how customers recognize value for money of products and services they use.

Churn rates tend to correlate with a company’s lost revenue and overall growth potential, so keeping churn to a minimum is key.  In addition, customers who have negative experiences with a brand are more likely to share their experiences with other potential customers through review sites or social media.  HubSpot research found that 49% of buyers reported sharing an experience they had with a company on social media.  In a world of eroding trust in business, word of mouth plays a more critical role in the buying process than ever before. 

Underestimating the impact of even a tiny percentage of churn can have a huge impact.  A small rate of monthly/quarterly churn will compound quickly over time.  According to Michael Redbord, general manager of Service Hub at HubSpot, “just 1 percent monthly churn translates to almost 12 percent yearly churn” for a subscription-based business.  Thus, companies with high churn rates can quickly find themselves in a financial hole as they will need to devote more resources to new customer acquisition.  Getting a new customer may cost up to five times more than retaining an existing customer.  


### Methods
#### Datasets
I obtained the test and train datasets for my project from Kaggle.com, which had already been divided into 80% training data and 20% test data (https://www.kaggle.com/mnassrib/telecom-churn-datasets?select=churn-bigml-80.csv, https://www.kaggle.com/mnassrib/telecom-churn-datasets?select=churn-bigml-20.csv).  The observations in the dataset contained phone data for each individual customer.  A description of the fields is provided in the table below:

| ![PNG](/images/cc1_dataset.png)   | 
|:--:| 
| *Figure 1: Dataset Fields* |

The dataset was fairly clean and contained no missing values.  State, area code, and the Boolean variables (including the churn target variable) were converted to factors.

#### EDA
A frequency distribution of the churn target variable indicated that 388 customers churned out of a total of 2,666 customers, reflecting an overall churn rate of 14.6%.  

| ![PNG](/images/cc2_distribution.png)   | 
|:--:| 
| *Figure 2: Distribution of Target Variable* |

Histograms, density plots, boxplots, and frequency distributions (for the categorical variables) were used to analyze each of the variables individually, as well as in combination with other variables.  

| ![PNG](/images/cc3_intl_bar.png)   | 
|:--:| 
| *Figure 3: International Plan Churn - Bar Plot* |

| ![PNG](/images/cc4_intl_prop.png)   | 
|:--:| 
| *Figure 4: International Plan Churn - Proportion* |

| ![PNG](/images/cc5_cs_bar.png)   | 
|:--:| 
| *Figure 5: Customer Service Call Churn - Bar Plot* |

| ![PNG](/images/cc6_cs_prop.png)   | 
|:--:| 
| *Figure 6: Customer Service Call Churn - Proportion* |

| ![PNG](/images/cc7_top_corr.png)   | 
|:--:| 
| *Figure 7: Correlations with Churn* |

| ![PNG](/images/cc8_corr_plot.png)   | 
|:--:| 
| *Figure 8: Correlation Plot* |

Key findings during the EDA phase indicated that churn was much higher for customers who had the international plan and more customer service calls.  It was also found that there were strong correlations between the number of minutes and total charges for each of day, evening, night, and international calls.  This made sense as total charges should be a function of the time spent on calls.  As a result, the number of minutes should be excluded from the model to avoid the problem of multicollinearity.  

### Modeling
Numerous logistic regression models were created in R, based on the initial EDA, correlation analysis and personal experience.  The final model calculated predicted churn based on whether the customer had the international plan and/or the voicemail plan, the number of international and customer service calls, and each of the charges for day, evening, night, and international calls.  Model parameters and statistics are shown below:

| ![PNG](/images/cc9_model_param.png)   | 
|:--:| 
| *Figure 9: Model Parameters* |

The churn variable was converted from Boolean to a numeric value of 0 (False) or 1 (True), and a confusion matrix was created to analyze the results on the training dataset.  Based on the high accuracy, precision, and recall from the training dataset, the model was then fit on the test dataset.

### Results

The confusion matrix and statistics for the test set were in line with the training set as shown below:
| ![PNG](/images/cc10_cm.png)   | 
|:--:| 
| *Figure 10: Confusion Matrix* |

| ![PNG](/images/cc11_metrics.png)   | 
|:--:| 
| *Figure 11: Metrics* |
 
The confusion matrix for the test set indicates strong values for accuracy, precision, and recall, as with the training set.  However, when analyzed more closely, it appears that the model was not as good at predicting true positives.  In this case, that would mean that the model did not correctly predict that a customer would churn when they, in fact, did.  This could indicate that the dataset used for this study may not have included all of the factors affecting customer churn.  For example, the customer may have found a better deal with another provider and cancelled without making any customer service calls.  This would be difficult to detect based on the dataset for this model, without being able to compare the fees charged by the company in question with what other providers are charging.  

In addition, the most predictive variables for the final model were arranged in order of importance as shown below:

| ![PNG](/images/cc12_feature.png)   | 
|:--:| 
| *Figure 12: Feature Importance* |
 
Based on these results, the client may want to further explore why customers with international plans are canceling and consider offering additional services.  In addition, efforts should be made to minimize customer service calls, as well as improving the quality of such calls to further engage the customer, especially for customers with higher total day charges. 

| ![PNG](/images/cc13_cs_ip.png)   | 
|:--:| 
| *Figure 13: Churn by Customer Service Calls and International Plan* |

| ![PNG](/images/cc14_dc_ip.png)   | 
|:--:| 
| *Figure 14: Churn by Day Charges and International Plan* |

### Conclusion
This study found that a logistic model can be used to accurately predict overall customer churn, as well as determining the key variables contributing to such churn.  Although the model was good overall at predicting whether a customer would churn or not, additional efforts could be made to focus on customers that were not expected to churn, but actually did, as the unexpected loss of customers can have significant impact on company revenue and growth.  Datasets incorporating more features relating to churn could also be incorporated.  

The key fields leading to churn were identified for possible corrective action.  Although such fields were identified, further analysis could be done to get to the true source of the problem (such as why customers with the international plan have a higher churn rate), so additional retention efforts can be made.


### References

1. Anderson, R. (2019, December 23). Stock Price Prediction Using Python & Machine Learning. Retrieved from Medium: https://medium.com/@randerson112358/stock-price-prediction-using-python-machine-learning
2. Banushev, B. (2019, January 14). Using the latest advancements in AI to predict stock market movements. Retrieved from Python Awesome: https://pythonawesome.com/using-the-latest-advancements-in-ai-to-predict-stock-market-movements/
3. Ganegedara, T. (2020, January 1). Stock Market Predictions with LSTM in Python. Retrieved from Data Camp: https://www.datacamp.com/community/tutorials/lstm-python-stock-market
4. Koehrsen, W. (2018, January 19). Stock Prediction in Python. Retrieved from Towards Data Science: https://towardsdatascience.com/stock-prediction-in-python
5. Kohorst, L. (2018, November 9). Predicting Stock Prices with Python. Retrieved from Towards Data Science: https://towardsdatascience.com/predicting-stock-prices-with-python
6. Migdon, H. (2020, September 2). How To Use the Alpha Vantage API with Python to Create a Stock Market Prediction App. Retrieved from Last Call - The RapidAPI Blog: https://rapidapi.com/blog/stock-market-prediction-python-api/
7. Müller, F. (2020, March 24). Stock market prediction: a time series forecasting problem. Retrieved from Relataly: https://www.relataly.com/stock-market-prediction-using-a-recurrent-neural-network
8. Nayak, A. (2019, March 18). Predicting Stock Price with LSTM. Retrieved from Towards Data Science: https://towardsdatascience.com/predicting-stock-price-with-lstm
9. Pochetti, F. (2014, September 20). Stock Market Prediction in Python Intro. Retrieved from Francesco Pochetti: http://francescopochetti.com/stock-market-prediction-part-introduction
10. Shamdasani, S. (2017, December 15). Build a Stock Prediction Algorithm. Retrieved from Enlight: https://enlight.nyc/projects/stock-market-prediction
11. Shyam R, V. P. (2020). Stock Prediction Overview and a Simple LSTM based Prediction Model. International Research Journal of Engineering and Technology (IRJET).
