---
title: "Researching Digital Life"
subtitle: "Lectures 6-9 Introduction"
author:
  name: Christopher Barrie
  affiliation: University of Edinburgh | [RDL](https://github.com/cjbarrie/RDL-Ed)
# date: Lecture 6  #"04 February 2021"
output: 
  html_document:
    theme: flatly
    highlight: haddock
    # code_folding: show
    toc: yes
    toc_depth: 4
    toc_float: yes
    keep_md: true
    
bibliography: RDL.bib    
---

# Introduction

This set of online documents is designed to give you some hands-on examples of analysing different types of data using various computational techniques.

The contents of each week's lecture is by no means exhaustive---these are designed to give you an introductory taste of different quantitative computational techniques, and the chance to try your hand at them yourselves. 

The exercises I provide use the <tt>R</tt> programming language. For the uninitated (and the initiated!) a great point of reference is the book "R For Data Science" by @Wickham2017.

Each week the readings selected are aimed at the analysis of a different type of data. Here, I aim to convince you that large-N quantitative analyses can rely on diverse forms of data and be credibly paired with more qualitative modes of analysis.

In the last instance, what we are working with are quantitative information arranged in the form of a spreadsheet. In <tt>R</tt>, we usually refer to these spreadsheets as ``dataframes." These are, quite simply, sets of variables (vectors of numbers or words), stored as columns alongside each other. Nothing more, nothing less!

What we'll discover over the course of this module is that these data, while similar in appearance, permit us to answer an extremely diverse set of questions.

Note: The articles are challenging but accessible. You will not understand every last thing in them. But I ask that you try to unpick the underlying intuition of the articles and think about what can and cannot be answered with the methods used. 

Think also about validity. This might be "construct" validity, i.e., whether the authors manage to capture what they claim to be measuring with the measurement techniques they use; "internal" validity, i.e., whether the analytical techniques (quantitative, computational or otherwise) they use are consistently capturing what they claim to be capturing; and external validity, i.e., whether their methods capture something that has generalizable lessons for other contexts. 

Finally, think too about sampling: where did the data come from? How was it generated? Are there biases built into how it was generated?

# Introduction to R 

This section is designed to ensure you are familiar with the <tt>R</tt> environment. It also provides guidelines on how to use the Swirl package in <tt>R</tt>: a built-in tutorial that familiarizes users with basic <tt>R</tt> commands. I thank Julia de Romémont for sharing an earlier version of this introductory section. 

## Getting started with R at home 

Given that we're all working from home these days, you'll need to download R and RStudio onto your own devices. R is the name of the programming language that we'll be using for coding exercises; RStudio is the IDE ("Integrated Development Environment"), i.e., the piece of software that almost everyone uses when working in R. 

You can download both of these on Windows and Mac easily and for free. This is one of the first reasons to use an "open-source" programming language: it's free! And this means everyone has access to it. 

1. Install R for Mac from here: https://cran.r-project.org/bin/macosx/. Install R for Windows from here: https://cran.r-project.org/bin/windows/base/.

2. Download RStudio for Windows or Mac from here: https://rstudio.com/products/rstudio/download/, choosing the Free version: this is what most people use and is more than enough for all of our needs.

**All programs are free. Make sure to load everything listed above for your operating system or R will not work properly!**

## Some basic information 

+ A script is a text file in which you write your commands (code) and comments.

+ If you put the <tt>#</tt> character in front of a line of text this line will not be executed; this is useful to add comments to your script!

+ <tt>R</tt> is case sensitive, so be careful when typing. 

+ To send code from the script to the console, highlight the relevant line of code in your script and click on <tt>Run</tt>, or select the line and hit <tt>ctrl+enter</tt> on PCR or <tt>cmd+enter</tt> on Mac

+ Access help files for <tt>R</tt> functions by preceding the name of the function with <tt>?</tt> (e.g., <tt>?table</tt>)

+ By pressing the <tt>up</tt> key, you can go back to the commands you have used before

+ Press the <tt>tab</tt> key to auto-complete variable names and commands

## Getting Started in RStudio 

Begin by opening RStudio (located on the desktop). Your first task is to create a new script (this is where we will write our commands). To do so, click: 


```r
File --> NewFile --> RScript
```

Your screen should now have four panes:

+ the Script (top left)

+ the Console (bottom left)

+ the Environment/History (top right)

+ Files/Plots/Packages/Help/Viewer (bottom right)

## A simple example 

The Script (top left) is where we write our commands for R. You can try this out for a first time by writing a small snipped of code as follows:


```r
x <- "I can't wait to learn Quantitative Research Methods" #Note the quotation marks!
```
To tell R to run the command, highlight the relevant row in your script and click the <tt>Run</tt> button (top right of the Script) - or hold down <tt>ctrl+enter</tt> on Windows or <tt>cmd+enter</tt> on Mac - to send the command to the Console (bottom left), where the actual evaluation and calculations are taking place. These shortcut keys will become very familiar to you very quickly!

Running the command above creates an object named ‘x’, that contains the words of your message.

You can now see ‘x’ in the Environment (top right). To view what is contained in x, type in the Console (bottom left):

```r
print(x)
```

```
## [1] "I can't wait to learn Quantitative Research Methods"
```

```r
# or alternatively you can just type:

x
```

```
## [1] "I can't wait to learn Quantitative Research Methods"
```

## Loading packages 
The 'base' version of <tt>R</tt> is very powerful but it will not be able to do everything on its own, at least not with ease. For more technical or specialized forms of analysis, we will need to load new packages. 

This is when we will need to install a so-called ‘package’---a program that includes new tools (i.e., functions) to carry out specific tasks. You can think of them as 'extensions' enhancing <tt>R</tt>'s capacities. To take one example, we might want to do something a little more exciting than print how excited we are about this course. Let's make a map instead.

This might sound technical. But the beauty of the packaged extensions of <tt>R</tt> is that they contain functions to perform specialized types of analysis with ease. We'll first need to install one of these packages, which you can do as below:


```r
install.packages("tidyverse")
```

You can load the most recent version of packages using RStudio (by clicking <tt>Install</tt> under the packages tab of the bottom right pane and typing the name of your desired package) and ensuring the top drop down menu says install from Repository (CRAN). Keep <tt>Install dependencies</tt> ticked.

After the package is installed, we then need to load it into our environment by typing <tt>library(<insert name of package here>)</tt>. Note that, here, you don't need to wrap the name of the package in quotation marks. So this will do the trick:


```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.0 ──
```

```
## ✓ ggplot2 3.3.3     ✓ purrr   0.3.4
## ✓ tibble  3.0.5     ✓ dplyr   1.0.3
## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
## ✓ readr   1.4.0     ✓ forcats 0.5.0
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

What now? Well, let's see just how easy it is to visualize some data using <tt>ggplot</tt> which is a package that comes bundled into the larger <tt>tidyverse</tt> package.


```r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy))
```

![](01-intro_files/figure-html/unnamed-chunk-6-1.png)<!-- -->

If we wanted to save where we'd got to with making our plots, we would want to save our scripts, and maybe the data we used as well, so that we could return to it at a later stage.

## Saving your objects, plots and scripts 

* Saving scripts: To save your script in RStudio (i.e. the top left panel), all you need to do is click File –> Save As (and choose a name for your script). Your script will be something like: myfilename.R.

* Saving plots: If you have made any plots you would like to save, click Export (in the plotting pane) and choose a relevant file extension (e.g. .png, .pdf, etc.) and size.

+ To save **individual** objects (for example <tt>x</tt> from above) from your environment, run the following command (choosing a suitable filename): 


```r
save(x,file="myobject.RData")
load(file="myobject.RData")
```
      
+ To save **all** of your objects (i.e. everything in the top right panel) at once, run the following command (choosing a suitable filename):


```r
save.image(file="myfilname.RData")
```

+ Your objects can be re-loaded into R during your next session by running:


```r
load(file="myfilename.RData")
```

## Knowing where R saves your documents 

If you are at home, when you open a new script make sure to check and set your working directory (i.e. the folder where the files you create will be saved). To check your working directory use the getwd() command (type it into the Console or write it in your script in the Source Editor):


```r
getwd()
```

To set your working directory, run the following command, substituting the file directory of your choice. Remember that anything following the `#’ symbol is simply a clarifying comment and R will not process it.


```r
## Example for Mac 
setwd("/Users/Documents/mydir/") 
## Example for PC 
setwd("c:/docs/mydir") 
```

## Practicing in R 

You're going to have your own lab tutorials in <tt>R</tt> and so this is not the appropriate place to teach you everything about the programming language. This course is principally designed to get you thinking about quantitative research methods. What I recommend that **all** of you do, though, before we begin our classes is to familiarize yourself with some of the basics of <tt>R</tt> in your own time.

The best places to start doing this are:

- The free online book by Hadley Wickham "R for Data Science" available [here](https://r4ds.had.co.nz/)

- A set of interactive tutorials, available through the package "learnr." Once you've installed this package, you can go through the tutorials yourselves by calling:


```r
library(learnr)

available_tutorials() # this will tell you the names of the tutorials available

run_tutorial(name = "ex-data-basics", package = "learnr") #this will launch the interactive tutorial in a new Internet browser window
```

## One final note 

Once you've dipped into the "R for Data Science" book you'll hear a lot about the so-called <tt>tidyverse</tt> in R. This is essentially a set of packages that use an alternative, and more intuitive, way of interacting with data. The main difference you'll notice here is that, instead of having separate lines for each function we want to run, sets of functions are "piped" into each other using "pipe" functions, which look have the appearance: `%>%`. 

In the first set of weekly exercises I will provide code in both the base R way, which you will predominantly use for your stats. tutorials. From Week One onwards I will only be using <tt>tidyverse</tt> syntax. It is worth getting used to this syntax because it has recently been incorporated into base R functionality, meaning it will likely become the norm from now on.


## References
