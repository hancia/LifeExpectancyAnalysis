---
title: "Life Expectancy Analysis"
---




```r
library(plotly)
```



```r
set.seed(0)
```


```r
data <- read.csv("Life_Expectancy_Data.csv")
head(data)
```

```
##       Country Year     Status Life.expectancy Adult.Mortality infant.deaths Alcohol percentage.expenditure Hepatitis.B Measles  BMI under.five.deaths Polio Total.expenditure Diphtheria HIV.AIDS
## 1 Afghanistan 2015 Developing            65.0             263            62    0.01              71.279624          65    1154 19.1                83     6              8.16         65      0.1
## 2 Afghanistan 2014 Developing            59.9             271            64    0.01              73.523582          62     492 18.6                86    58              8.18         62      0.1
## 3 Afghanistan 2013 Developing            59.9             268            66    0.01              73.219243          64     430 18.1                89    62              8.13         64      0.1
## 4 Afghanistan 2012 Developing            59.5             272            69    0.01              78.184215          67    2787 17.6                93    67              8.52         67      0.1
## 5 Afghanistan 2011 Developing            59.2             275            71    0.01               7.097109          68    3013 17.2                97    68              7.87         68      0.1
## 6 Afghanistan 2010 Developing            58.8             279            74    0.01              79.679367          66    1989 16.7               102    66              9.20         66      0.1
##         GDP Population thinness..1.19.years thinness.5.9.years Income.composition.of.resources Schooling
## 1 584.25921   33736494                 17.2               17.3                           0.479      10.1
## 2 612.69651     327582                 17.5               17.5                           0.476      10.0
## 3 631.74498   31731688                 17.7               17.7                           0.470       9.9
## 4 669.95900    3696958                 17.9               18.0                           0.463       9.8
## 5  63.53723    2978599                 18.2               18.2                           0.454       9.5
## 6 553.32894    2883167                 18.4               18.4                           0.448       9.2
```



```r
nrow(data)
```

```
## [1] 2938
```

```r
summary(data)
```

```
##    Country               Year         Status          Life.expectancy Adult.Mortality infant.deaths       Alcohol        percentage.expenditure  Hepatitis.B       Measles              BMI       
##  Length:2938        Min.   :2000   Length:2938        Min.   :36.30   Min.   :  1.0   Min.   :   0.0   Min.   : 0.0100   Min.   :    0.000      Min.   : 1.00   Min.   :     0.0   Min.   : 1.00  
##  Class :character   1st Qu.:2004   Class :character   1st Qu.:63.10   1st Qu.: 74.0   1st Qu.:   0.0   1st Qu.: 0.8775   1st Qu.:    4.685      1st Qu.:77.00   1st Qu.:     0.0   1st Qu.:19.30  
##  Mode  :character   Median :2008   Mode  :character   Median :72.10   Median :144.0   Median :   3.0   Median : 3.7550   Median :   64.913      Median :92.00   Median :    17.0   Median :43.50  
##                     Mean   :2008                      Mean   :69.22   Mean   :164.8   Mean   :  30.3   Mean   : 4.6029   Mean   :  738.251      Mean   :80.94   Mean   :  2419.6   Mean   :38.32  
##                     3rd Qu.:2012                      3rd Qu.:75.70   3rd Qu.:228.0   3rd Qu.:  22.0   3rd Qu.: 7.7025   3rd Qu.:  441.534      3rd Qu.:97.00   3rd Qu.:   360.2   3rd Qu.:56.20  
##                     Max.   :2015                      Max.   :89.00   Max.   :723.0   Max.   :1800.0   Max.   :17.8700   Max.   :19479.912      Max.   :99.00   Max.   :212183.0   Max.   :87.30  
##                                                       NA's   :10      NA's   :10                       NA's   :194                              NA's   :553                        NA's   :34     
##  under.five.deaths     Polio       Total.expenditure   Diphtheria       HIV.AIDS           GDP              Population        thinness..1.19.years thinness.5.9.years
##  Min.   :   0.00   Min.   : 3.00   Min.   : 0.370    Min.   : 2.00   Min.   : 0.100   Min.   :     1.68   Min.   :3.400e+01   Min.   : 0.10        Min.   : 0.10     
##  1st Qu.:   0.00   1st Qu.:78.00   1st Qu.: 4.260    1st Qu.:78.00   1st Qu.: 0.100   1st Qu.:   463.94   1st Qu.:1.958e+05   1st Qu.: 1.60        1st Qu.: 1.50     
##  Median :   4.00   Median :93.00   Median : 5.755    Median :93.00   Median : 0.100   Median :  1766.95   Median :1.387e+06   Median : 3.30        Median : 3.30     
##  Mean   :  42.04   Mean   :82.55   Mean   : 5.938    Mean   :82.32   Mean   : 1.742   Mean   :  7483.16   Mean   :1.275e+07   Mean   : 4.84        Mean   : 4.87     
##  3rd Qu.:  28.00   3rd Qu.:97.00   3rd Qu.: 7.492    3rd Qu.:97.00   3rd Qu.: 0.800   3rd Qu.:  5910.81   3rd Qu.:7.420e+06   3rd Qu.: 7.20        3rd Qu.: 7.20     
##  Max.   :2500.00   Max.   :99.00   Max.   :17.600    Max.   :99.00   Max.   :50.600   Max.   :119172.74   Max.   :1.294e+09   Max.   :27.70        Max.   :28.60     
##                    NA's   :19      NA's   :226       NA's   :19                       NA's   :448         NA's   :652         NA's   :34           NA's   :34        
##  Income.composition.of.resources   Schooling    
##  Min.   :0.0000                  Min.   : 0.00  
##  1st Qu.:0.4930                  1st Qu.:10.10  
##  Median :0.6770                  Median :12.30  
##  Mean   :0.6276                  Mean   :11.99  
##  3rd Qu.:0.7790                  3rd Qu.:14.30  
##  Max.   :0.9480                  Max.   :20.70  
##  NA's   :167                     NA's   :163
```


```r
data_new <- data[complete.cases(data[ , 'Life.expectancy']),]
```


```r
na_columns <- list("Alcohol", "Hepatitis.B", "BMI", "Polio", "Total.expenditure", "Diphtheria", "GDP", "Population", "thinness..1.19.years", "thinness.5.9.years", "Income.composition.of.resources", "Schooling")

for (col in na_columns){
    m <- median(data_new[ , col], na.rm=TRUE)
    print(col)
    print(m)
    data_new[ , col][is.na(data_new[ , col])] <- m
}
```

```
## [1] "Alcohol"
## [1] 3.77
## [1] "Hepatitis.B"
## [1] 92
## [1] "BMI"
## [1] 43.35
## [1] "Polio"
## [1] 93
## [1] "Total.expenditure"
## [1] 5.75
## [1] "Diphtheria"
## [1] 93
## [1] "GDP"
## [1] 1764.974
## [1] "Population"
## [1] 1391757
## [1] "thinness..1.19.years"
## [1] 3.3
## [1] "thinness.5.9.years"
## [1] 3.4
## [1] "Income.composition.of.resources"
## [1] 0.677
## [1] "Schooling"
## [1] 12.3
```



```r
fig <- plot_ly(y = data_new[, "Alcohol"], type = "box", quartilemethod="exclusive")

fig
```

![plot of chunk unnamed-chunk-8](figure/unnamed-chunk-8-1.png)
