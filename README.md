# README

## Getting and Cleaning Data course project

#### Description of the program

Download File

```r
x_train <- read.table(file.path(pathdata, "train", "X_train.txt"), header = F)
y_train <- read.table(file.path(pathdata, "train", "y_train.txt"),header = F)
subject_train <- read.table(file.path(pathdata, "train", "subject_train.txt"),header = F)

x_test <- read.table(file.path(pathdata, "test", "X_test.txt"),header = FALSE)
y_test <- read.table(file.path(pathdata, "test", "y_test.txt"),header = FALSE)
subject_test <- read.table(file.path(pathdata, "test", "subject_test.txt"),header = FALSE)

features <- read.table(file.path(pathdata, "features.txt"),header = FALSE)

activityLabels <- read.table(file.path(pathdata, "activity_labels.txt"),header = FALSE)

```

Rename the name of the column. The column names for x_train and x_test are stored in a dataset features.

```r
colnames(x_train) <- features[,2]
colnames(x_test) <- features[,2]

colnames(y_train) <- "activityID"
colnames(subject_train) <- "subjectID"

colnames(y_test) <- "activityID"
colnames(subject_test) <- "subjectID"

colnames(activityLabels) <- c("activityID", "activityType")
```
Merge training data and testing data

```r
train <- cbind(x_train, subject_train, y_train)
test <- cbind(x_test, subject_test, y_test)
data <- rbind(train, test)
```
Let's take the names of the columns already from dataset data

```r
cnames <- colnames(data)
```
Extracts only the measurements on the mean and standard deviation for each measurement. 
```r
data_for_mean_std <- (grepl("activityID" , cnames) | grepl("subjectID" , cnames) | grepl("mean.." , cnames) | grepl("std.." , cnames))
dataMean_Std <- data[, data_for_mean_std == T] 
```
Appropriately labels the data set with descriptive variable names.
```r
dataActivity <- merge(dataMean_Std, activityLabels, by = 'activityID', all.x = T)
tidySet <- aggregate(. ~subjectID + activityID, dataActivity, mean)
tidySet <- tidySet[order(tidySet$subjectID, tidySet$activityID),]
```
Write the received data to a file TidySet.txt
```r
write.table(tidySet, "TidySet.txt", row.name = F)
```
##### Tidy data
[TidySet](https://github.com/AlexBowsunowski/GettingAndCleaningDataCourseProject/blob/main/TidySet.txt)
