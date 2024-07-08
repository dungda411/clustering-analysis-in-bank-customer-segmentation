# Clustering Analysis in Bank Customer Segmentation
This is one of my assignments in Master's Degree in Business Analytics. Regarding the tasks, I was asked to carry out a study on behalf of a business analytics consultancy company that had recently signed a contract with a UK bank. The bank’s product development team wished to undertake segmentation analysis to identify trends and patterns in a sample of records collected from a number of their customers. The segments could be later used for the development of segment-specific financial products and promotions.

The data include information on the customers’ gender, age, savings and current account balances, marital status, homeownership and employability. The collected data also contains information on how long they have been customers with the bank, how long they have been in employment as well as their credit risk. The dataset is provided above. As a business analytics expert, I was required to analyse those data and make any necessary modifications to segment the customers into homogenous groups.
--------------------------
## Data pre-processing
### Data cleaning
The dataset was first checked for missing and unexpected values. Overall, this is a clean dataset, with no such value.
### Data modification
![image](https://github.com/dungda411/clustering-analysis-in-bank-customer-segmentation/assets/157843205/5b6d02c9-6f55-4e45-92fc-fbe5b81a581d)

The histogram of current and savings accounts shows that most of the dataset are below 1000 for both. Therefore, current account is grouped into 2 groups, above 1000 and below 1000. The same is done with savings account.
For each categorical features, dummy variables are created based on their unique values. For the remaining numeric features (Months Customer, Months Employed, Age), Min Max Scaler was applied, which stretches all the values into a range from 0 to 1. This ensures that the calculations of distances are in the same range, which is helpful in case of using Euclidean distance.

--------------------------
## Cluster analysis
Two clustering algorithms were implemented in Python, namely ‘ward’ and ‘average’, with distance metric being ‘Euclidean’.
### Ward method
![image](https://github.com/dungda411/clustering-analysis-in-bank-customer-segmentation/assets/157843205/a539581f-b0cc-499f-87a3-219997249cde)

The algorithm automatically suggests two clusters with two colours. However, the number of clusters also can be 3 or 4, depending on deeper analysis.

### Average method
![image](https://github.com/dungda411/clustering-analysis-in-bank-customer-segmentation/assets/157843205/291df0da-79e5-41bf-b1a7-b78dd05f2975)

The average method does the clustering smaller, with high number of clusters suggested.

### Selecting number of clusters
Choosing the number of clusters for each method is based on three rules of an optimal clustering:
- Least number of clusters: to ensure that the model contains least clusters, 5 values from 2 to 6 are tested.
- High similarity within a cluster and low similarity between clusters: this can be analysed by calculating p value of chi-squared test between the predicted cluster and each categorical variable. P value below 0.05 indicates that there is association between two features. The smaller the p value is, the stronger the association gets.

In both algorithms, the cluster feature has very strong associations with gender, marital status and housing, with their p values of chi-squared tests very small. It is also noticeable that in ward method, the higher the number of clusters is, the lower the p values are. In other words, the algorithm does the clustering on these features more detailly.

![image](https://github.com/dungda411/clustering-analysis-in-bank-customer-segmentation/assets/157843205/bfeb8896-a892-4767-9745-bc337e848981)

With ward method, cases 5 and 6 do great in detailed clustering, but I will go with the 3 for simpler model. With average algorithm, case 4 is the most desirable as the p values are quite similar in all cases.

#### Comparison
##### a. Number of points in each cluster
![image](https://github.com/dungda411/clustering-analysis-in-bank-customer-segmentation/assets/157843205/0d279ea8-a39b-4d43-a5d8-deaa6b305f26)

Ward method has a fairer division in terms of number of points of each cluster as average algorithm offers cluster 4 with only 4 cases. However, fair distribution is not always a good sign, it might be because features in the dataset are largely imbalance.


##### b.	Similarity within cluster and dissimilarity between clusters
- Gender

![image](https://github.com/dungda411/clustering-analysis-in-bank-customer-segmentation/assets/157843205/57820f33-3164-45e0-8b4c-8411ecfb8e8b)

Gender is a good separator in terms of high similarity within clyster, which is also proven in chi squared test in Figure 5.6. With W3 algorithm, almost all females are in cluster 1, and clusters 2 and 3 consist of only men. The same is also seen in A4, most cluster 1 includes women and the rests contain all men. However, it has low dissimilarity between clusters.


- Marital Status

![image](https://github.com/dungda411/clustering-analysis-in-bank-customer-segmentation/assets/157843205/27872169-e8c3-4cac-8ee7-576ae600417f)

Regarding marital status, both have same cluster including only divorced customer, while their rest clusters do not so different from each other.


- Current Account

![image](https://github.com/dungda411/clustering-analysis-in-bank-customer-segmentation/assets/157843205/fc13915b-50d3-414e-9cf2-11a70f9c470a)

Number of customers owning current account more 1000 is small compared to those with account less than 1000. It seems that the average algorithm is more effective than ward. With average method, customers within a cluster are more similar, cluster 2, 3, 4 for instance, and the dissimilarity between groups is also clear. While those are not the case for ward method.


- Savings Account

![image](https://github.com/dungda411/clustering-analysis-in-bank-customer-segmentation/assets/157843205/38845f16-46ef-4a8e-99d4-3e611e9ad325)

Regarding savings account, ward method is slightly better, which is clearly seen in its clusters 2 and 3.


- Months Employed

![image](https://github.com/dungda411/clustering-analysis-in-bank-customer-segmentation/assets/157843205/faaa036e-00a4-4b40-a8da-857163320d50)

In terms of months employed of customers, the differences are clearer in average algorithm. However, both do not offer good separation as the similarity within a group is ambiguous.

#### Conclusion
From the comparison, cluster characteristics from each algorithm can be drawn as follow. All clusters in each method are mutually exclusive. The only difference between the two is that A4 does clustering on another feature, which is current account. However, looking at the trade-off between its detail and fair division, the average method is less desirable than ward method.
![image](https://github.com/dungda411/clustering-analysis-in-bank-customer-segmentation/assets/157843205/3dddcaf7-49e1-4525-b58e-1fbb4e55a8ce)


