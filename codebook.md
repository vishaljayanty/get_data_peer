No other transformations than the ones done in the script has been made on the data. The script merges many the different files, into one single dataset as it has been stated in the exercise (see readme for the exercise's description).

The input is described in the README.txt of the downloaded input (see "UCI HAR Dataset/README.txt" file once the input is downloaded).

The output represents the average of each variable for each activity and each subject. It is a table ; each variable is represented by a column, and each activity / subject is represented by a row. The columns names are slightly modified from the "features.txt" input file content. The code with the headings explains what was done

#library(data.table)

## dowload and unzip  file
url <- "http://archive.ics.uci.edu/ml/machine-learning-databases/00341/HAPT%20Data%20Set.zip"
setwd('C:/Coursera/Data_Science_Course/Assignment4')
if (!file.exists('C:/Coursera/Data_Science_Course/Assignment4/UCI HAR Dataset.zip')){
  download.file(url,'C:/Coursera/Data_Science_Course/Assignment4/UCI HAR Dataset.zip', mode = 'wb')
  unzip("UCI HAR Dataset.zip", exdir = 'C:/Coursera/Data_Science_Course/Assignment4/Unzip')
}

## setting workdir 
setwd('C:/Coursera/Data_Science_Course/Assignment4/Unzip')

## put the files into a data table
features <- read.csv('C:/Coursera/Data_Science_Course/Assignment4/Unzip/features.txt', header = FALSE)

## Training DataSets
data.train.features <- read.csv('C:/Coursera/Data_Science_Course/Assignment4/Unzip/Train/X_train.txt', header = FALSE, sep = ' ')
data.train.activity <- read.csv('C:/Coursera/Data_Science_Course/Assignment4/Unzip/Train/y_train.txt', header = FALSE, sep = ' ')
data.train.subject <- read.csv('C:/Coursera/Data_Science_Course/Assignment4/Unzip/Train/subject_id_train.txt',header = FALSE, sep = ' ')

## Test DataSets
data.test.features <- read.csv('C:/Coursera/Data_Science_Course/Assignment4/Unzip/Test/X_test.txt', header = FALSE, sep = ' ')
data.test.activity <- read.csv('C:/Coursera/Data_Science_Course/Assignment4/Unzip/Test/y_test.txt', header = FALSE, sep = ' ')
data.test.subject <- read.csv('C:/Coursera/Data_Science_Course/Assignment4/Unzip/Test/subject_id_test.txt', header = FALSE, sep = ' ')

## combining the data sets
data.subject <- rbind(data.train.subject, data.test.subject)
data.activity<- rbind(data.train.activity, data.test.activity)
data.features<- rbind(data.train.features, data.test.features)

## combine data sets
data.combine <- data.frame(data.subject, data.activity , data.features )

## column names
var <- as.character(features$V1)
names(data.combine) <- c(c('subject', 'activity'), var)

## extract data with mean or std in column names - grep or grepl did not work so dtplyr
##install.packages("dtplyr")
library(dtplyr)
sub.column.mean_interim_1 <- tbl_dt(data.combine) 
sub.column.mean_interim_2 <- select(sub.column.mean_interim_1,contains("mean"))
sub.column.mean <- names(sub.column.mean_interim_2)
sub.column.std_interim_2 <- select(sub.column.mean_interim_1,contains("std"))
sub.column.mean <- names(sub.column.mean_interim_2)
sub.column.std <- names(sub.column.std_interim_2)
sub.column <- unique(c("subject", "activity", sub.column.mean,sub.column.std))

## selecting subset of data
data.sub <- subset(data.combine,select=sub.column)

##reading activity names
activity.labels <- read.table('C:/Coursera/Data_Science_Course/Assignment4/Unzip/activity_labels.txt', header = FALSE)
activity.labels <- as.character(activity.labels[,2])
data.sub$activity <- activity.labels[data.sub$activity]
data.sub$activity <- activity.labels[data.combine$activity]

## cleaning up column names
names.new <- names(data.sub)
names.new <- gsub("^t", "TimeDomain_", names.new)
names.new <- gsub("^f", "FrequencyDomain_", names.new)
names(data.sub) <- names.new

## creating tidy data
Data2 <- aggregate(. ~subject + activity, data.sub, mean)
Data2 <- Data2[order(Data2$subject,Data2$activity),]

### writing to a file
write.table(Data2, file = "tidydata.txt",row.name=FALSE)