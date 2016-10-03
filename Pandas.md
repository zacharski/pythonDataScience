# Introduction to Pandas

### Estimated Video Length (20-25 minutes, each video 4-5 minutes)  may need more time

#### introduction and motivation
Pandas is a package for organizing data that has different types (strings, Boolean, integers, floats, etc.) into one neat interface. It has a lot of built-in functions to clean, summarise, and manipulate data to develop an exploratory understanding of a given dataset.
Use example where necessary, as this enhances the learning.

* Intro & Motivation: Why Pandas? Pandas based on Numpy
* How to read data from various sources (database, web, csv, etc.)
* Summarizing data from Pandas
* Cleaning data in Pandas

## Intro & Motivation
TBD

## Pandas basics
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
a table or spreadsheet like structure. 

make | mpg | cylinders | HP | 0-60
---- | :---: | :---: | :---: | :---: | :---: |
Fiat | 38 | 4 | 157   | 6.9
Ford F150 | 19 | 6 | 386 | 6.3 |
Mazda 3 | 37 | 4 | 155 |  7.5 |
Ford Escape | 27 | 4 | 245 | 7.1 |
Kia Soul | 31 | 4 | 164 | 8.5 | 

a common way to create a dataframe is to use a python dictionary as follows:

     cars = {'make': ['Fiat 500', 'Ford F-150', 'Mazda 3', 'Ford Escape', 'Kia Soul'],
        'mpg': [38, 19, 37, 27, 31],
        'cylinders': [4, 6, 4, 4, 4],
        'HP': [157, 386, 155, 245, 164],
        '0-60': [6.9, 6.3, 7.5, 7.1, 8.5]}

     df = DataFrame(cars)
     df
     
     0-60 | HP | cylinders | make | mpg
     ------+-----+------------+-----------+------
     6.9  | 157 |      4       | Fiat 500 | 38


The columns are displayed in sorted order. If we want to specify a column order we can do so:

     df2 = DataFrame(cars, columns=['make', 'mpg', 'cylinders', 'HP', '0-60' ])


We can also create a DataFrame from a set of Series objects:

     cars2 = {'make': Series(['Fiat 500', 'Ford F-150', 'Mazda 3', 'Ford Escape', 'Kia Soul']),
        'mpg': Series([38, 19, 37, 27, 31]),
        'cylinders': Series([4, 6, 4, 4, 4]),
        'HP': [157, 386, 155, 245, 164],
        '0-60': Series([6.9, 6.3, 7.5, 7.1, 8.5])}
        
     df2 = DataFrame(cars2)

## reading data from different sources.
### csv file:
we can create a dataframe from a CSV file (comma separated values).

For example, a CSV file representing the car table above would be:

	make,mpg,cylinders,HP,0-60
	Fiat,38,4,157,6.9
	Ford F-150,19,6,386,6.3
	Mazda 3,37,4,155,7.5
	Ford Escape,27,4,245,7.1
	Kia Soul,31,4,164,8.5

In my case, I named the file `mpg.csv` and saved the file in my home directory `/Users/raz/` and I can make a dataframe out of this file by:

     df3 = pd.read_csv('/Users/raz/mpg.csv')

Sometimes csv files don't have column names. For example, we could have a CSV file that looks like:

	Fiat,38,4,157,6.9
	Ford F-150,19,6,386,6.3
	Mazda 3,37,4,155,7.5
	Ford Escape,27,4,245,7.1

In this case we can specify the column names when we create the dataframe:

	df4 = pd.read_csv('/Users/raz/mpg2.csv', names = ['make', 'mpg', 'cylinders', 'hp', '0-60'])

### reading csv file from url
You can also read in CSV data directly from a URL:

	df5 = pd.read_csv( 'https://archive.ics.uci.edu/ml/machine-learning-databases/pima-indians-diabetes/pima-indians-diabetes.data', names = ['timesPregnant', 'glucose', 'bloodPressure', 'skinFold', 'insulin', 'bmi', 'pedigree', 'diabetes'])


There are many other ways of reading in data including from SQL databases, mongoDB, andwebpages. See the Pandas documentation for details.

### missing values

Let's say our data contains some missing values. For example, in our car dataset suppose we don't know how many cylinders a Ford F-150 has. In the CSV file we would represent that as

	Fiat,38,4,157,6.9
	Ford F-150,19,,386,6.3
	Mazda 3,37,4,155,7.5
	Ford Escape,27,4,245,7.1
	Kia Soul,31,4,164,8.5

When we read that data in 

	df4 = pd.read_csv('/Users/raz/mpg2.csv', names = ['make', 'mpg', 'cylinders', 'hp', '0-60'])
	
and look at the results:
make | mpg | cylinders | HP | 0-60
---- | :---: | :---: | :---: | :---: | :---: |
Fiat | 38 | 4 | 157   | 6.9
Ford F150 | 19 | NaN | 386 | 6.3 |
Mazda 3 | 37 | 4 | 155 |  7.5 |
Ford Escape | 27 | 4 | 245 | 7.1 |
Kia Soul | 31 | 4 | 164 | 8.5 | 

we see that Pandas indicates a missing value with NaN (not a number)


## accessing data
by columns



