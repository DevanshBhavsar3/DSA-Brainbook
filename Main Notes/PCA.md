26-11-2025  16:54

Status:

Tags: [[Machine Learning]] [[Tags/100 Days of ML (CampusX)|100 Days of ML (CampusX)]]

# PCA

### What is Principal Component Analysis?

PCA is an algorithm used to extract data from higher dimensions to lower dimensions without losing the essence of it. It is widely used for visualization and dimensionality reduction.


### What is Variance?

Variance is a statistical method used to calculate the measure of dispersion (How much the data is squeezed or stretched) of the data. So it is proportional to the spread if data. i.e, If the spread of the data is larger the variance will be bigger.

#### $V = \sum_{i = 1}^{n} \frac{(x_i - \bar{x})^2}{n}$

In PCA, you want the variance to be the maximum of the axis you choose, so that the data still holds the distance it originally had.


### How to find best Principal Component?

1. PCA first generates a unit vector, because we just need to find the direction of the new axis.

2. Then it projects the data onto that unit vector with,
#### $a_{proj} = \frac{a . b}{|b|}$

Since the b vector in unit vector, $|b|$ (magnitude) of b will be 1.
#### $a_{proj} = a . b$


3. Now you will find the variance of this projection. Which will be,
#### $V = \frac{\sum_{i = 1}^n(x_{i_{proj}} - \bar{x}_{proj})^2}{n}$

The goal of the PCA is to find unit vector with maximum $V$.


### Covariance

Covariance is a measure of the joint variability of two random variables. i,.e When one increase what will happen to the other.

Essentially it is just like Correlation but it is not bound to -1 to 1.


### Eigen Vectors

Vectors that doesn't change their direction after any linear transformations are called **Eigen Vectors**. The value of that vectors after linear transformations is called **Eigen Values**.
#### $A\vec{v} = \lambda{\vec{v}}$

Where,
$\vec{v}$ is eigen vector,
$\lambda$ is eigen value


### How does PCA work?

1. You perform Mean centering of the data. That is subtract every data point with its mean.
2. Find Covariance Matrix.
3. Find Eigen Values & Eigen Vectors. This will be all the Principal Components of the data.





# References