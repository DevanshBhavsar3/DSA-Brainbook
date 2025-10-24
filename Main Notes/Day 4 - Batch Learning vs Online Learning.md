30-09-2025  17:47

Status:

Tags: [[Machine Learning]] [[Tags/100 Days of ML (CampusX)|100 Days of ML (CampusX)]]

# Day 4 - Batch Learning vs Online Learning

### Batch Learning (Offline Learning)

![[Pasted image 20250930191154.png]]

In the batch learning system, the model is first trained and pushed to production server. Now whenever you need to update the model you again need to fetch the model, train it again and deploy to production.

This required a lot of computing resource & time because the model is trained on **all** the available data before deploying. You need to train the model from the scratch whenever you want to update it.

Because batch learning is time consuming it is often done on weekly or monthly bases. But if your problem requires a more fast and efficient model that update with new data you need to train the model on the new data quickly.

#### Disadvantages:

**Lots of data**

The model needs to train on the full data from the scratch, not just the new data. If the data is very large then this can be impossible to implement.

**Hardware Limitation**

Not every hardware is capable of training the model on very large amount of data. You might need to spend a lot for buying the computing power at a large scale.

**Availability**

Lastly, what if the system where your model run doesn't have very stable internet connection. The system can be a smart phone or a mars rover, where the availability is often low.



### Online Learning

![[Pasted image 20250930190757.jpg]]

In the Online learning systems, your model is trained incrementally with the new data it receives while in production. 

Initially the model is trained on the available data and then deployed to the production, now whenever there is new data generated called **mini batch**, the model trains itself while serving to the user queries simultaneously.

#### Advantages:

**Concept drift**

Machine learning systems where the model need to consider latest changes relatively quickly, online learning outperforms batch learning.
Example., Stock market changes.

**Cost effective**

Because the model is trained on the new data which is small compared to the entire dataset combined. The cost to train and run the model is less compared to batch learning systems.

**Faster solution**

It is faster than batch learning because the data batches are smaller resulting in faster training time.

#### How to implement??

https://github.com/online-ml/river
https://github.com/VowpalWabbit/vowpal_wabbit

#### Online Learning Rate

Online learning rate refers to the parameter that decided how fast or slow should the machine learning system adapt to the new data.

If your machine learning system learns very quickly, it may forgot the old data. And oppositely, if the learning rate is very slow then the system will consider the new data very less, but it will also help in ignoring the outliers or noisy data.

#### Out-of-core Learning

When you have very large amount of data that can't be trained on a single system, you can divide those data into small and trainable batches. This batches then can be used train the model using online learning. This is called **Out-of-core Learning**.

This all happens offline, so to make it less confusing you can also name online learning **Incremental Learning**.

#### Disadvantages

**Tricky to use**

Online learning can be very efficient and useful for large enterprise companies, but it is very tricky to implement at production level. If the data is not very large and concept drift is very low batch learning is often considered more.

**Risky**

Because the system is learning from the new data without any monitoring, the model can become unstable or biased towards more common data. You should have some kind of backups or safety while using online learning systems in production.



### Summary

![[Pasted image 20250930190443.png]]





# References