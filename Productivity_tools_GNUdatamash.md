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

**NOTE:** It is important to have the latest version of Datamash (1.3) installed.

1) Download the classic Iris flower data set (A.K.A Fisher's Iris data set), the filename is **iris.csv** file.

2) Inspect the **iris.csv** file using *head* and determine how many lines and fields it has (hint: you can use **datamash check**)

3) What species of *Iris* has on average the **longest** petals? (hint: the column for petals is the **3rd field**)

4) Which species has more variability in petals size? What about sepals? (hint: you can use **pvar**)

You can do a lot of things! :octocat:

## Exercises Part II: Genes

Datamash allows you to quickly count how many transcripts per gene there are, which gene has more transcripts, number of exons, etc. 

We will next work with a GTF file, the format is as follows (extracted from Ensembl):

---------------------
- **seqname** - name of the chromosome or scaffold; chromosome names can be given with or without the 'chr' prefix. 
- **source** - name of the program that generated this feature, or the data source (database or project name)
- **feature** - feature type name, e.g. Gene, Variation, Similarity
-  **start** - Start position of the feature, with sequence numbering starting at 1.
-  **end** - End position of the feature, with sequence numbering starting at 1.
-  **score** - A floating point value.
- **strand** - defined as + (forward) or - (reverse).
- **frame** - One of '0', '1' or '2'. '0' indicates that the first base of the feature is the first base of a codon, '1' that the second base is the first base of a codon, and so on..
- **attribute** - A semicolon-separated list of tag-value pairs, providing additional information about each feature.
---------------------

With that in mind let's start practicing! :octocat:

1) Download the transcripts GTF file from Gencode latest version and unzip it (it is in the main folder)

Or download this file but it requires some tinkering before using:
```
wget ftp://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_28/gencode.v28.annotation.gtf.gz
```
2) Count the number of transcripts per gene using **groupby** together with **count** (hint: genes are in column #9 and transcripts in column #10). How many transcripts the gene with the Ensembl ID: **ENSG00000257198.6** has? (hint use **grep**)

3) Can you tell which are the Ensembl IDs for the transcripts of gene **ENSG00000257198.6**? (hint use **collapse**) 


Overall, there are many ways of transforming data to analyze it. Using *datamash* it is possible to quickly process data and use it as input into for other programming languages performing more sophisticated analyses and/or visualization by directly plotting it :octocat:








