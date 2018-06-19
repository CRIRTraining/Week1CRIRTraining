---
title: "Week One Introduction"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
First step is to install R Markdown

R Markdown is one way to break up the code and make it easier to work in R Studio.
It also allows you to post results on the internet.

You can write comments in the white space and insert lines of code for R using the insert button and select R.  You need to write in between the r code.

If nothing else R can work as a fancy calculator.  

To run code in R Markdown, you can hit the play button for each chunck, hit run at the top, or highlight the code and hit command enter if you just want to run some of the code.
```{r}
5+5
10/5
(10*2+6/80)^3
```
Most of the time you will want to assign variable so you can work with them later on.  
```{r}
a = 5
b = 10
a/b
a^b
a*b
```
You can assign letters and phrases as well, but you need to use parentheses.  To print, the results just rewrite the variable on its own line.
```{r}
R = "R Rules SPSS Drools!!"
R
```
R has several different types of data.  We will review integer, double, and factor.

Integers and double are basically the same and contain only numbers; however double accounts for variables with decimals.

Using "c" means concatenate and is one way to combine elements like numbers in R.
```{r}
integer = as.integer(c(2,4,5,6))
typeof(integer)
double = c(4.5, 6.5, 9, 10)
typeof(double)
```
Factors can either be numbers or words.  For example, a gender factor could be male, female, another gender identity, or 0,1,2.

If gender is numbers, you will want to tell R that the gender is a factor by making it a factor using the as.factor and overwriting the variable (or making a new variable).

If your variable is coded as words, you can change the reference level (i.e. the word that is alphabetically first) by using the relevel function and setting a new reference level.
```{r}
genderNumbers = as.factor(c(0,1,2))
genderNumbers

genderWords = as.factor(c("Male", "Female", "Another gender identity"))
genderWords

genderWords = relevel(genderWords, ref = "Male")
genderWords
```
There are several different data types in R as well.  We will cover vectors, matrices, data frames.

We have mostly been dealing with vectors so far.  They are one row of data.  You can add them and each element will be added to the corresponding element.
```{r}
vector_var1 = as.vector(c(2,3,45))
vector_var1
vector_var2 = as.vector(c(5,4,3))

vector_var12 = vector_var1+vector_var2; vector_var12
```
We can combine vectors to create matrices.  You will need to specify the number of rows and columns.  Given that we have two variables there should be two columns and three rows because each vector as three data points.  Vectors with differing numbers of rows cannot be combined.  To subset the data you can use []
```{r}
vector_var1 = as.vector(c(2,3,45))
vector_var1
vector_var2 = as.vector(c(5,4,3))
matrix12 = matrix(vector_var1,vector_var2, nrow = 3, ncol = 2)

#Rows 
matrix12[1,]
#Columns
matrix12[,1]
#Both
matrix12[1,2]
```
The most common data type you all will be working with is a data.frame.  Data frames need variable names.

You can use the $ to get the variables, use the matrix notation, or use attach and just use the actual name.
```{r}
data.frame12 = data.frame(vector_var1,vector_var2)
data.frame12

data.frameNames = data.frame(var1 = c(1,2,3), var2 = c(4,5,6))
data.frameNames

data.frame12$vector_var1
data.frame12[,1]

attach(data.frameNames)
var1
var2

```
You can also use logical operations like you would in excel.
```{r}
var1 > var2
var1 == var2
var2 > var1
```
The first thing you want to do is set the working directory.  This tells R where you want to read in and store data sets.  Go to the session, set working directory, then choose the working directory.  Then you can copy that path into the code so you don't have to do that every time.

***** I am working on a mac so make sure you don't copy and paste the setwd directly from this page and you actually find the specific file path for your computer if you have a PC.

Let's first export the data set that we have to a csv file because that is the easiest file to work with.  We can use the write.csv function to do that.  Row names are likely to be false.

Then you can read the csv file using the read.csv function.  Most of the time the first row in the dataset will be the variable names, so you will need to set the header to be true.  You can also specify which data points are "NA".
```{r}
setwd("~/Desktop")
write.csv(data.frameNames, "data.frameNames.csv", row.names = FALSE)
data.frameNames = read.csv("data.frameNames.csv", header = TRUE, na.strings = c("NA", " "))

```
To get some summary statistics we will need some different statistical packages.  This means we need to use the install.packages function to install the psych and prettyR packages and then library them.

You can also get summary statistics fairly quickly using summary and or describe for continuous variables and describe.factor for ordinal, categorical, and binary types.

describe.factor only works with a single variable; however, we will learn how to use it to provide counts and percentages for several variables at a time.
```{r}
#install.packages("psych")
#install.packages("prettyR")
library(psych)
library(prettyR)
summary(data.frameNames)
describe(data.frameNames)
describe.factor(genderWords) 
```
Also, to better understand the packages you can use the help function
```{r}
help("summary")
```


Homework: Find a data set that you have access to (let Matt know if you need a data set) and get means and sds for the continuous variables (or all of them).  Also if possible get counts and percentages for one categorical variable.







