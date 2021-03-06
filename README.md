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

## Models:

### For the purpose of pairing customers and products, xGBoost technique was utilized.  

Link to the notebook: https://github.com/SNPranay/Product-Recommendation-System/blob/master/Customer_Pairing.ipynb  

xGBoost is an optimized distributed gradient boosting library designed to be highly efficient, flexible and portable. It implements machine learning algorithms under the Gradient Boosting framework. xGBoost provides a parallel tree boosting (also known as GBDT, GBM) that solve many data science problems in a fast and accurate way. The same code runs on major distributed environment (Hadoop, SGE, MPI) and can solve problems beyond billions of examples. XGBoost stands for eXtreme Gradient Boosting. It is an implementation of gradient boosting machines created by Tianqi Chen,now with contributions from many developers. It belongs to a broader collection of tools under the umbrella of the Distributed Machine Learning Community or DMLC who are also the creators of the popular mxnet deep learning library. The implementation of the algorithm was engineered for efficiency of compute time and memory resources. A design goal was to make the best use of available resources to train the model. Generally, XGBoost is fast. Really fast when compared to other implementations of gradient boosting. Szilard Pafka performed some objective benchmarks comparing the performance of XGBoost to other implementations of gradient boosting and bagged decision trees. He wrote up his results in May 2015 in the blog post titled “Benchmarking Random Forest Implementations“.His results showed that XGBoost was almost always faster than the other benchmarked implementations from R, Python Spark and H2O. From his experiment, he commented: ”I also tried xgboost, a popular library for boosting which is capable to build random forests as well. It is fast, memory efficient and of high accuracy” — Szilard Pafka, Benchmarking Random Forest Implementations. The XGBoost library implements the gradient boosting decision tree algorithm. This algorithm goes by lots of different names such as gradient boosting, multiple additive regression trees, stochastic gradient boosting or gradient boosting machines. Boosting is an ensemble technique where new models are added to correct the errors made by existing models. Models are added sequentially until no further improvements can be made. A popular example is the AdaBoost algorithm that weights data points that are hard to predict. Gradient boosting is an approach where new models are created that predict the residuals or errors of prior models and then added together to make the final prediction. It is called gradient boosting because it uses a gradient descent algorithm to minimize the loss when adding new models. This approach supports both regression and classification predictive modeling problems.  

### Extremely Randomized Trees were for predicting a customer’s needs based on his/her locality.  

Link to the notebook: https://github.com/SNPranay/Product-Recommendation-System/blob/master/Product_Location.ipynb  

In extremely randomized trees, randomness goes one step further in the way splits are computed. As in random forests, a random subset of candidate features is used, but instead of looking for the most discriminative thresholds, thresholds are drawn at random for each candidate feature and the best of these randomly-generated thresholds is picked as the splitting rule. This usually allows to reduce the variance of the model a bit more, at the expense of a slightly greater increase in bias. A decision tree is usually trained by recursively splitting the data. Each split is chosen according to an information criterion which is maximized (or minimized) by one of the “splitters”. These splitter usually take the form of x[i]>t where t is a threshold and x[i] indicates the i-th component of an observation. Decision trees, being prone to overfit, have been transformed to random forests by training many trees over various subsamples of the data (in terms of both observations and predictors used to train them). The main difference between random forests and extra trees (usually called extreme random forests) lies in the fact that, instead of computing the locally optimal feature/split combination (for the random forest), for each feature under consideration, a random value is selected for the split (for the extra trees). This leads to more diversified trees and less splitters to evaluate when training an extremly random forest. The point here is not to be exhaustive.  

### Multi Layer Perceptron Neural Networks were used to identify, or predict a customer’s features based on the products he/she has purchased.  

Link to the notebook: https://github.com/SNPranay/Product-Recommendation-System/blob/master/Characteristics_Product.ipynb  

A multilayer perceptron (MLP) is a class of feedforward artificial neural network. An MLP consists of, at least, three layers of nodes: an input layer, a hidden layer and an output layer. Except for the input nodes, each node is a neuron that uses a nonlinear activation function. MLP utilizes a supervised learning technique called back propagation for training. Its multiple layers and non-linear activation distinguish MLP from a linear perceptron. It can distinguish data that is not linearly separable. Multilayer perceptrons are sometimes colloquially referred to as ”vanilla” neural networks, especially when they have a single hidden layer. If a multilayer perceptron has a linear activation function in all neurons, that is, a linear function that maps the weighted inputs to the output of each neuron, then linear algebra shows that any number of layers can be reduced to a two-layer input-output model. In MLPs some neurons use a nonlinear activation function that was developed to model the frequency of action potentials, or firing, of biological neurons. Learning occurs in the perceptron by changing connection weights after each piece of data is processed, based on the amount of error in the output compared to the expected result. This is an example of supervised learning, and is carried out through backpropagation, a generalization of the least mean squares algorithm in the linear perceptron. The term ”multilayer perceptron” does not refer to a single perceptron that has multiple layers. Rather, it contains many perceptrons that are organized into layers. An alternative is ”multilayer perceptron network”. Moreover, MLP ”perceptrons” are not perceptrons in the strictest possible sense. True perceptrons are formally a special case of artificial neurons that use a threshold activation function such as the Heaviside step function. MLP perceptrons can employ arbitrary activation functions. A true perceptron performs binary classification (either this or that), an MLP neuron is free to either perform classification or regression, depending upon its activation function.  

I’ve used the ReLu activation function over other activation functions that were possible to use while applying MLPclassifier because I was obtaining maximum accuracy when I used ReLu activation function. Accuracy aside, I was getting minimum log-loss when I used ReLu, which indicates that the model was more confident when ReLu was used as compared to when other activation functions were used. Also, ReLu gave results quicker than any other activation function and it can also overcome the issue of ”Vanishing Gradient”. Empirically, I observed that L-BFGS converges faster and with better solutions on small datasets. For relatively large datasets, however, Adam is very robust. It usually converges quickly and gives pretty good performance. Stochastic Gradient Descent (SGD) with momentum or Nesterov’s momentum, on the other hand, can perform better than those two algorithms if learning rate is correctly tuned. I tried changing the learning rate parameter from ”constant” to ”adaptive”, but there was no significant increase in accuracy, thus I set it to the default value, ”constant”. I tweaked the beta1 and beta2 values while keeping them between \[0.9. 1), but even this tuning resulted in no significant contribution towards accuracy. Changing number of Hidden Layer and the size of Hidden Layers also did not affect the accuracy too much.

## Refernces:  

[1] https://jair.org/index.php/jair/article/view/10302  
[2] https://medium.com/erinludertblog/smote-synthetic-minorityover-sampling-technique-caada3df2c0a  
[3] https://xgboost.readthedocs.io/en/latest/  
[4] https://machinelearningmastery.com/gentle-introductionxgboost-applied-machine-learning/  
[5] https://scikit-learn.org/stable/modules/ensemble.html  
[6] https://www.thekerneltrip.com/statistics/random-forest-vsextra-tree  
[7] https://en.wikipedia.org/wiki/Multilayer perceptron  
[8] https://medium.com/usf-msds/choosing-the-right-metricfor-evaluating-machine-learning-models-part-2-86d5649a5428  
