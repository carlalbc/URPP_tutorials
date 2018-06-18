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


- For other systems check: https://www.gnu.org/software/datamash/download/


## Examples  :octocat::speech_balloon:


Open the terminal and in the command-line print numbers from 1 to 10 using **_seq 10_**, then send the result into datamash using pipe (|) and sum the values from the first and only field, then calculate the mean:

 
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
Easy! :+1:








