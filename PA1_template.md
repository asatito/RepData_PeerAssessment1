---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---


## Loading and preprocessing the data

1. Load the Data


```r
unzip("activity.zip")
data <- read.csv("activity.csv")
```

2. Process/transform the data (if necessary) into a format suitable for your analysis


```r
dates <- as.Date(data$date, "%Y-%m-%d")
data$date <- dates 
```

## What is mean total number of steps taken per day?

1. Calculate the total number of steps taken per day


```r
library(dplyr)
group_data = data %>% group_by(date)  
TotalStepsPerDay=summarize(group_data, totalSteps=sum(steps,na.rm=TRUE))
as.data.frame(TotalStepsPerDay)
```

```
##          date totalSteps
## 1  2012-10-01          0
## 2  2012-10-02        126
## 3  2012-10-03      11352
## 4  2012-10-04      12116
## 5  2012-10-05      13294
## 6  2012-10-06      15420
## 7  2012-10-07      11015
## 8  2012-10-08          0
## 9  2012-10-09      12811
## 10 2012-10-10       9900
## 11 2012-10-11      10304
## 12 2012-10-12      17382
## 13 2012-10-13      12426
## 14 2012-10-14      15098
## 15 2012-10-15      10139
## 16 2012-10-16      15084
## 17 2012-10-17      13452
## 18 2012-10-18      10056
## 19 2012-10-19      11829
## 20 2012-10-20      10395
## 21 2012-10-21       8821
## 22 2012-10-22      13460
## 23 2012-10-23       8918
## 24 2012-10-24       8355
## 25 2012-10-25       2492
## 26 2012-10-26       6778
## 27 2012-10-27      10119
## 28 2012-10-28      11458
## 29 2012-10-29       5018
## 30 2012-10-30       9819
## 31 2012-10-31      15414
## 32 2012-11-01          0
## 33 2012-11-02      10600
## 34 2012-11-03      10571
## 35 2012-11-04          0
## 36 2012-11-05      10439
## 37 2012-11-06       8334
## 38 2012-11-07      12883
## 39 2012-11-08       3219
## 40 2012-11-09          0
## 41 2012-11-10          0
## 42 2012-11-11      12608
## 43 2012-11-12      10765
## 44 2012-11-13       7336
## 45 2012-11-14          0
## 46 2012-11-15         41
## 47 2012-11-16       5441
## 48 2012-11-17      14339
## 49 2012-11-18      15110
## 50 2012-11-19       8841
## 51 2012-11-20       4472
## 52 2012-11-21      12787
## 53 2012-11-22      20427
## 54 2012-11-23      21194
## 55 2012-11-24      14478
## 56 2012-11-25      11834
## 57 2012-11-26      11162
## 58 2012-11-27      13646
## 59 2012-11-28      10183
## 60 2012-11-29       7047
## 61 2012-11-30          0
```

2. Histogram of the total number of steps taken each day


```r
library(ggplot2)
qplot(TotalStepsPerDay$totalSteps, geom="histogram",
      binwidth=1000,
      xlab="Total number of steps taken each day")
```

![plot of chunk hist_steps_per_day](figure/hist_steps_per_day-1.png) 

3. Calculate and report the mean and median of the total number of steps taken per day.


   Mean steps per day:

```r
MeanStepsPerDay=summarize(group_data, meanSteps=mean(steps,na.rm=TRUE))
as.data.frame(MeanStepsPerDay)
```

```
##          date  meanSteps
## 1  2012-10-01        NaN
## 2  2012-10-02  0.4375000
## 3  2012-10-03 39.4166667
## 4  2012-10-04 42.0694444
## 5  2012-10-05 46.1597222
## 6  2012-10-06 53.5416667
## 7  2012-10-07 38.2465278
## 8  2012-10-08        NaN
## 9  2012-10-09 44.4826389
## 10 2012-10-10 34.3750000
## 11 2012-10-11 35.7777778
## 12 2012-10-12 60.3541667
## 13 2012-10-13 43.1458333
## 14 2012-10-14 52.4236111
## 15 2012-10-15 35.2048611
## 16 2012-10-16 52.3750000
## 17 2012-10-17 46.7083333
## 18 2012-10-18 34.9166667
## 19 2012-10-19 41.0729167
## 20 2012-10-20 36.0937500
## 21 2012-10-21 30.6284722
## 22 2012-10-22 46.7361111
## 23 2012-10-23 30.9652778
## 24 2012-10-24 29.0104167
## 25 2012-10-25  8.6527778
## 26 2012-10-26 23.5347222
## 27 2012-10-27 35.1354167
## 28 2012-10-28 39.7847222
## 29 2012-10-29 17.4236111
## 30 2012-10-30 34.0937500
## 31 2012-10-31 53.5208333
## 32 2012-11-01        NaN
## 33 2012-11-02 36.8055556
## 34 2012-11-03 36.7048611
## 35 2012-11-04        NaN
## 36 2012-11-05 36.2465278
## 37 2012-11-06 28.9375000
## 38 2012-11-07 44.7326389
## 39 2012-11-08 11.1770833
## 40 2012-11-09        NaN
## 41 2012-11-10        NaN
## 42 2012-11-11 43.7777778
## 43 2012-11-12 37.3784722
## 44 2012-11-13 25.4722222
## 45 2012-11-14        NaN
## 46 2012-11-15  0.1423611
## 47 2012-11-16 18.8923611
## 48 2012-11-17 49.7881944
## 49 2012-11-18 52.4652778
## 50 2012-11-19 30.6979167
## 51 2012-11-20 15.5277778
## 52 2012-11-21 44.3993056
## 53 2012-11-22 70.9270833
## 54 2012-11-23 73.5902778
## 55 2012-11-24 50.2708333
## 56 2012-11-25 41.0902778
## 57 2012-11-26 38.7569444
## 58 2012-11-27 47.3819444
## 59 2012-11-28 35.3576389
## 60 2012-11-29 24.4687500
## 61 2012-11-30        NaN
```


   Median steps per day:

```r
MedianStepsPerDay=summarize(group_data, medianSteps=median(steps,na.rm=TRUE))
as.data.frame(MedianStepsPerDay)
```

```
##          date medianSteps
## 1  2012-10-01          NA
## 2  2012-10-02           0
## 3  2012-10-03           0
## 4  2012-10-04           0
## 5  2012-10-05           0
## 6  2012-10-06           0
## 7  2012-10-07           0
## 8  2012-10-08          NA
## 9  2012-10-09           0
## 10 2012-10-10           0
## 11 2012-10-11           0
## 12 2012-10-12           0
## 13 2012-10-13           0
## 14 2012-10-14           0
## 15 2012-10-15           0
## 16 2012-10-16           0
## 17 2012-10-17           0
## 18 2012-10-18           0
## 19 2012-10-19           0
## 20 2012-10-20           0
## 21 2012-10-21           0
## 22 2012-10-22           0
## 23 2012-10-23           0
## 24 2012-10-24           0
## 25 2012-10-25           0
## 26 2012-10-26           0
## 27 2012-10-27           0
## 28 2012-10-28           0
## 29 2012-10-29           0
## 30 2012-10-30           0
## 31 2012-10-31           0
## 32 2012-11-01          NA
## 33 2012-11-02           0
## 34 2012-11-03           0
## 35 2012-11-04          NA
## 36 2012-11-05           0
## 37 2012-11-06           0
## 38 2012-11-07           0
## 39 2012-11-08           0
## 40 2012-11-09          NA
## 41 2012-11-10          NA
## 42 2012-11-11           0
## 43 2012-11-12           0
## 44 2012-11-13           0
## 45 2012-11-14          NA
## 46 2012-11-15           0
## 47 2012-11-16           0
## 48 2012-11-17           0
## 49 2012-11-18           0
## 50 2012-11-19           0
## 51 2012-11-20           0
## 52 2012-11-21           0
## 53 2012-11-22           0
## 54 2012-11-23           0
## 55 2012-11-24           0
## 56 2012-11-25           0
## 57 2012-11-26           0
## 58 2012-11-27           0
## 59 2012-11-28           0
## 60 2012-11-29           0
## 61 2012-11-30          NA
```
## What is the average daily activity pattern?

1. Time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and 
   the average number of steps taken, averaged across all days (y-axis)
   

```r
group_data_interval = group_by(data,interval)
mean_steps_interval = summarize(group_data_interval,
                                meanStepsAtInterval=mean(steps,na.rm=TRUE)
                                )
with(mean_steps_interval,plot(interval,
                              meanStepsAtInterval,
                              type="l",
                              main="Average daily activity pattern", 
                              xlab="Interval", 
                              ylab="Mean steps per interval"
     ))
```

![plot of chunk activity_pattern](figure/activity_pattern-1.png) 

2. Which 5-minute interval, on average across all the days in the dataset, 
contains the maximum number of steps?


```r
max_steps_interval = max(mean_steps_interval$meanStepsAtInterval)
max_interval = mean_steps_interval[mean_steps_interval$meanStepsAtInterval 
                                   == max_steps_interval,
                                   c("interval")
                                  ]
as.numeric(max_interval)
```

```
## [1] 835
```

## Imputing missing values

1. Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)


```r
IsComplete <- complete.cases(data$steps)
naRows = sum(as.numeric(!IsComplete))
naRows
```

```
## [1] 2304
```

2. Strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.


```r
fillFunc = function(steps, interval) {
    if (!is.na(steps))
        fillFunc = steps
    else
        fillFunc<- (as.numeric(mean_steps_interval[mean_steps_interval$interval==interval,c("meanStepsAtInterval")]))
}
```

3. Creating a new dataset that is equal to the original dataset but with the missing data filled in.


```r
c_data = data
c_data$steps <- mapply(fillFunc, c_data$steps, c_data$interval)
```

4. Make a histogram of the total number of steps taken each day and Calculate 
and report the mean and median total number of steps taken per day. Do these 
values differ from the estimates from the first part of the assignment? What 
is the impact of imputing missing data on the estimates of the total daily 
number of steps?

Histogram of Daily Steps



```r
group_data_daily = c_data %>% group_by(date)  
TotalDailyStep=summarize(group_data_daily, totalSteps_Fill=sum(steps,na.rm=TRUE))
qplot(TotalDailyStep$totalSteps_Fill, geom="histogram",
      binwidth=1000,
      xlab="Total number of steps taken each day")
```

![plot of chunk amissing_4_h](figure/amissing_4_h-1.png) 



Mean Daily steps


```r
MeanDailyStep = summarize(group_data_daily, meanSteps_Fill=mean(steps,na.rm=TRUE))
as.data.frame(MeanDailyStep)
```

```
##          date meanSteps_Fill
## 1  2012-10-01     37.3825996
## 2  2012-10-02      0.4375000
## 3  2012-10-03     39.4166667
## 4  2012-10-04     42.0694444
## 5  2012-10-05     46.1597222
## 6  2012-10-06     53.5416667
## 7  2012-10-07     38.2465278
## 8  2012-10-08     37.3825996
## 9  2012-10-09     44.4826389
## 10 2012-10-10     34.3750000
## 11 2012-10-11     35.7777778
## 12 2012-10-12     60.3541667
## 13 2012-10-13     43.1458333
## 14 2012-10-14     52.4236111
## 15 2012-10-15     35.2048611
## 16 2012-10-16     52.3750000
## 17 2012-10-17     46.7083333
## 18 2012-10-18     34.9166667
## 19 2012-10-19     41.0729167
## 20 2012-10-20     36.0937500
## 21 2012-10-21     30.6284722
## 22 2012-10-22     46.7361111
## 23 2012-10-23     30.9652778
## 24 2012-10-24     29.0104167
## 25 2012-10-25      8.6527778
## 26 2012-10-26     23.5347222
## 27 2012-10-27     35.1354167
## 28 2012-10-28     39.7847222
## 29 2012-10-29     17.4236111
## 30 2012-10-30     34.0937500
## 31 2012-10-31     53.5208333
## 32 2012-11-01     37.3825996
## 33 2012-11-02     36.8055556
## 34 2012-11-03     36.7048611
## 35 2012-11-04     37.3825996
## 36 2012-11-05     36.2465278
## 37 2012-11-06     28.9375000
## 38 2012-11-07     44.7326389
## 39 2012-11-08     11.1770833
## 40 2012-11-09     37.3825996
## 41 2012-11-10     37.3825996
## 42 2012-11-11     43.7777778
## 43 2012-11-12     37.3784722
## 44 2012-11-13     25.4722222
## 45 2012-11-14     37.3825996
## 46 2012-11-15      0.1423611
## 47 2012-11-16     18.8923611
## 48 2012-11-17     49.7881944
## 49 2012-11-18     52.4652778
## 50 2012-11-19     30.6979167
## 51 2012-11-20     15.5277778
## 52 2012-11-21     44.3993056
## 53 2012-11-22     70.9270833
## 54 2012-11-23     73.5902778
## 55 2012-11-24     50.2708333
## 56 2012-11-25     41.0902778
## 57 2012-11-26     38.7569444
## 58 2012-11-27     47.3819444
## 59 2012-11-28     35.3576389
## 60 2012-11-29     24.4687500
## 61 2012-11-30     37.3825996
```

Median Daily Steps


```r
MedianDailyStep = summarize(group_data_daily, medianSteps_Fill=median(steps,na.rm=TRUE))
as.data.frame(MedianDailyStep)
```

```
##          date medianSteps_Fill
## 1  2012-10-01         34.11321
## 2  2012-10-02          0.00000
## 3  2012-10-03          0.00000
## 4  2012-10-04          0.00000
## 5  2012-10-05          0.00000
## 6  2012-10-06          0.00000
## 7  2012-10-07          0.00000
## 8  2012-10-08         34.11321
## 9  2012-10-09          0.00000
## 10 2012-10-10          0.00000
## 11 2012-10-11          0.00000
## 12 2012-10-12          0.00000
## 13 2012-10-13          0.00000
## 14 2012-10-14          0.00000
## 15 2012-10-15          0.00000
## 16 2012-10-16          0.00000
## 17 2012-10-17          0.00000
## 18 2012-10-18          0.00000
## 19 2012-10-19          0.00000
## 20 2012-10-20          0.00000
## 21 2012-10-21          0.00000
## 22 2012-10-22          0.00000
## 23 2012-10-23          0.00000
## 24 2012-10-24          0.00000
## 25 2012-10-25          0.00000
## 26 2012-10-26          0.00000
## 27 2012-10-27          0.00000
## 28 2012-10-28          0.00000
## 29 2012-10-29          0.00000
## 30 2012-10-30          0.00000
## 31 2012-10-31          0.00000
## 32 2012-11-01         34.11321
## 33 2012-11-02          0.00000
## 34 2012-11-03          0.00000
## 35 2012-11-04         34.11321
## 36 2012-11-05          0.00000
## 37 2012-11-06          0.00000
## 38 2012-11-07          0.00000
## 39 2012-11-08          0.00000
## 40 2012-11-09         34.11321
## 41 2012-11-10         34.11321
## 42 2012-11-11          0.00000
## 43 2012-11-12          0.00000
## 44 2012-11-13          0.00000
## 45 2012-11-14         34.11321
## 46 2012-11-15          0.00000
## 47 2012-11-16          0.00000
## 48 2012-11-17          0.00000
## 49 2012-11-18          0.00000
## 50 2012-11-19          0.00000
## 51 2012-11-20          0.00000
## 52 2012-11-21          0.00000
## 53 2012-11-22          0.00000
## 54 2012-11-23          0.00000
## 55 2012-11-24          0.00000
## 56 2012-11-25          0.00000
## 57 2012-11-26          0.00000
## 58 2012-11-27          0.00000
## 59 2012-11-28          0.00000
## 60 2012-11-29          0.00000
## 61 2012-11-30         34.11321
```


After inputting the missing values the mean remains either remained the same or increased. Total Number of Daily steps remained the same for days which had no missing values. For days with missing values the total steps now increase as we have populated them with the mean values of the interval.


## Are there differences in activity patterns between weekdays and weekends?

1. Create a new factor variable in the dataset with two levels - "weekday" and "weekend" indicating whether a given date is a weekday or weekend day.


```r
cdata_2 = mutate ( c_data, w_wend=factor(ifelse(weekdays(date) 
                %in% c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday"),
                "weekday","weekend"))
                 )
```

2. Make a panel plot containing a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis). See the README file in the GitHub repository to see an example of what this plot should look like using simulated data.


```r
mean_w <- aggregate(steps ~ interval + w_wend, data=cdata_2, mean)
ggplot(mean_w, aes(interval, steps)) + geom_line() + facet_grid(w_wend ~ .) +
    xlab("5-minute interval") + ylab("Number of steps")
```

![plot of chunk 5_2](figure/5_2-1.png) 

