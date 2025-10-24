01-10-2025  16:07

Status:

Tags: [[Machine Learning]] [[Tags/100 Days of ML (CampusX)|100 Days of ML (CampusX)]]

# Day 5 - Instance-Based vs Model-Based Learning

### Context

You can also differentiate machine learning models based on how they are learning. For an example in the real world, to remember anything you can memorize the thing directly or go deep down to its concepts and how it works.

There are 2 types of ML model based on how they learn:
- Instance-Based Learning
- Model-Based Learning

### Instance-Based Learning

In the Instance-Based Learning the model doesn't do anything with the data. Whenever there is some new query, it finds the similar training data and just return the result of the training data, that is most similar to the new data.

Instance-Based Learning is also called **Lazy Learning**, because your model doesn't do anything at the training.

Example, 
If there is student data with IQ, CGPA and Placement. Now whenever the model is asked to predict for student with high IQ and CGPA, it finds the neighboring students with similar data and predicts if the new student will be placed or not. This is same logic applied in KNN (K-nearest neighbors).

![[Pasted image 20251001165712.png]]


### Model-Based Learning

Unlike instance based learning, model based learning finds the hidden relationships (concepts) between inputs and outputs. It creates a mathematical expression that points each inputs to its specific output.

Most of the machine learning model uses Model-Based learning like Linear Regression, Logistic Regression, etc.

Example,
For the same students data, a model based learning system will create a decision boundary that can be used to classify, if the student will be placed or not.

![[image.NY98C3.png]]


### Difference

![[Pasted image 20251001164617.png]]





# References