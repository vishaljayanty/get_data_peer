# get_data_peer

This repo contains my solution to the Getting and Cleaning Data Peer Assessment. This has been tested in windows 10 (local laptop) and it worked fine generating the tidy version of the file that has been attached.

Simply execute "run_analysis.R". The folders where the files needs to be created are - C:/Coursera/Data_Science_Course/Assignment4 and the unzip files are in C:/Coursera/Data_Science_Course/Assignment4/Unzip

If you already have downloaded the data, extract the zip file inside the same folder than the script. Just to be clear, the relative path compared to "run_analysis.R" of the "activity_labels.txt" file should be "UCI HAR Dataset/activity_labels.txt" for instance.

###There are some issues whilst sourcing the file or running ther knit command and this because of some issue with the dtplyr package as well as dtplyr package. Did some research and looks like this is an issue with the file character set. Apart from that the file runs fine.

#The exercise's description

The purpose of this project is to demonstrate your ability to collect, work with, and clean a data set. The goal is to prepare tidy data that can be used for later analysis. You will be graded by your peers on a series of yes/no questions related to the project. You will be required to submit: 1) a tidy data set as described below, 2) a link to a Github repository with your script for performing the analysis, and 3) a code book that describes the variables, the data, and any transformations or work that you performed to clean up the data called CodeBook.md. You should also include a README.md in the repo with your scripts. This repo explains how all of the scripts work and how they are connected.

One of the most exciting areas in all of data science right now is wearable computing - see for example this article . Companies like Fitbit, Nike, and Jawbone Up are racing to develop the most advanced algorithms to attract new users. The data linked to from the course website represent data collected from the accelerometers from the Samsung Galaxy S smartphone. A full description is available at the site where the data was obtained:

http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

Here are the data for the project:

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip

You should create one R script called run_analysis.R that does the following. Merges the training and the test sets to create one data set. Extracts only the measurements on the mean and standard deviation for each measurement. Uses descriptive activity names to name the activities in the data set Appropriately labels the data set with descriptive activity names. Creates a second, independent tidy data set with the average of each variable for each activity and each subject. Good luck!