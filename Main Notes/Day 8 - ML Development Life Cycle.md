04-10-2025  18:46

Status:

Tags: [[Machine Learning]] [[Tags/100 Days of ML (CampusX)|100 Days of ML (CampusX)]]

# Day 8 - ML Development Life Cycle

![[machine_learning_lifecycle.webp]]

### What is Machine Learning Development Life Cycle

It is the standard path to convert machine learning ideas into product, covering all the steps from gathering the data to deployment of the model. Every engineer should follow it for successfully creating a ML product from the idea.


### 1. Frame the Problem

In the first stage of Machine Learning Development Life Cycle you start with framing the problem. You should think about what algorithm to use, should you consider supervised or unsupervised learning, batch learning of online learning, from where you will collect the data, etc.

### 2. Gathering Data

![[Pasted image 20251004190038.png]]

Data can be gathered from various source like CSV files from kaggle, different website's APIs, Databases and Data Warehouses via ETL (Extract, Transform, Load), or sparse clusters.

You should gather sufficient amount of data that is specific to the problem you are solving. And it should be in suitable format for you machine learning model.

### 3. Data Preprocessing

You may have gathered data from third-party, so it may be dirty in the sense that it contains duplicates, missing cells, outliers, etc.

Before giving the data to your model you should consider,
- Removing duplicate rows,
- Handling missing values,
- Handling outliers,
- Scaling the values to specific range. (Standardization)

### 4. Exploratory Data Analysis (EDA)

After processing the data, you look at the data to find hidden relationships yourself to make some choices easy later on. You can take the mean, median, min value, max value, percentiles for each of the column for analysis.

You can also,
- Visualize the data with graphs,
- Perform Univariate, Bivariate or Multivariate analysis,
- Detecting outliers in the data,
- Finding and removing imbalances across the data.

### 5. Feature Engineering and Selection

After performing analysis on the data, you may have notices that certain features can be grouped together to make new powerful features. This is called **Feature Engineering**.

Example,
For predicting house prices give no. of bedrooms and washrooms, you can create a new feature called total rooms that affects the price more than both of them alone.

Also you can remove unnecessary features that don't contribute to the output. This is called **Feature Selection**. This can fasten your model training because the number of columns are less.

Example, 
For the same example, If you are also given another country's GDP, you can ignore that because it doesn't affect the house price.

### 6. Model Training, Evaluation and Selection

After gathering, cleaning and processing the data for the model, you don't know which model can perform better than one another. So, you can train different models on the same data and select the one which performs the best. This is called **Model Selection**.

For selecting the best model you evaluate them with different accuracy measures, like for linear regression you evaluate based on the Mean Squared Error (MSE). This is called **Model Evaluation**.

You can now train the model that you know will perform best among all the others. You can also use Ensemble Learning to combine 2 models and create one powerful model.

### 7. Model Deployment

Now to make the trained model public, you convert the model's code into binary and create an API that can serve user requests.

Now, whenever the user requests to the API, the API can run those model binaries for prediction and give responses to the user.

APIs can be hosted on Heroku, AWS (Amazon Web Service), GCP (Google Cloud Platform).

### 8. Testing

Before rolling out the model to all the users, you perform beta testing or A/B testing. This is to ensure that the model you created is meeting the needs of the user. If the model performs bad, you have to repeat all the steps again to meet the user needs.

### 9. Optimize

At last, you optimize the model serving before opening it to all the user by making backups, load balancing the users, etc.

You also ensure to retrain the model after certain time period to prevent **Model Rotting**. This is to make sure that the model is up to the mark for the latest changes in data.





# References