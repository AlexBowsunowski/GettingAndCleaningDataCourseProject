# README
##Getting and Cleaning Data course project

##Description of the program

### Download File
```r
x_train <- read.table(file.path(pathdata, "train", "X_train.txt"), header = F)
y_train <- read.table(file.path(pathdata, "train", "y_train.txt"),header = F)
subject_train <- read.table(file.path(pathdata, "train", "subject_train.txt"),header = F)

x_test = read.table(file.path(pathdata, "test", "X_test.txt"),header = FALSE)
y_test = read.table(file.path(pathdata, "test", "y_test.txt"),header = FALSE)
subject_test = read.table(file.path(pathdata, "test", "subject_test.txt"),header = FALSE)

features = read.table(file.path(pathdata, "features.txt"),header = FALSE)

activityLabels = read.table(file.path(pathdata, "activity_labels.txt"),header = FALSE)

```

###Rename the name of the column
```r
colnames(x_train) <- features[,2]
colnames(x_test) <- features[,2]

colnames(y_train) <- "activityID"
colnames(subject_train) <- "subjectID"

colnames(y_test) <- "activityID"
colnames(subject_test) <- "subjectID"

colnames(activityLabels) <- c("activityID", "activityType")
```
