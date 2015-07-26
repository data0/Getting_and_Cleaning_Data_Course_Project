---
title: "CodeBook"
author: "Serge"
date: "07/26/2015"
output: html_document
---

#Getting and Cleaning Data Course Project CodeBook


|Object Name|Type|Dimension|Description|Values or Explanation|
|---|---|---|---|---|
|X_train|data.frame|7352x561|Training set|Described in the features_info.txt file|
|y_train|data.frame|7352x1|Training labels|Its range is from 1 to 6|
|X_test|data.frame|2947x561|Test set|Described in the features_info.txt file|
|y_test|data.frame|2947x1|Test labels|Its range is from 1 to 6|
|subjTrain|data frame|7352x1|Subject identifiers for Training set|Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to 30|
|subjTest|data frame|2947x1|Subject identifiers for Test set|Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to 30|
|train|data.frame|7352x563|Training set, labels and subjects|Merged all traning data|
|test|data.frame|2947x563|Test set, labels and subjects |Merged all test data|
|data|data.frame|10299x563|Full data set, labels and subjects|Merged all data|
|dataFeatures|data.frame|561x2, 66x2|List of features|Mean and standard deviation features have been extracted from the original list of features. "(", ")" and "-" have been removed from feature names to make them human friendly|
|dataStrip|data.frame|10299x66, 10299x68|Mean and standard deviation data set|The measurements on the mean and standard deviation have been extracted from the original data set. Variable names are taken from dataFeatures. Two last rows included for activity and subject variables. Descriptive activity names from activityLab used to name the activities in the data set|
|activityLab|character array|6x2|Array links the labels with their activity name|Character vector with lables and activity name transformed into a 6x2 character array|
|dataSplit|list of data.frame|180|List of measurements grouped by activities and subjects|split function used to create a measurement list grouped by activities and subjects|
|meanActivitySubj|numeric, data.table|180x66, 180x68|Data set with the average of each variable for each activity and each subject|sapply function used to calculate the average for each element defined on the dataSplit list. The new data set is transposed to have measurements in rows. Two additional columns for activities and subjects. Finally the tidy data set is reordered by activities and subjects, and saved for futher submission|
|nameSplit|list of character|180|List of activities and subjects|The list is taken from meanActivitySubj row names.  Used to separate the activity and subject variables|
|activity|character|180|Activity vector|Activity vector will be included into the final tidy data set|
|subj|character|180|Subject vector|Subject vector will be included into the final tidy data set|

                                                            
 