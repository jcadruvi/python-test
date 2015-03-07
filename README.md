# python-test

We are having an issue with generating a stream of data so that we can use on several algorithms. We have two csv files. The first one is called dates.csv. The second one is called data.csv. We have a date range filter of start date and end date. What we need to do is to bring both csv files into memory. The dates.csv should be changed to an object that has the following structure:

key, start_date, end_date

in the dates.csv

key = line[0] + line[1]
start_date = line[2]
end_date = line[3]

This structure can be a dictionary, numpy array ect.


The data.csv should be changed to an object that has the following structure:

key, date, float1, float2

in the data.csv

key = line[0] + line[2]
date = line[1]
float1 = line[3]
float2 = line[4]

The system will be write very little but read a lot. This means that we can cache the structure of this object in shared memory or file or some other way. The time that it takes to write the structure in shared memory or wherever it is stored is not really counted. Whatever method you choose to cache or store this data must be able to handle several processes trying to read from the data at once. What we are mainly concerned with is the time it takes to read the data from where it is cached or stored and then do a transformation so our algorithm can operate on the data. The transformation needs to be the following:

Using start and end date passed in go through the dates object and find all the keys that have a start date <= the input start date and an end date >= the input end date. In other wards the input start and end date range must be greater than or equal to the keys start and end date range. Once the dates have been parsed use the key values to go through the data object to find all of the date, float1, and float2 values that fall within the input date range. Another transformation object needs to be created that looks like the following:

key1, [[date[0], float1[0], float2[0], date[1], float1[1], float2[1], ect…]],
key2, [[date[0], float1[0], float2[0], date[1], float1[1], float2[1], ect…]],
key3, [[date[0], float1[0], float2[0], date[1], float1[1], float2[1], ect…]]

This will be an array structure. 

We need to be able to create this transformation object in python in about 1 - 2 seconds.  
