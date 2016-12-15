<style>
.small-code pre code {
  font-size: 1em;
}
</style>

Let's Code - Week 1
========================================================
author: Adrien ROUX
date: January, 2017
autosize: true

Getting started with R (1/.)
========================================================

R works on pretty much every platform available, including the widely available Windows, Mac OS X, and Linux systems. To get started you basically need 2 things :

1. **R kernel**, e.g. R-3.3.0. It is open source. Usually you start to install the base kernel and then add packages on the fly when they are needed. On my computer, the kernel is installed in C:\Program Files\Microsoft\MRO\R-3.3.0.

1. The **IDE** (**I**ntegrated **D**evelopment **E**nvironment) of your choice : I highly recommend **RStudio**, which is widely used and is free as long as you're fine with the desktop version. Non-free server versions of RStudio exist too and are necessary for more advanced/commercial use of R.

Links for download: 


Getting started with R (2/.)
========================================================

In XXI century, coding often happens in group/team. Sharing (public or restricted) often allows you to leverage on other's work. Other developers may send you suggestions so you benefit from other's ideas or experience. 

Sharing is easily done through IDE using a source control software, e.g. **Git**.

**NB:** Please make sure the installs are perfomed in the order specified above. Otherwise some  manipulations are required to allow the IDE to work as expected.

Usually for professional developers, code is shared over private repositories stored on the company's servers. As we are beginners and the content of our code is not sensitive, we are going to use **GitHub.com**. 

Link to **GitHub**: <https://github.com/Yenyenx/LetsCode-Contents>


R Nuts and Bolts (1/.)
========================================================
class: small-code

Enough talking... Let's start coding. As we go through some exercices, I'll take some time to give you more background on **R**, my favorite IDE **RStudio**, **Git** and **GitHub**.

A first basic example (at least to test that what we installed so far is working well).

Declare and instanciate a variable :

```r
x <- 1; y = 10
```


```r
print(x);
```

```
[1] 1
```

x is equal to 1 and y equals 10.

R Nuts and Bolts (2/.)
========================================================
class: small-code

You should become familiar with:
- the help embedded in the IDE: **?function.name**, e.g. *?strsplit*,
- warnings and error messages sent by the **R** console,
- 


Quick review of the basic algebra operations : +, -, *, / and first manipulation with *string*


```r
2 * x / 2.0 - 0.0
```

```
[1] 1
```


```r
str1 <- "Default_Name_0101"
strsplit(str1, "_")
```

```
[[1]]
[1] "Default" "Name"    "0101"   
```

A more advanced example (1/.)
========================================================
class: small-code

R base package comes with standard datasets often used to present method behavior and test packages. Here is the *cars* dataset.


```r
summary(cars)
```

```
     speed           dist       
 Min.   : 4.0   Min.   :  2.00  
 1st Qu.:12.0   1st Qu.: 26.00  
 Median :15.0   Median : 36.00  
 Mean   :15.4   Mean   : 42.98  
 3rd Qu.:19.0   3rd Qu.: 56.00  
 Max.   :25.0   Max.   :120.00  
```

A more advanced example (2/.)
========================================================
class: small-code

Here is the simplest way to present a graph. Even when coding, taking some time to briefly look at the data using a quickly generated graph is a good practice.

![plot of chunk unnamed-chunk-6](Week1-figure/unnamed-chunk-6-1.png)




