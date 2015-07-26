<<<<<<< HEAD
---
title: "README"
author: "Serge"
date: "07/26/2015"
output: html_document
---

#Getting and Cleaning Data Course Project README
#
###This repo is for Peer Assessments  of the Getting and Cleaning Data Course Project.
#
######Howto:
######1.  Clone this repo (git clone https://github.com/data0/Getting_and_Cleaning_Data_Course_Project.git)
######2.	Launch R-Studio
######3.	Set working directory to the repository location
######4.	Open and launch run_analysis.R script
######5.  run_analysis.R saves tidy data set into the tidyDataSet.txt file
#
#
######run_analysis.R script:

```
## Getting and Cleaning Data Course Project
## run_analysis.R
## My apologies for the bulky and unstructured script. I should spend more effort on planning and code optimization, but I was under time pressure.

## Loading required packages
library("data.table")
library("plyr")

## Downloading and unzipping the dataset
## setwd("~work/r/03/UCI HAR Dataset")
download.file("https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip", destfile="Dataset.zip", method="curl", quiet="True")
unzip("Dataset.zip")


## Loading the training, test and an identifier of the subject data
X_train<-read.table("./train/X_train.txt")
y_train<-read.table("./train/y_train.txt", col.names="y")
X_test<-read.table("./test/X_test.txt")
y_test<-read.table("./test/y_test.txt", col.names="y")
subjTrain<-read.table("./train/subject_train.txt", col.names="subj")
subjTest<-read.table("./test/subject_test.txt", col.names="subj")

## Merging the training and the test data sets
train<-cbind(X_train, y_train, subjTrain)
test<-cbind(X_test, y_test, subjTest)
data<-rbind(train, test)

## Removing unused data objects 
rm(X_test, y_test, X_train, y_train, test, train, subjTest, subjTrain)

## Extracting the measurements on mean and standard deviation for each measurement
## Loading the list of all features
dataFeatures<-read.table("./features.txt")

## Extracting mean and standard deviation features
dataFeatures<-dataFeatures[grep("mean\\(|std\\(", dataFeatures[,2]),]

## Creating human friendly features' names
dataFeatures[,2]<-dataFeatures[, 2]<-sub("\\(\\)", "", dataFeatures[,2])
dataFeatures[,2]<-dataFeatures[, 2]<-gsub("-", "", dataFeatures[,2])

## dataStrip contains the extracted mean and standard deviation measurements
dataStrip<-data[,dataFeatures[,1]]
dataStrip<-cbind(dataStrip, data$y, data$subj)  ## Two last columns for activity and subject
names(dataStrip)<-c(dataFeatures[, 2], "activity", "subj")

## Naming activities with descriptive names
activityLab<-c(1:6, "walking", "walkingUpStairs", "walkingDownStairs", "sitting", "standing", "laying")
dim(activityLab)<-c(6,2)
dataStrip[,"activity"] <- as.factor(activityLab[dataStrip[,"activity"], 2])

## Creating meanActivitySubj data set with the average of each variable for each activity and each subject
## dataSplit is the list of the dataSprip measurements grouped by activities and subjects
dataSplit<-split(dataStrip, f = list(dataStrip$activity, dataStrip$subj))

## meanActivitySubj contains the average of each variable for each activity and each subject
## c(1:{ncol(dataStrip)-2} used to calculate number of measurement columns. 2 last columns used for activities a subjects
meanActivitySubj<-t(sapply(dataSplit, function(x){colMeans(x[, c(1:{ncol(dataStrip)-2})])}))  ##  Transposing the data set

## Reshaping data and creating two additional columns for activities and subjects. 
nameSplit<-strsplit(rownames(meanActivitySubj), "\\.") ## Activities and subject variables are taken from meanActivitySubj row names
activity<-sapply(nameSplit, function(x){x[[1]]})
subj<-sapply(nameSplit, function(x){x[[2]]})
meanActivitySubj<-as.data.table(meanActivitySubj)
meanActivitySubj<-mutate(meanActivitySubj, activity=activity, subj=subj)

## Reordering the data set by activities and subjects
meanActivitySubj$activity<-factor(meanActivitySubj$activity, levels=c("walking", "walkingDownStairs", "walkingUpStairs", "sitting", "standing", "laying" ))
meanActivitySubj<-meanActivitySubj[order(meanActivitySubj$activity, as.integer(meanActivitySubj$subj)),]

## Saving the meanActivitySubj for submission
write.table(meanActivitySubj, "tidyDataSet.txt", row.name=FALSE)

## Removing unused data objects
rm(data, dataFeatures, dataSplit, dataStrip, meanActivitySubj, activityLab, activity, subj, nameSplit)
```
=======
# test-repo
This is a test repo
>>>>>>> 101201aa4298b5350079af3654e88931c1395bf8
