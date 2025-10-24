11-10-2025  14:47

Status:

Tags: [[Machine Learning]] [[Tags/100 Days of ML (CampusX)|100 Days of ML (CampusX)]]

# Day 10 - Tensors

### What is a Tensor?

Tensors is a data structure used in machine learning and deep learning to store numbers.
Vectors and Matrix can also be called Tensors.


### 0D Tensor / Scalar

0-Dimension Tensors are just scalar values with 0 dimension.

```python
a = np.array(4)
a.ndim
```

Result:
```
0
```


### 1D Tensor / Vectors

1-Dimension Tensor are vectors or a array. It is collection of 0D Tensors or Scalars.

```python
a = np.array([1, 2, 3, 4])
a.ndim
```

Result:
```
1
```

Example,

1D Tensor / Vector can be a single row of the input data with dimension 1. But the dimensions of the vector will be the no. of features in that row.

![[Pasted image 20251011154546.png]]


### 2D Tensor / Matrix

2-Dimension Tensors are vector of vectors or a matrix. It is the collection of 1D Tensors.

```python
a = np.array([
	[1, 2, 3],
	[4, 5, 6],
	[7, 8, 9]
])

a.ndim
```

Result:
```
2
```

Example,

In most of the machine learning, the input data is structured as a 2D Tensor / Matrix, with rows as a vector.

![[Pasted image 20251011154950.png]]


### ND Tensors

You can further group the 2D tensors to create 3D tensors. Group 3D tensors to make 4D tensors and so on...

More importantly you just create a new axis with the smaller dimension structure or make a collection of them to get the next dimension.

![[Pasted image 20251011151519.png]]


### Rank, Axes and Shape

The Rank of the tensor and total axes of a tensor are same. In case of 3x3 matrix (2D Tensor), the rank of the tensor will be 2 and so will be the axes.

The shape of the tensor tell how many row or columns are there.

The size of the tensors tell how many elements can be fitted into it, it is just a multiplication of the shape.

Examples,
```python
a = np.array([
	[1, 2, 3],
	[4, 5, 6]
])

print(a.shape)
print(a.size)
```

```
(2, 3)
6
```

```python
b = np.array([1, 2, 3, 4, 5])

print(b.shape)
print(b.size)
```

```
(5,)
5
```


### Example of 3D Tensor

If you collect time-series data of a stock throughout out a year and you have 10 such analysis of the same stock. It can be represented as shown below,

![[Pasted image 20251011160951.png]]


### Example of 4D Tensor

Collection of Image based data is often represented in 4D Tensor, where each image has 3 channels of Red, Green and Blue, each of them is a matrix.

![[a-brief-survey-of-tensors-5-638.webp]]


### Example of 5D Tensor

Collection of Videos can be represented in 5D Tensor because, they are just collection of images (4D Tensor), where each image is a 3D Tensor with RGB channels (2D Tensor).

![[Pasted image 20251011162931.png]]





# References