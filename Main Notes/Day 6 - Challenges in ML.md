02-10-2025  17:06

Status:

Tags: [[Machine Learning]] [[Tags/100 Days of ML (CampusX)|100 Days of ML (CampusX)]]

# Day 6 - Challenges in ML

### Data Collection

The biggest challenge in machine learning is to find relevant data according to the problem you are solving. Most companies have small to medium level of data which can be insufficient for a more complex problem.

While learning you can easily get data from an external API or via web scraping, but getting it at very large scale and for a specific problem requires a lot of time and effort.

### Insufficient Data / Labelled Data

Suppose you train one ML model with very less amount of data and another model with lots of data. Which one do you think will perform better?

Obviously, the model with more amount of data will perform better. So it shows that the size of data matters. If you have less data you can't train an effective model.

Similarly, finding labelled data is challenging. You can get lots of data from external sources like web scraping but labeling them still requires man hours.

Example,
When creating a animal classifier you can get all the animal images via web scraping from google, but you still need to label them to train the model.

> An interesting study shows that if you have lots of data, then algorithms doesn't matter. This is known as The Unreasonable Effectiveness of Data. But most of the data is still small and medium sized, so the algorithms are going no where.

### Non Representative Data

Now, you have sufficient data for your ML model, but what if the data is not representing every other possibility.

Suppose, you take a survey from Indians about their thoughts on who will win the cricket match. This survey doesn't represent the entirety of possibilities because Indians will be biased towards India winning the match. This is called **Sampling Bias**.

Instead you should have surveyed people from different nationalities to get the data that is representative of different countries but not biased towards India.

### Poor Quality Data

If your data have lots of outliers, noise and empty cells, then ML system might find it harder to learn the hidden pattern in those data.

Before giving data to the ML system you should handle outliers, clean up empty cells and transform the data into suitable format for algorithms.

### Irrelevant Features

Your data should not have irrelevant features, because if the model gets garbage, it will spit out garbage. You should remove unnecessary features or create new meaningful features (Feature Engineering) from it.

Example,
If you have data of participant in a marathon with their name, age, weight and nationality and you try to predict if the participant will come in the marathon or not.

You can clearly tell that nationality doesn't quite play a necessary role in the data so you can remove it (Feature selection), while you can also merge age and weight to create a new BMI feature. (Feature extraction)

### Overfitting

![[Pasted image 20251002183044.png]]

Overfitting refers to the trap in which the machine learning system learns the data to well that it can not even predict well for the new unseen data i.e,. don't generalize well.

To avoid this you can,
- remove noise from the data, 
- add new training data, 
- remove some features. 
This is called **Regularization**.

### Underfitting

![[Pasted image 20251002183103.png]]

Opposite of overfitting, underfitting occurs when the model doesn't quite learn from the training data, that means it ignores the underlying patterns and relationship of the data.

To avoid underfitting you can,
- add more parameters to the model,
- feature engineering
- reduce regularization.

### Software Integration

After all, you need the ML system to be usable by the end user and if the model doesn't support to run on the user's software, it is all worthless.

There are so many challenges in running ML model on various operating systems, integrating it with another programming language, using libraries that are not cross-compatible, etc.

### Deployment & Cost

Deploying machine learning models on the cloud or server is very challenging. Although, you can deploy it with some hassle, the cost to run these algorithms on the cloud with large user base is very big.

https://research.google/pubs/pub43146/

Because deploying and managing the cost of these models are very challenging, there is new role called **MLOps** that is emerged in the market.





# References