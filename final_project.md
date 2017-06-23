---
title: "final_project"
output: html_document
---


```{r}
library(caret)
library(randomForest)
library(rpart)
library(rpart.plot)
set.seed(1234)
```
## We spilt the data
```{r}
trainingset <- read.csv("C:/Users/User/Desktop/coursera/training_set.csv", na.strings=c("NA","#DIV/0!", ""))

testingset <- read.csv("C:/Users/User/Desktop/coursera/test_set.csv", na.strings=c("NA","#DIV/0!", ""))

trainingset<-trainingset[,colSums(is.na(trainingset)) == 0]

testingset <-testingset[,colSums(is.na(testingset)) == 0]
```

```{r}
inTrain <- createDataPartition(y=trainingset$classe, p=0.75, list=FALSE)
Training1 <- trainingset[inTrain, ] 
Testing1 <- trainingset[-inTrain, ]
```

## Start Predicting and the plot a Decision Tree using rPart
```{r}
model1 <- rpart(classe ~ ., data=Training1, method="class")
prediction1 <- predict(model1, Testing1, type = "class")
rpart.plot(model1, main="Classification Tree", extra=102, under=TRUE, faclen=0)
confusionMatrix(prediction1, Testing1$classe)

```
## Start Predicting and the plot a Decision Tree using randomforest
```{r}
model2 <- randomForest(classe ~. , data=Training1, method="class")
prediction2 <- predict(model2, Testing1, type = "class")
confusionMatrix(prediction2, Testing1$classe)
```


