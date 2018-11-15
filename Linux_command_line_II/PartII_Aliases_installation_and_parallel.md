# Overview
  - Alias (command)
  - Installing software from source (without *root* priviledge) 
  - [GNU Parallel](https://www.gnu.org/software/parallel/parallel_tutorial.html=)
  - Cluster usage (qsub, qstat, etc)

# Alias (command)

An **alias** in computing, is a command in various command line interpreters (shells) such as Unix shells, AmigaDOS, 4DOS/4NT, KolibriOS and Windows PowerShell, which enables a replacement of a word by another string ([source:Wikipedia](https://en.wikipedia.org/wiki/Alias_(command))). You can customize your working environment by modifying your **.bashrc**, for example by adding **aliases**.  

# What is the .bashrc?

[.bashrc](https://unix.stackexchange.com/questions/129143/what-is-the-purpose-of-bashrc-and-how-does-it-work) is a [shell script](https://en.wikipedia.org/wiki/Shell_script) that [Bash](https://www.gnu.org/software/bash/) runs everytime a shell session is initialized. We will learn how to modify it Today.

###  :beginner: Exercise 1.- Customize your working enviroment by adding aliases to your .bashrc


For the purposes of **Today's practical exercises**, we will use [Gedit](https://wiki.gnome.org/Apps/Gedit), [Nano](https://www.nano-editor.org/). However you could use any other editor of your choice, such as [Vim](https://www.vim.org/), [Emacs](https://www.gnu.org/software/emacs/), [Atom](https://atom.io/), [Sublime Text](https://www.sublimetext.com/), among others.

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

###  With root priviledges:


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

### :beginner: Exercise 3. Download bam-readcount and install it


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

  - Drag and drop markdown and HTML files into Dillinger
  - Export documents as Markdown, HTML and PDF

Markdown is a lightweight markup language based on the formatting conventions that people naturally use in email.  As [John Gruber] writes on the [Markdown site][df1]

> The overriding design goal for Markdown's
> formatting syntax is to make it as readable
> as possible. The idea is that a
> Markdown-formatted document should be
> publishable as-is, as plain text, without
> looking like it's been marked up with tags
> or formatting instructions.

This text you see here is *actually* written in Markdown! To get a feel for Markdown's syntax, type some text into the left window and watch the results in the right.

### Tech

Dillinger uses a number of open source projects to work properly:

* [AngularJS] - HTML enhanced for web apps!
* [Ace Editor] - awesome web-based text editor
* [markdown-it] - Markdown parser done right. Fast and easy to extend.
* [Twitter Bootstrap] - great UI boilerplate for modern web apps
* [node.js] - evented I/O for the backend
* [Express] - fast node.js network app framework [@tjholowaychuk]
* [Gulp] - the streaming build system
* [Breakdance](http://breakdance.io) - HTML to Markdown converter
* [jQuery] - duh

And of course Dillinger itself is open source with a [public repository][dill]
 on GitHub.

### Installation

Dillinger requires [Node.js](https://nodejs.org/) v4+ to run.

Install the dependencies and devDependencies and start the server.

```sh
$ cd dillinger
$ npm install -d
$ node app
```

For production environments...

```sh
$ npm install --production
$ NODE_ENV=production node app
```

### Resources

Dillinger is currently extended with the following plugins. Instructions on how to use them in your own application are linked below.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| Github | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |


### Development

Want to contribute? Great!

Dillinger uses Gulp + Webpack for fast developing.
Make a change in your file and instantanously see your updates!

Open your favorite Terminal and run these commands.

First Tab:
```sh
$ node app
```

Second Tab:
```sh
$ gulp watch
```

(optional) Third:
```sh
$ karma test
```
#### Building for source
For production release:
```sh
$ gulp build --prod
```
Generating pre-built zip archives for distribution:
```sh
$ gulp build dist --prod
```
### Docker
Dillinger is very easy to install and deploy in a Docker container.

By default, the Docker will expose port 8080, so change this within the Dockerfile if necessary. When ready, simply use the Dockerfile to build the image.

```sh
cd dillinger
docker build -t joemccann/dillinger:${package.json.version} .
```
This will create the dillinger image and pull in the necessary dependencies. Be sure to swap out `${package.json.version}` with the actual version of Dillinger.

Once done, run the Docker image and map the port to whatever you wish on your host. In this example, we simply map port 8000 of the host to port 8080 of the Docker (or whatever port was exposed in the Dockerfile):

```sh
docker run -d -p 8000:8080 --restart="always" <youruser>/dillinger:${package.json.version}
```

Verify the deployment by navigating to your server address in your preferred browser.

```sh
127.0.0.1:8000
```

#### Kubernetes + Google Cloud

See [KUBERNETES.md](https://github.com/joemccann/dillinger/blob/master/KUBERNETES.md)


### Todos

 - Write MORE Tests
 - Add Night Mode

License
----

MIT


**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)


   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>

