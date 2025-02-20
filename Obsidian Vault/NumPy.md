#python #AI #MachineLearning #DeepLearning

NumPy is a python library that is extensively used in machine learning, AI and Dl. NumPy is faster and more versatile than lists, it is quite literally the operational backbone of ML, DL and AI. 

# Why use NumPy over lists?

Numpy uses fixed types, when an integer 5 is stored in memory it is represented as (00000101) in binary, you can store numbers in int32, int16, int8 or any other data type by using *np.arrays()*, Lists on the other hand store information about size, reference count, object type and object value along with the element data. Hence, Numpy reads bytes of memory faster than lists because it uses up significantly less storage compared to lists. 

Numpy also doesn't go through type checking when iterating through objects. Numpy also leverages contiguous memory.

![[Pasted image 20250122140956.png#center]]


# Basic Functionality 

Importing numpy as np is a convention, makes code more readable

```python
import numpy as np 
```

## Initializations

```python
a = np.array([1,3,5])

# initializes a = [1,3,5] as a one dimentional array.

b = np.arrange(100)
# initializes b as a one dimentional array from 0 - 99
c = np.linspace(0, 1, 10) # start, end, num-point
# c = [0. 0.11111111 0.22222222 0.33333333 0.44444444 0.55555556 0.66666667 0.77777778 0.88888889 1. ]

d = np.ones((4,4)) 
# d is initialized as a 4x4 matrix of ones. 

e = np.eye(4)
# e = 4x4 identity matrix

f = np.diag(np.array([1, 2, 3, 4]))

#f = [[1 0 0 0
     #[0 2 0 0]
     #[0 0 3 0]
     #[0 0 0 4]]



```

## Contextual Information 


```python
print(arrayname.ndim) # gives dimention of the array 
print(arrayname.shape) # gives shape of the array in (rows,columns) for 1d arrays gives (col, ) the 2nd argument is blank here. 
arrayname.datatype # gives datatype
```

# Arithmetic

All arithmetic operations in numpy are done element wise. When multiplying two arrays each element is multiplied by the subsequent one in the other multiplier array. 

# Linear Algebra

```python
np.matmal(a,b) # matrix multiplication
np.linalg.det(m) # find determinant of m 
np.min(m) # min in a matrix
np.max(m) # max in a matrix
np.sum(m) # sum of all elements in the matrix
np.cross(a,b) # cross product

```

# Embedding Matrices 
You can embed a smaller matrix within a larger matrix in NumPy by slicing the larger matrix and assigning the values of the smaller matrix to that section. Here's an example:

```python
import numpy as np

# Create a larger matrix (5x5) initialized with zeros
large_matrix = np.zeros((5, 5))

# Create a smaller matrix (3x3) with ones
small_matrix = np.ones((3, 3))

# Define the top-left position where the small matrix should be embedded
start_row, start_col = 1, 1  # Embeds at (1,1) in the large matrix

# Embed the smaller matrix
large_matrix[start_row:start_row+small_matrix.shape[0], start_col:start_col+small_matrix.shape[1]] = small_matrix

print(large_matrix)

```

Output: 
```python
[[0. 0. 0. 0. 0.]
 [0. 1. 1. 1. 0.]
 [0. 1. 1. 1. 0.]
 [0. 1. 1. 1. 0.]
 [0. 0. 0. 0. 0.]]

```
