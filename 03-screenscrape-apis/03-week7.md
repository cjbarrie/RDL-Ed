---
title: "Researching Digital Life"
subtitle: "Lecture 7: Screen-scraping and APIs"
author:
  name: Christopher Barrie
  affiliation: University of Edinburgh | [RDL](https://github.com/cjbarrie/RDL-Ed)
# date: Lecture 6  #"24 February 2021"
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


# Week 7: Screen-scraping and APIs

This week you had readings by @Freelon2018a, @Bruns2019, @Puschmann2019, and @Lazer202b as well as a [report](https://www.disinfobservatory.org/download/26541) by SOMA outlining solutions for research data exchange. 

The hands-on exercise for this week uses different sources of online data, and here I introduce you to how we might gather data through both screen-scraping (or server-side) techniques as well as API (or client-side) techniques.

## Week 7 Exercise 

In this tutorial, you will learn how to summarise, aggregate, and analyze text in R:

* How to select elements of CSS using SelectorGadget
* How to use the <tt>rvest</tt> package to scrape CSS elements
* How to use the Twitter API

## Setup 

To practice these skills, we will use a series of webpages on the Internet Archive that host material collected at the Arab Spring protests in Egypt in 2011. The original website can be seen [here](https://www.tahrirdocuments.org/) and below.

<iframe src="https://www.tahrirdocuments.org/" width="100%" height="400px"></iframe>

This might sound complicated but it isn't really. In essence, APIs simply provide data in a more usable format without the need for alternative techniques such as web scraping. Be warned, too, that some websites do not permit automated web scraping, meaning the use of an API is essential.

##  Load data and packages 

Beforce proceeding, we'll load the remaining packages we will need for this tutorial.


```r
library(tidyverse) # loads dplyr, ggplot2, and others
library(ggthemes) # includes a set of themes to make your visualizations look nice!
library(readr) # more informative and easy way to import data
library(stringr) # to handle text elements
library(rvest) #for scraping
```

We can download the final dataset we will produce with:


```r
pamphdata <- read_csv("data/pamphlets_formatted_gsheets.csv")
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   title = col_character(),
##   date = col_date(format = ""),
##   year = col_double(),
##   text = col_character(),
##   tags = col_character(),
##   imageurl = col_character(),
##   imgID = col_character(),
##   image = col_character()
## )
```

If you're working on this document from your own computer ("locally") you can download the Edinburgh Fringe data in the following way:


```r
pamphdata <- read_csv("https://raw.githubusercontent.com/cjbarrie/RDL-Ed/main/03-screenscrape-apis/data/pamphlets_formatted_gsheets.csv")
```


## Inspect and filter data 

Let's have a look at what we will end up producing:


```r
colnames(pamphdata)
```

```
## [1] "title"    "date"     "year"     "text"     "tags"     "imageurl" "imgID"   
## [8] "image"
```

And then: 


```r
glimpse(pamphdata)
```

```
## Rows: 523
## Columns: 8
## $ title    <chr> "The Season of Anger Sets in Among the Arab Peoples", "The M…
## $ date     <date> 2011-03-30, 2011-03-30, 2011-03-30, 2011-03-30, 2011-03-30,…
## $ year     <dbl> 2011, 2011, 2011, 2011, 2011, 2011, 2011, 2011, 2011, 2011, …
## $ text     <chr> "The Season of Anger Sets in Among the Arab Peoples,,A membe…
## $ tags     <chr> "Solidarity", "Solidarity, Workers", "Solidarity, Workers", …
## $ imageurl <chr> "https://wayback.archive-it.org/2358/20120130161341im_/http:…
## $ imgID    <chr> "imgID1", "imgID2", "imgID3", "imgID4", "imgID5", "imgID6", …
## $ image    <chr> "=Arrayformula(image(F2,2))", NA, NA, NA, NA, NA, NA, NA, NA…
```


## References 
