#python #DeepLearning #AI #MachineLearning 

Matplotlib is the most popular library for visualisation with Python. As with NumPy it is generally
imported in a shorthand way (matplotlib.pyplot as plt). Two important aspects of matplotlib are
figures and axes. Figures correspond to a physical figure, while an axes corresponds to regions or
sections of the figure. 

# Basic Setup 

```python 
import matplotlib.pyplot as plt
fig, (ax1, ax2) = plt.subplots(2) # two plots..
fig, (ax1, ax2) = plt.subplots(2, sharex=True, sharey=True) # same as above,␣
                            #but with a shared x and y axis between the two plots
plt.show() # function to show the output

# Here the `fig` object represents the **entire figure**, while `ax1`, `ax2`, and `ax3` are the individual **axes (subplots)** created within that figure.
```
![[c7XGVPhp9q.png#center]]

# Further Examples

```python 
fig, (ax1, ax2, ax3) = plt.subplots(3)
sigma=3
mu = 2
n = sigma * np.random.randn(500,1) + mu
ax1.plot(n)
# add some noise to n for visualisation purposes
mu_noise, sigma_noise = 1, .7
noise = sigma_noise * np.random.randn(500,1) + mu_noise
y = n * noise
ax2.scatter(n, y)
ax3.hist(n)
# annoyingly we sometimes need this to display plots with better spacing
plt.tight_layout()
plt.show()
```
![[C0zk4tMNU0.png#center]]


# Random Variables with [[NumPy]]

```python
n100 = np.random.normal(0,1,100)
plt.hist(n100, bins=10)
plt.show()
```

We can generate random variables using NumPy quite easily. In the following code snippet:
• Line 1 will generate 100 standard normally distributed random numbers and store them in
the variable n100.
• Line 2 plots a histogram with 10 intervals from n100.

![[Pasted image 20250122155740.png#center]]

