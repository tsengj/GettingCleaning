# Code Book

This code book describes variables, data, and any transformations or work performed to clean up the data. These efforts resulted into a clean and tidy dataset - please see tidy_data.txt and tidy_data.csv.

# Data Source Details

* Original data: https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip
* Information provided by the authors: http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

# Dataset Description

Full details and explanations can be found in 'README.txt' in the ZIP file containing the original data source.

# Quick facts

* The experiments involved a group of 30 volunteers (19 - 48 years of age)
* Each person performed six activities while wearing a smartphone (Samsung Galaxy S II) on their waist
* The activities consisted of three types of walking (flat, upstairs and downstairs), sitting, standing and laying
* The experiments have been video recorded (YouTube)

# Data Partitioning

The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data.

# Measurements

The following sensor signals were captured using the smartphone's embedded accelerometer and gyroscope:

* three-axial linear acceleration
* three-axial angular velocity at a constant rate of 50Hz
The captured signals were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). From each window, a vector of features was obtained by calculating variables from the time and frequency domain. See the section 'Feature Selection' below, also the file 'features_info.txt' has complete details.

# Feature Selection

* The features selected for this database come from the accelerometer and gyroscope three-axial raw signals tAcc-XYZ and tGyro-XYZ.

* The time domain signals were captured at a constant rate of 50 Hz, prefix 't' denotes time
* The signals were then filtered to remove noise
* The accelaration signal was separated into body and gravity acceleration signals:
** tBodyAcc-XYZ
** tGravityAcc-XYZ
* Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals:
** tBodyAccJerk-XYZ
** tBodyGyroJerk-XYZ
* Next, the magnitude of these three-dimensional signals were calculated using the Euclidean form:
** tBodyAccMag
** tGravityAccMag
** tBodyAccJerkMag
** tBodyGyroMag
** tBodyGyroJerkMag
* Finally a Fast Fourier Transform (FFT) was applied to some of these signals, prefix 'f' indicates frequency domain signals:
** fBodyAcc-XYZ
** fBodyAccJerk-XYZ
** fBodyGyro-XYZ
** fBodyAccJerkMag
** fBodyGyroMag
** fBodyGyroJerkMag

That leaves us with the following set of signals, suffix '-XYZ' denotes three-axial signals in the X, Y and Z directions:

** tBodyAcc-XYZ
** tGravityAcc-XYZ
** tBodyAccJerk-XYZ
** tBodyGyro-XYZ
** tBodyGyroJerk-XYZ
** tBodyAccMag
** tGravityAccMag
** tBodyAccJerkMag
** tBodyGyroMag
** tBodyGyroJerkMag
** fBodyAcc-XYZ
** fBodyAccJerk-XYZ
** fBodyGyro-XYZ
** fBodyAccMag
** fBodyAccJerkMag
** fBodyGyroMag
** fBodyGyroJerkMag

The features were further combined with a variety of estimated variables, such as mean value, standard deviation, largest and smallest value in the set etc. This adds up to over 550 of different indicators in total. The file 'features.txt' lists all of the variables.

# Transformations

As stipulated by the requirements the following transformations were made to keep the resulting output clean and tidy:

* The training and the test sets have been merged to form a single data set
* Out of the broad spectrum of features only the measurements on the mean and standard deviation were considered
* Descriptive activity names and labels were used appropriately to increase data readability
* A separate tidy dataset was created as the final step of data refinement efforts
In addition to the aforementioned mandatory transformations, the feature names have been amended to adhere to naming standards of the R language. That allowed for an elegant use of R languague features, such as column name filtering, and an increased code readability. I consider this additional transformation a minor change, which I believe doesn't have an adverse impact on the original information.

Feature name adjustment example:

* 'tBodyAcc-mean()-X' has been changed to 'tBodyAcc_mean_X'
* 'tBodyAcc-std()-Z' has been changed to 'tBodyAcc_std_Z'
* etc.
The transformations are achieved by the script called run_analysis.R, which:

* Ensures that all non-standard R packages (dplyr, reshape2) are installed
* Defines a number of helper functions to promote code reuse
* Downloads the original dataset and verifies its content
* Loads activity and label names datasets
* Loads training and test datasets and enhances column names with appropriate labels
* Merges the testing and the test datasets using dplyr's support for method chaining (pipe operator)
* Creates an independent tidy dataset based on mean and standard deviations
* Saves the tidy dataset as tidy_data.txt and tidy_data.csv so that it can be easily imported and viewed