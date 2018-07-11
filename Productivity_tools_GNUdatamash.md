# Productivity Tools - Section II :clock9:
## GNU Datamash Tutorial, July 2018

GNU datamash is a command-line program which performs basic numeric, textual and statistical operations (sum, min, max, stdev, etc.) on input text files.


## Installing GNU datamash

- **Debian (package):**

sudo apt-get install datamash

- **Ubuntu (package):**

sudo apt install datamash

- **Mac OS X using HomeBrew (package):**

brew install datamash

- **Bioconda install:**

conda install datamash


- For other systems check [here](https://www.gnu.org/software/datamash/download/).

## Datamash functions

Sum values, calculate their mean, median, standard deviation and more by simply using the following command:

```
datamash [FUNCTION] [FIELD]
```

See all the possible functions by writing in the command line:

- datamash --help (brief overview)

- man datamash (extended manual)


## Examples  :octocat::speech_balloon:


Open the terminal and in the command-line print numbers from 1 to 10 using **_seq 10_**, then send the result into datamash using pipe (|) and sum the values from the first and only field, then calculate the mean. 

Last, make another sequence with positive and negative values and determine the min and max value of the list.

 
```
#Sum values from the sequence 1..10 
seq 10 | datamash sum 1  

#Sum values from the sequence 1..10 and calculate the mean 
seq 10 | datamash sum 1 mean 1 

#Minimum value of the sequence -5..5 in increments of 1  
seq -5 1 5 | datamash min 1

#Maximum value of the sequence -5..5 in increments of 1
seq -5 1 5 | datamash max 1

```
Easy! :octocat:

Now that we know how to call it let's do some exercises.

## Exercises Part I: Iris dataset

**NOTE:** It is important to have the latest version of Datamash (1.3)

1) Download the classic Iris flower data set (A.K.A Fisher's Iris data set), the filename is **iris.csv** file (hint: use wget)
2) Inspect the file using head and determine how many lines and fields it has (hint: you can use datamash check) 
3) What species of Iris has on average the longest petals? (hint: the column for petals is the 3rd field)
4) Which species has more variability in petals size? What about sepals?

You can do a lot of things! :octocat:

For example, if you want to operate in all columns instead of each one independently, you could combine awk with datamash like it follows:

cols=$( awk '{print NF; exit}' foo); cat foo | datamash -t\  sum 1-$cols


## Exercises Part II: Genes

There are many ways of transforming data to analyze it. Using *datamash* it is possible to quickly process data and use it as input into for a Python script performing more sophisticated analyses and/or directly plotting it.








