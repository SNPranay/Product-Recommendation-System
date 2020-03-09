# Product-Recommendation-System
This repository contains codes and files that were utilized for developing this Product Recommendation System.

Link to the dataset used: https://www.kaggle.com/c/santander-product-recommendation/data

This data represents 1.5 years of customers' behavior data from Santander Bank. The data starts at 2015-01-28 and has monthly records of products a customer has, such as "credit card", "savings account", etc.

Using this data, 3 objectives were achieved:
1. Pairing Customers with vaarious products of the bank
2. Predicting the bank's product that a customer may need, based on the customer's location
3. Preidct the characteristics or attributes of a customer based on the products of the bank, used by them

The basic thing we are trying to do here is pairing up people customer with Santander’s products to develop a more effective system than Santander’s previous system, which can better meet the individual needs of all customers and ensure their satisfaction no matter where they are in life. Santander has previously tried to do this, but it wasn’t very effective as they have stated. The issue with their previously operating person-to-product matching algorithm was that a small number of Santander’s customers received a large number of
recommendations while the large number of remaining customers rarely saw any recommendations from Santander.

## Data Compresssion:

Link to the notebook: https://github.com/SNPranay/Product-Recommendation-System/blob/master/Data_Compression.ipynb  

The data add up to 15.3 GB of training data. This large volume of data caused my system to crash and thus I had to figure out how to compress the data to use it all, and more importantly, efficiently. Numerical Data which were of data-types ’int64’ or ’float64’,
were converted to ’int32’ or ’float32’ wherever it was possible. This reduced the memory requirements by an exponential factor.
Furthermore, data which were of the type ’object’ were converted to ’categorical’. The reason we did this was, when some variable is of the ’object’ data-type, it is stored in the system as a string, whereas upon converting to ’categorical’ data-type, although the data would still appear as a string, it would actually be stored as binary numbers in the system. As a result of all the techniques thus applied, I successfully compressed data 2.13 GB data, which had a 15.3 GB footprint in Pandas, into 1.89 GB of data, without any loss whatsoever.

## Data Cleaning:

Link to the notebook: https://github.com/SNPranay/Product-Recommendation-System/blob/master/Data_Cleaning.ipynb  

This involved some basic steps like dropping columns having large percentage of null values, and filling up blank cells in a methodological manner.  

There was visible redundancy in the data-set provided to us. Having features like Province Name and Province Code is an instance of redundant features from our data-set. Such columns were dropped to keep only the relevant features and remove redundancy from the data-set. As a result of this, we were successful in scaling down the total number of features to 63.  

The data we had, was very highly biased, when it came to data about the products possessed by the bank’s customer. This biased data resulted in very vague results when various training models were applied on this unprocessed data. Overfitting was the reason for these vague results. To make amends to this biased data, we applied Synthetic Minority Over-Sampling Technique, known as SMOTE.  

