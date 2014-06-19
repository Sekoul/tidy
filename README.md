**run_analysis Explanation**
========================================================  

First, we open the necessary files and load them into variables:  

```{r}
#set workign directory
setwd("C:\\Users\\Sekoul\\Dropbox\\MISC\\Code\\Coursera\\GettingandClearningData\\CourseProject\\UCI HAR Dataset")

#open labels
labels <- read.table("activity_labels.txt", header=FALSE, stringsAsFactors = FALSE)
features <- read.table("features.txt", header=FALSE, stringsAsFactors = FALSE)

#open databases and store in variables
xtrain <- read.table("train\\X_train.txt", header=FALSE, stringsAsFactors = FALSE)
ytrain <- read.table("train\\y_train.txt", header=FALSE, stringsAsFactors = FALSE)
subtrain <- read.table("train\\subject_train.txt", header=FALSE, stringsAsFactors = FALSE)

xtest <- read.table("test\\X_test.txt", header=FALSE, stringsAsFactors = FALSE)
ytest <- read.table("test\\y_test.txt", header=FALSE, stringsAsFactors = FALSE)
subtest <- read.table("test\\subject_test.txt", header=FALSE, stringsAsFactors = FALSE)
```  


**Merges the training and the test sets to create one data set.**  

```{r}
# merge variables together to create whole dataset
sub <- rbind(subtest, subtrain)
y <- rbind(ytest, ytrain)
x <- rbind(xtest, xtrain)
```  

**Extracts only the measurements on the mean and standard deviation for each measurement.**  
AND  
**Appropriately labels the data set with descriptive variable names.**  
```{r}
# name the columns of X according to features list
colnames(x) <- features$V2

# take columns of x containg the mean
xmean <- subset(x, select = grepl("mean", colnames(x)))

# take columns of x containg the mean
xstd <- subset(x, select = grepl("std", colnames(x)))
```  



**Uses descriptive activity names to name the activities in the data set**  
```{r}
# Change activity numbers to tags and add to X
y$V1[y$V1==1] <- labels[1,2]
y$V1[y$V1==2] <- labels[2,2]
y$V1[y$V1==3] <- labels[3,2]
y$V1[y$V1==4] <- labels[4,2]
y$V1[y$V1==5] <- labels[5,2]
y$V1[y$V1==6] <- labels[6,2]


#change names of subject and activity column
colnames(sub)[1] <- "subject"
colnames(y)[1] <- "activity"

# combine xmean, xstd, subject and activity
xfinal <- cbind(xmean, xstd, sub, y)
```  

**Creates a second, independent tidy data set with the average of each variable for each activity and each subject. **  

```{r}


#makes tidy copy of the data above
namelist <- list(colnames(xmean))
xtidy <- cbind(xmean, sub, y)
xtidy <- data.frame(xtidy, stringsAsFactors = FALSE)
xtidyy <- melt(xtidy, id=c('subject', 'activity'))

#saves result as .txt file
write.table(xtidyy, "tidyData.txt")
```















