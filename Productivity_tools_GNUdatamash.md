# Productivity Tools - Section II

## GNU Datamash Tutorial, July 2018

GNU datamash is a command-line program which performs basic numeric, textual and statistical operations (sum, min, max, stdev, etc.) on input text files.

## Installing GNU datamash

- **Debian (package):**

sudo apt-get install datamash

- **Ubuntu (package):**

sudo apt install datamash

- **Mac OS X using HomeBrew (package):**

brew install datamash

- For other systems check: https://www.gnu.org/software/datamash/download/

## Examples 


Open the terminal and in the command-line print numbers from 1 to 10 using **seq** 10, then send the result into datamash using pipe (|) and sum the values:

```
seq 10 | datamash sum 1
```

