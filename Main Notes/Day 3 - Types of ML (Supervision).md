29-09-2025  15:43

Status:

Tags: [[Machine Learning]] [[Tags/100 Days of ML (CampusX)|100 Days of ML (CampusX)]]

# Day 3 - Types of ML (Supervision)

### Context

![[Pasted image 20250929172848.png]]


### Supervised Learning

In the supervised machine learning, you have both the input and output in your dataset. The algorithms tries to find patterns in the given inputs and outputs, and generate a mathematical expression the will predict outputs for future inputs.

Supervised Learning has 2 types:

#### 1. Regression

When the output of your data is numeric, like 
- Given the house size predict its price,
- Given IQ of a student predict how much salary will he/she earn.
is when the problem can be called a **Regression Problem**.

![[Pasted image 20250929161242.png]]

#### 2. Classification

If the output you want the machine to predict is a category, like
- Given the marks of a student will he/she will be able to crack a job,
- Give an email predict if it is a spam or not.
is the the problem stated as **Classification Problem**.

![[Pasted image 20250929161437.png]]


### Unsupervised Learning

In contrast to supervised learning where the dataset contains the output columns, Unsupervised learning algorithms only have input columns.

The algorithms it self derives some similarity between data by pattern recognition. It has few types like,

#### Clustering

In the clustering algorithms, the machine groups the similar data points together creating clusters.
We can then label this clusters for further business purpose.

![[Pasted image 20250929163553.png]]

#### Dimensionality Reduction

The goal of the machine in this algorithm is to simplify the given data without losing the too much information and patterns of the original data.

This can be done by combining the two or more related input columns into single column, which is called **feature extraction**. The output of the algorithms then can be used for visualization.

Example, visualization of complex data with dimensionality reduction
![[Pasted image 20250929164242.png]]

#### Anomaly Detection

In anomaly detection, the machine is trained on normal instance of the data. Now, when there is some abnormal data is found after training, the machine can flag it as anomaly.

This is widely used to prevent fraud, catching manufacturing defects, or automatically removing outliers from a dataset before feeding it to another learning algorithm.

![[Pasted image 20250929164702.png]]

#### Association Rule Learning

The goal of association rule learning is to find hidden relations between different data columns.

Example, Finding the relation between 2 products in the supermarket, so the manager can place them together to increase sales.

Real-world example,
https://tdwi.org/articles/2016/11/15/beer-and-diapers-impossible-correlation.aspx


### Semi-supervised Learning

Semi-supervised Learning is defined by using a small amount of labeled data ( Supervised Learning ) and other unlabeled data ( Unsupervised Learning ).

For an example, the teacher solved 1 sample question and then doesn't solve other similar problems, which can be used in exams or practice.

Real life example, 
Google photos automatically creates groups of photos with similar person in the picture ( Unsupervised ). Then it prompts the user to label the person ( Supervised ) which can be used in future pictures.

As you can notice that the Semi-supervised learning is just the combination of Supervised and Unsupervised learning.


### Reinforcement Learning

Unlike all the other types of machine learning, Reinforcement learning doesn't have any data.
The algorithm called **Agent** tries to learn things from its surrounding environment.

If the agent performs valid actions it get rewards, else there is some penalty so that the agent avoid similar mistakes in the future.

By iterating in the same environment the agent makes up a **Policy**, which defines what should the agent do when it is in a given situation.

![machine-learning Tutorial => Reinforcement Learning](https://i.stack.imgur.com/gWmhs.jpg)

Real life example, 
Google DeepMind made AlphaGo agent with RL which can play go (a chinese game).
https://youtu.be/WXuK6gekU1Y?si=YLim0ZlaBB70DXGK





# References