# Introduction to Pandas

### Estimated Video Length (20-25 minutes, each video 4-5 minutes)  may need more time

#### introduction and motivation
Pandas is a package for organizing data that has different types (strings, Boolean, integers, floats, etc.) into one neat interface. It has a lot of built-in functions to clean, summarise, and manipulate data to develop an exploratory understanding of a given dataset.

## series
####  a 1d array-like object

     from pandas import Series, DataFrame
     import pandas as pd

Let's consider the heights of Japan's Women's Basketball Team at the 2016 Olympics.      
We can create a series in a number of ways.

##### directly from a Python list

    japan = [173, 182, 185, 176, 183, 165, 191, 177, 165, 161, 175, 189]
    athletesHeight = Series(japan)
    
We could also have done

     athletesHeight = Series([173, 182, 185, 176, 183, 165, 191, 177, 165, 161, 175, 189])
     
In either case we can see the value of the Series athletesHeight

     athletesHeight
	0     173
	1     182
	2     185
	3     176
	4     183
	5     165
	6     191
	7     177
	8     165
	9     161
	10    175
	11    189
	dtype: int64

As like arrays you are familiar with, the left number is the index and the right the value. And we can find the value at a particular index by the usual:

     athletesHeight[3]
     176
     

##### specifying indices
Instead of the index 0, 1, 2, 3 ... you can specify your own index values. For example, we can label them 'a'. 'b', "c" ... etc. 

     athletes2 = Series(japan, index = ['a', 'b', 'c', 'd', 'e', 'f', 'g','h', 'i', 'j', 'k', 'l'])
     athletes2
     a    173
     b    182
     c    185
     d    176
     e    183
     f    165
     g    191
     h    177
     i    165
     j    161
     k    175
     l    189
     dtype: int64

Or suppose we want to keep track of the Chinese team members by their jersey numbers:

	jersey = [4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
	newathletes = Series(japan, index=jersey)
	newathletes
	4     173
	5     182
	6     185
	7     176
	8     183
	9     165
	10    191
	11    177
	12    165
	13    161
	14    175
	15    189
	dtype: int64

So the height of the woman wearing jersey number 11 is 177:

	newathletes[11]
	177
	


​


## dataframe


