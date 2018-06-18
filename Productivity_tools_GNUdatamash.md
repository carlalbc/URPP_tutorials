# Productivity Tools
## Section II: GNU Datamash Tutorial, July 2018

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


Open the terminal and in the command-line create data with 10 values using _seq 10_, pipe the result into datamash and sum the values:

```
seq 10 | datamash sum 1
```

