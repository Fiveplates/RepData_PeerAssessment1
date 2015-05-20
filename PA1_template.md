# Reproducible Research: Peer Assessment 1
 

```r
library(knitr)
opts_chunk$set(fig.path="figure/")
```
 
## Loading and preprocessing the data

### Data

The data for this assignment can be downloaded from the course web site:

* Dataset: [Activity monitoring data][1] [52K]

The variables included in this dataset are:

* steps: Number of steps taking in a 5-minute interval (missing values are coded as NA)  
* date: The date on which the measurement was taken in YYYY-MM-DD format  
* interval: Identifier for the 5-minute interval in which measurement was taken  

The dataset is stored in a comma-separated-value (CSV) file and there are a total of 17,568 observations in this dataset.

### Loading the activity monitoring data


```r
ActivityData <- read.csv(file = "./data/activity.csv", stringsAsFactors = FALSE)

summary(ActivityData)
```

```
##      steps            date              interval     
##  Min.   :  0.00   Length:17568       Min.   :   0.0  
##  1st Qu.:  0.00   Class :character   1st Qu.: 588.8  
##  Median :  0.00   Mode  :character   Median :1177.5  
##  Mean   : 37.38                      Mean   :1177.5  
##  3rd Qu.: 12.00                      3rd Qu.:1766.2  
##  Max.   :806.00                      Max.   :2355.0  
##  NA's   :2304
```

```r
str(ActivityData)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : chr  "2012-10-01" "2012-10-01" "2012-10-01" "2012-10-01" ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```

### Processing the activity monitoring data

The date variable in the Activity Monitoring Data is loaded from the csv file as character (chr), convert to a date (Date) format


```r
ActivityData$date <- as.Date(ActivityData$date, format = "%Y-%m-%d")
```


## What is mean total number of steps taken per day?

### Calculate the total number of steps taken per day


```r
StepsPerDay <- aggregate(ActivityData$steps, by = list(ActivityData$date), FUN = sum, na.rm = TRUE)

library(data.table)
### Set the column names
setnames(StepsPerDay, c("date", "steps"))
```

### Histogram of the total number of steps taken per day


```r
hist(StepsPerDay$steps, col = "red", main = "Total Number of Steps taken Each Day", xlab = "Steps")
```

![](figure/Histogram-1.png) 

### Calculate the mean and median of the total number of steps taken per day

```r
meanValue <- mean(StepsPerDay$steps)

medianValue <- median(StepsPerDay$steps)
```

The mean of the total number of steps taken per day is **9354.2295082**.  
The median of the total number of steps taken per day is **10395**.

## What is the average daily activity pattern?





## Imputing missing values

Note that there are a number of days/intervals where there are missing values (coded as **NA**). The presence of missing days may introduce bias into some calculations or summaries of the data.




## Are there differences in activity patterns between weekdays and weekends?

[1]: https://d396qusza40orc.cloudfront.net/repdata/data/activity.zip "Activity Monitoring Data"
