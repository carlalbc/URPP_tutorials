# Overview
  - Alias (command)
  - Installing software from source files (without *root* priviledge) 
  - [GNU Parallel](https://www.gnu.org/software/parallel/parallel_tutorial.html=)
  - Cluster usage (qsub, qstat, etc)

# Alias (command)

An **alias** in computing, is a command in various command line interpreters (shells) such as Unix shells, AmigaDOS, 4DOS/4NT, KolibriOS and Windows PowerShell, which enables a replacement of a word by another string ([source:Wikipedia](https://en.wikipedia.org/wiki/Alias_(command))). You can customize your working environment by modifying your **.bashrc**, for example by adding **aliases**.  

# What is the .bashrc?

[.bashrc](https://unix.stackexchange.com/questions/129143/what-is-the-purpose-of-bashrc-and-how-does-it-work) is a [shell script](https://en.wikipedia.org/wiki/Shell_script) that [Bash](https://www.gnu.org/software/bash/) runs everytime a shell session is initialized. We will learn how to modify it Today.

###  :beginner: Exercise 1.- Customize your working enviroment by adding aliases to your .bashrc


For the purposes of **Today's practical exercises**, we will use [Gedit](https://wiki.gnome.org/Apps/Gedit). However you could use any other editor of your choice, such as [Vim](https://www.vim.org/), [Emacs](https://www.gnu.org/software/emacs/), [Atom](https://atom.io/), [Sublime Text](https://www.sublimetext.com/), among others.

- Open your [.bashrc](https://unix.stackexchange.com/questions/129143/what-is-the-purpose-of-bashrc-and-how-does-it-work) file with the text editor of your choice by:

```sh
$ gedit ~/.bashrc

#My aliases and shortcuts
alias rm='rm -i'                            #Ask before deleting files, can be override with "-f" (force)
alias l="less"                              #Shortens your typing
alias h="head"                              #Shortens your typing
alias ..='cd ..'                            #Shortens your typing
alias subtab="sed 's/\t/\,/g'"              #Change tabular-separated files to comma-separated files
alias subcomma="sed 's/\,/\t/g'"            #Change comma-separated files to tabular-separated files 
alias untar='tar -zxvf'                     #Decompression of files
```


- **Save and exit** from your text editor. In Gedit you can use **Ctrl+S** (to save) and then **Ctrl+Q** (to exit)
- Your new .bashrc configuration **has to be reloaded** to work. You can do that **without** logging in-and-out of the Terminal by running the following command from your current Terminal window:

```sh
$ source ~/.bashrc
```

#### Using your aliases:

As a general rule, first type the command --in this case the new alias, then the file/s you want to modify and if you want to save it, redirect the output with '>'

```sh
[alias] yourfile > newfile                      #example of how it should be
[alias] yourfile | [another alias] > newfile    #you use more than one alias at once with pipes "|" 
```

### :beginner: Exercise 2. Change a comma-separated file to a tab-separated file by using your new alisases

-  **NOTE:** You can save Github files (of moderate size) by doing **right click** with your mouse on the displayed raw data and then using **Save as**. The following link [iris.csv](https://raw.githubusercontent.com/carlalbc/URPP_tutorials/master/Linux_command_line_II/iris.csv) redirects you to the raw data file. 
-  **Save** the previous file in your **current** folder (you can check by using **pwd**, by *default* you should be in the **home** folder).
- **Change the comma-separated file to a tab-separated file** by using the new aliases (**hint**: use subcomma)
- **Evaluate the first 10 lines**. Remember you can use pipes (**hint:** use h)
---

:traffic_light:
- Solution (first try on your own):

```sh
#We use the new alias arbitrarily called "subcomma"
$ subcomma iris.csv                           #substitutes "," for "tabs"
$ subcomma iris.csv | h                       #substitutes "," for "tabs" and shows the first 10 lines
$ subcomma iris.csv | h | column -t           #same as above and prints the table nicely in the Terminal

sepal_length  sepal_width  petal_length  petal_width  species
5.1           3.5          1.4           0.2          setosa
4.9           3.0          1.4           0.2          setosa
4.7           3.2          1.3           0.2          setosa
4.6           3.1          1.5           0.2          setosa
5.0           3.6          1.4           0.2          setosa
5.4           3.9          1.7           0.4          setosa
4.6           3.4          1.4           0.3          setosa
5.0           3.4          1.5           0.2          setosa
4.4           2.9          1.4           0.2          setosa

$ subcomma iris.cvs > iris.tsv               #substitutes "," for "tabs" and saves the file tab delimited 
```
---



- Many other aliases can be added (NOTE: This part **is just to show what can be done** in the .bashrc)

```sh
#Basic file conversion by calling tailored made scripts 

alias FastatoTbl='bash ~/Scripts/fastatotbl.sh'
alias TbltoFasta='bash ~/Scripts/tbltofasta.sh'

#Changing Python environments
alias py3='source activate py36'
alias py2='source activate py26'
```

# Installing software 

###  With *root* priviledges:


```sh

#Ubuntu, Debian, Mint
$ sudo apt install app_name 
$ sudo apt update
$ sudo apt upgrade

#Fedora, CentOS, Red Hat    
$ sudo yum install app_name 
$ yum update
```

### Without *root* priviledges (from source)

  - Go to the webpage and copy the download link
  - Download source package/s (you can use wget, curl, save as)
  - Unpack the files (you can use the **untar** alias!)
  - Go inside the folder and check the README file.
  - Build if necessary and use the binary files once built.
  - Add the binaries to your PATH

Generally, you can install in your server or computer by using:

```sh
$ ./configure --prefix=/home/user/.local; make; make install        #Some program of interest
$ pip install --user or python setup.py install --user              #Installing Python modules
```
NOTE: You should always **read the documentation first**, more often than not you have to install dependencies, libraries or preexisting software for your program to work properly.

### :beginner: Exercise 3. Download bam-readcount and install it

### [Bam-readcount](https://github.com/genome/bam-readcount) documentation
- You could try following the directions from their documentation first. Else go straight ahead and follow the instructions below.
```sh
$ git clone https://github.com/genome/bam-readcount.git     #Clone the repo

$ cd ~/bam-readcount                  #work in your home folder
$ cmake ~/bam-readcount               #inside the bam-recount folder
$ make                                #inside the bam-recount folder

$ echo 'export PATH=/home/YOUR_USERNAME/bam-readcount/bin:$PATH' >>~/.bashrc   #Add the PATH to your .bashrc, remember to change "YOUR_USERNAME for your pesonal user name"
$ bam-readcount                       #run it
```
You can also:
  - Open your ~/.bashrc and add the following line directly there:
```sh
$ gedit ~/.bashrc                                       #Open Gedit
export PATH="$PATH:/home/you/bam-readcount/"            #Add this line with the path of the program, save and exit
$ source ~/.bashrc                                      #Reload your .bashrc
```
And lastly you can also:

```sh
$ cp -R bam-readcount/bin/* ~/bin      #copy the binaries of the program to your bin folder
```

Try it! It should run without issues
```sh
$ bam-readcount
Usage: bam-readcount [OPTIONS] <bam_file> [region]
Generate metrics for bam_file at single nucleotide positions.
Example: bam-readcount -f ref.fa some.bam

Available options:
  -h [ --help ]                         produce this message
  -v [ --version ]                      output the version number
  -q [ --min-mapping-quality ] arg (=0) minimum mapping quality of reads used 
                                        for counting.
  -b [ --min-base-quality ] arg (=0)    minimum base quality at a position to 
                                        use the read for counting.
  -d [ --max-count ] arg (=10000000)    max depth to avoid excessive memory 
                                        usage.
  -l [ --site-list ] arg                file containing a list of regions to 
                                        report readcounts within.
  -f [ --reference-fasta ] arg          reference sequence in the fasta format.
  -D [ --print-individual-mapq ] arg    report the mapping qualities as a comma
                                        separated list.
  -p [ --per-library ]                  report results by library.
  -w [ --max-warnings ] arg             maximum number of warnings of each type
                                        to emit. -1 gives an unlimited number.
  -i [ --insertion-centric ]            generate indel centric readcounts. 
                                        Reads containing insertions will not be
                                        included in per-base counts

```
Relevant *xkcd comics* [universal install](https://xkcd.com/1654/) and [success...](https://xkcd.com/349/)


# GNU Parallel 

GNU parallel is a shell tool for executing jobs in parallel using one or more computers. More info [here](https://www.gnu.org/software/parallel/)

  - Install GNU parallel 

Quick install in Ubuntu, Debian or Mint:

```sh
sudo apt-get install parallel
```

Or if you are feeling like practicing the previous knowledge:
```sh
$ wget https://ftpmirror.gnu.org/parallel/parallel-20181022.tar.bz2
$ bzip2 -dc parallel-20181022.tar.bz2 | tar xvf -
$ cd parallel-20181022
$ ./configure && make && sudo make install
```
([More installation options here](http://git.savannah.gnu.org/cgit/parallel.git/tree/README))

### Examples:

The input of parallel can be referred by using curly brackets **{}** . In the following example we can input all human chromosomes to parallel:
```sh
parallel echo chr{}.fa ::: {1..22} X Y M | head -5     #see the first five chromosomes
```

Run a blat for all chromosomes, you can use --dryrun to see the commands before running it to evaluate it:
```sh
parallel --dryrun blat chr{}.fa human/test.fa test_{}.psl ::: {1..22} X Y M | head -5
```
Run FASTQC in multiple files (10 in this case) simultaneously:
```sh
ls *.fq | parallel  -j 10 "fastqc {} --outdir ."
```
Align multiple files with bwa:
```sh
find ./ -name "*.fastq.gz"| parallel --dryrun bwa aln -f {/.}.sai dummy.fa {}
```

ls *.sam | parallel "samtools view -b -S {} | samtools sort - {.}; samtools index {.}.bam"

### :beginner: Exercise 4. 

  - This [Biostar](https://www.biostars.org/p/63816/) thread is really good
 ```
 
 ### :beginner: Exercise 4. 

  
  
  

### Resources

Some useful links for further reading; the internet is full of information.

| Plugin | README |
| ------ | ------ |
| More on Installation | [https://github.com/mr-c/misc/wiki/Linux-Home-Directory-Program-Installation] |
| Useful Oneliners including aliases | [https://github.com/stephenturner/oneliners] |
| Official GNU Parallel Tutorial | [https://www.gnu.org/software/parallel/parallel_tutorial.html] |
| More on GNU Parallel  | [https://davetang.org/muse/2013/11/18/using-gnu-parallel/] |

### Todos

 - Make many aliases
 - Install more software
 - Parallelize everything

