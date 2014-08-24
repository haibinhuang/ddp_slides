---
title       : Shiny App -- Iris Classification
subtitle    : 
author      : H Huang
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Introduction


This famous (Fisher's or Anderson's) iris data set gives the measurements in centimeters of the variables sepal length and width and petal length and width, respectively, for 50 flowers from each of 3 species of iris. The species are Iris setosa, versicolor, and virginica.

```r
data(iris); dim(iris)
```

```
## [1] 150   5
```

```r
sub <- iris[c(1,100,150),]; sub
```

```
##     Sepal.Length Sepal.Width Petal.Length Petal.Width    Species
## 1            5.1         3.5          1.4         0.2     setosa
## 100          5.7         2.8          4.1         1.3 versicolor
## 150          5.9         3.0          5.1         1.8  virginica
```

--- .class #id 

## Methods
The famous iris data set has been covered by Data Science class several times. Several methods (tree classification and random forest) have been used to classify the iris species. I have built a model using boosting method (gbm) to perform the classification, which has a quite high prediction accuracy of 0.9333333.


```r
library(caret); data(iris)
inTrain <- createDataPartition(y=iris$Species, p=0.8, list=FALSE)
training <- iris[inTrain,]; testing <- iris[-inTrain,]
model <- train(Species ~ ., method="gbm", data=training)
predictions <- predict(model, newdata=testing)
accuracy <- confusionMatrix(predictions, testing$Species)$overall[1]
accuracy
save(model, file = "model.rda")
```
Training part of the Modeling was done locally. Model saved to a local file and were loaded during app running on remote server.

---

## How to Run App and What to Expect
To run the app, simply visit [here](http://haibinhuang.shinyapps.io/iris/)

"Introduction" page you will encounter when you visit the app homepage:

![Default page of Shiny app -- Iris Classification](iris-1.png)

---

## How to Run App and What to Expect
"Iris Classification" page where you can change your input and get the prediction results:

![Iris Classification page of Shiny app](iris-2.png)



