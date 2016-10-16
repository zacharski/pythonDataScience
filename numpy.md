# Section 4: Understanding Numerical & Scientific Operations
Estimated Video Length (16-20 minutes, each video 4-5 minutes)

 
In this section, we’ll look at the Numpy & Scipy libraries that are used for numerical and scientific computation. I’ll go over arrays in Numpy and numerical operations on those arrays. We’ll then see how Scipy adds a layer of scientific computation on top of Numpy.
 
Use example where necessary, as this enhances the learning.

* What are Numpy arrays? - Array operations, slicing, selection, iteration, basic math’s
* Polynomial math’s & basic statistics in Numpy
* What is Scipy? Matrix & Linear Algebra operations in Scipy
* Optimization and Root finding in Scipy

## Numpy 
## creating ndarrays - n-dimensional arrays.

a single dimension

     ages = numpy.array([21, 30, 27, 24, 19])
     ages
     array([21, 30, 27, 24, 19])
     
unlike Python arrays numpy array elements need to be of the same type. You can check the type of the array by using `dtype`

	ages.dtype
	dtype('int64')
	
multidimensional arrays:

     ratings = numpy.array([[1, 2, 3], [4, 5, 6], [7,8,9]])
     	ratings
     	array([[1, 2, 3],
               [4, 5, 6],
               [7, 8, 9]])
	
### selection
2 ways:

	ratings[1][0]
	4
	ratings[1, 0]
	4
	

### slicing

	ages
	array([21, 30, 27, 24, 19])
	ages[1:3]
	array([30, 27])
	
	ratings[1:]
	array([[4, 5, 6],
           [7, 8, 9]])
## vectorization
In arrays in most computer languages, you loop over the array. For numpy arrays, you can apply the same function to all elements in a efficient way using `vectorization`  or ufunc - universal functions. Here are some examples

	ages
 	array([21, 30, 27, 24, 19])
 	numpy.sqrt(ages)
 	array([ 4.58257569,  5.47722558,  5.19615242,  4.89897949,  4.35889894])

	memory = ([[2, 4, 8], [16, 32, 64]])
	numpy.log2(memory)
	array([[ 1.,  2.,  3.],
           [ 4.,  5.,  6.]])
           
A *ufunc* that is called on a single array is called a *unary ufunc* One that operates on 2 arrays is called a *binary ufunc*

	ones = numpy.array([[1, 1, 1],[1,1,1]])
	numpy.add(memory, ones)
	array([[ 3,  5,  9],
       [17, 33, 65]])

### iteration
if you need to iterate -works same as Python

	for row in memory:
         print(row)
         
	[2 4 8]
	[16 32 64]
	
or

	for row in memory:
 	   print(sum(row))
 	14
	112

