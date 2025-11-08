29-10-2025  19:42

Status:

Tags: [[Machine Learning]] [[Tags/100 Days of ML (CampusX)|100 Days of ML (CampusX)]]

# Feature Engineering

### Context

![[Pasted image 20251029195251.png]]

### What is Feature Engineering?

Feature Engineering is a process of using domain knowledge to extract features from raw data. These features can be used to improve the performance of machine learning algorithms.

### Feature Transformation
#### Missing Value Imputation

![[Pasted image 20251029200439.png]]

The first step in the entire feature engineering pipeline is to handle missing values in the data. You might be using Scikit-Learn to train the model, which does not accept missing value in the data.

So first you need to handle it by,
- Removing all rows which have missing values if the number of missing data is less,
- Changing the null values to mean or median of the data,
- Changing categorical null values to the most occuring values. 


#### Handling Categorical Features

There are 2 types of categorical data,
- Nominal Data
	Nominal data is a type of qualitative, categorical data used to label variables without any inherent order or numerical value.
	
	Example, States of a country, name of students, etc.
	
- Ordinal Data
	Ordinal data is a type of categorical data where the values have a natural, meaningful order or rank, but the exact distance between the categories is not known or equal.
	
	Example, Education level, military ranks, etc.

The ML model can not interpret this categorical values as good as numerical values. So you probably need to convert them to numbers. There is various ways you can handle categorical features like,
1. Ordinal Encoding,
2. Label Encoding,
3. One Hot Encoding,
4. Target Encoding,
5. Frequency Encoding,


#### Outlier Detection

Outlier refers to the value which are very far from the normal data range. 

Example, If person's age is ranging from 1-20 in some data and some person have 102 years of age. It is called outlier.

It is important to handle outliers in the data so that the algorithm performs well on the normal data.

![[Pasted image 20251029202846.png]]


#### Feature Scaling

Feature Scaling is a technique to standardize the independent features present in the data in a fixed range.

![[feature-scaling-techniques-1.webp]]

##### Why it is important?

It is important to scale all the feature to some defined range, because if your algorithm uses some distance formula like KNN, the larger scaled value can dominate the algorithm more than the smaller ones. Normally, the data is scaled between -1 to 1.

There are again various ways for feature scaling like,
- Normalization,
	- Min-Max Scaling,
	- Mean Absolute Scaling.
- Standardization.

##### Normalization

Normalization is a technique often applied as a part of data preparation for Machine Learning. The goal of the normalization is to change the values of numeric columns in the dataset to use a common scale, without distorting the differences in the ranges of values or losing information.

##### When to use Standardization?

![[Pasted image 20251030201630.png]]


### Feature Construction

Feature Construction is taking few features from the data, combining them and creating more important features. It requires a domain-level knowledge and can improve the performance of the model drastically.

Example,
In the titanic dataset shown below, you can combine SibSp and Parch columns to create a family column which can be further classifies into small, medium and large families.

![[Pasted image 20251030183050.png]]



### Feature Selection

You don't need to feed all the feature columns to the ML model but only the important ones. The process of selecting important features is called **Feature Selection**. There are various ways for feature selection like,
- Backward Selection
- Forward Elimination

Example,
In the MNIST dataset each of the image is just a lot of feature columns (28x28) containing the color strength in each of the pixel. You can remove the feature columns that is around the digits, which are useless and improve speed and performance of the model. 

![[Pasted image 20251030183605.png]]



### Feature Extraction

Feature Extraction is where you take already present high-dimensional features and convert them to low-dimensions without losing important information.

You can do this by using various algorithms like,
- PCA
- LDA
- tSNE





# References