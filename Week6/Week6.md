<style>
.small-code pre code {
  font-size: 1em;
}
</style>

Let's Code - Week 6
========================================================
author: Adrien ROUX
date: January, 2017
autosize: true

Getting Data In and Out of R
========================================================
class: small-code

Multiple use cases:
* data are available **on your computer locally** or through **local network**,
* data are available through **R repositories** => reference dataset,
* data is stored in outside world...: classic web or API.

But first of all, let us learn how to manipulate file and folder in R.

Basic file manipulation (1/)
========================================================
class: small-code

File manipulation in R:
* **file.create(..., showWarnings = TRUE)** : creates files with the given names if they do not already exist and truncates them if they do. They are created with the maximal read/write permissions.


```r
file.create("HelloWorld.txt", showWarnings = T)
```

```
[1] TRUE
```

```r
file.create(c("File1.txt", "File2.txt"), showWarnings = T)
```

```
[1] TRUE TRUE
```

* **file.exists(...)** :  returns a logical vector indicating whether the files exist. (Here *exists* is in the sense of the system's stat call: a file will be reported as existing only if you have the permissions needed.)


```r
file.exists("HelloWorld.txt")
```

```
[1] TRUE
```

```r
file.exists("Blabla.txt")
```

```
[1] FALSE
```

**NB:** the existence of a file does not imply that it is readable.

Basic file manipulation (2/)
========================================================
class: small-code

* **file.rename(from, to)** : 

```r
file.rename("File1.txt", "File1.csv")
```

```
[1] TRUE
```

* **file.copy(from, to, overwrite = recursive, recursive = FALSE, copy.mode = TRUE, copy.date = FALSE)** :

```r
file.copy(from="File2.txt", to="File3.txt")
```

```
[1] TRUE
```

Basic file manipulation (3/)
========================================================
class: small-code

* **file.remove(...)** : attempts to remove the files named in its argument. On Windows, *file* means a regular file and not, say, an empty directory.

```r
file.remove("File3.txt")
```

```
[1] TRUE
```

* **file.info(...)**,
* **file.access(...)**.

**NB:** All these methods are available in base package.

A first basic example
========================================================
class: small-code


```r
if(file.create("BasicExample.txt")) {
  fileConn <- file("BasicExample.txt")
  writeLines("First Basic Example", fileConn)
  close(fileConn)  
}

if(file.exists("BasicExample.txt")) {
  if(!file.copy("BasicExample.txt", "BasicExample2.txt")) {
    warning("file not properly copied!")
  }
}

if(file.exists("BasicExample.txt") & file.exists("BasicExample2.txt")) {
  if(!file.append("BasicExample.txt", "BasicExample2.txt")){
    warning("Appending data to file went wrong!")
  }
}

if(file.exists("BasicExample.txt")) {
  content <- readLines(fileConn <- file("BasicExample.txt"))
  print(content)
  close(fileConn)  
}
```

```
[1] "First Basic Example" "First Basic Example" "End of file"        
```

```r
if(file.exists("BasicExample.txt")) {
  if(!file.remove("BasicExample.txt")) {
    warning("File not properly removed!")
  }
}
```

Basic folder manipulation
========================================================
class: small-code

folder manipulation:
* **list.files()**: produce a character vector of the names of files or directories in the named directory.
* **getwd()**: returns an absolute filepath representing the current working directory of the R process.
* **setwd(**dir**)**: used to set the working directory to *dir*.
* **dir.create(**path**)**: creates a new directory.
* **dir.exists(**paths**)**: checks if a list of directories exist.

A first basic example
========================================================
class: small-code


```r
list.files()
```

```
[1] "BasicExample2.txt" "File1.csv"         "File2.txt"        
[4] "HelloWorld.txt"    "R google API.txt"  "Test.xls"         
[7] "Test.xlsx"         "Week6.html"        "Week6.Rpres"      
```

```r
list.dirs()
```

```
[1] "."
```

Reading data into R
========================================================
class: small-code

There are a few principal functions reading data into R:

* **read.table**, **read.csv**, for reading tabular data ;
* **readLines**, for reading lines of a text file
* **source**, for reading in R code files (inverse of dump)
* **dget**, for reading in R code files (inverse of dput)
* **load**, for reading in saved workspaces
* **unserialize**, for reading single R objects in binary form.

There are of course, many R packages that have been developed to read in all kinds of other datasets, and you may need to resort to one of these packages if you are working in a specific area.

A first example
========================================================
class: small-code


```r
library(RCurl) #getURL
url <- "https://opendata.paris.fr/explore/dataset/les-1000-titres-les-plus-reserves-dans-les-bibliotheques-de-pret/download/?format=csv&timezone=Europe/Berlin&use_labels_for_header=true"
x <- getURL(url)
out <- read.csv(textConnection(x), sep=";")
str(out)
```

```
'data.frame':	1000 obs. of  6 variables:
 $ Support                    : Factor w/ 22 levels "Bande dessinée jeunesse",..: 12 18 16 18 16 12 8 12 12 18 ...
 $ Auteur                     : Factor w/ 375 levels "","Abi Rasid, Zinai",..: 121 328 362 127 208 102 1 131 221 306 ...
 $ URL.de.la.fiche.de.l.auteur: Factor w/ 624 levels "","https://bibliotheques.paris.fr/Default/doc/SYRACUSE/1000013",..: 36 314 85 301 17 607 1 603 221 321 ...
 $ Titre                      : Factor w/ 993 levels "10 Cloverfield lane [images animées]",..: 497 131 172 759 445 960 709 368 913 66 ...
 $ URL.de.la.fiche.de.l.oeuvre: Factor w/ 1000 levels "http://b14-sigb.apps.paris.mdp/vdp/LinkToVubis.csp?title=Game%20of%20Thrones&Database=1&Profile=Default&NumberToRetrieve=10",..: 54 577 129 563 30 963 163 957 388 584 ...
 $ Nombre.de.réservations     : int  1094 668 667 538 502 421 420 369 326 283 ...
```

Reading data from MS Excel files
========================================================
class: small-code


```r
library(openxlsx)
df <- read.xlsx("Test.xlsx", sheet= 1, startRow= 1, colNames = T)
str(df)
```

```
'data.frame':	4 obs. of  2 variables:
 $ Name: chr  "Adrien" "Bob" "Adrien" "Bob"
 $ Dist: num  10 45 20 42
```

```r
library(readxl)
df <- read_excel("Test.xls", sheet= 1)
str(df)
```

```
Classes 'tbl_df', 'tbl' and 'data.frame':	4 obs. of  3 variables:
 $ Name: chr  "Adrien" "Bob" "Adrien" "Bob"
 $ Dist: num  10 45 20 42
 $ Unit: chr  "km" "km" "miles" "km"
```

Using the readr Package
========================================================
class: small-code

The readr package is recently developed by Hadley Wickham to deal with reading in large flat
files quickly. The package provides replacements for functions like read.table() and read.csv(). The analogous functions in readr are **read_table()** and **read_csv()**. This functions are oven much faster than their base R analogues and provide a few other nice features such as progress meters.






Using Textual and Binary Formats for Storing Data
========================================================
class: small-code




Interfaces to the Outside World
========================================================
class: small-code

Data are read in using connection interfaces. Connections can be made to files (most common) or to other more exotic things.

- file, opens a connection to a file
- gzfile, opens a connection to a file compressed with gzip
- bzfile, opens a connection to a file compressed with bzip2
- url, opens a connection to a webpage
