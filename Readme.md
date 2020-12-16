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
##    Country               Year         Status          Life.expectancy Adult.Mortality infant.deaths       Alcohol        percentage.expenditure  Hepatitis.B       Measles        
##  Length:2938        Min.   :2000   Length:2938        Min.   :36.30   Min.   :  1.0   Min.   :   0.0   Min.   : 0.0100   Min.   :    0.000      Min.   : 1.00   Min.   :     0.0  
##  Class :character   1st Qu.:2004   Class :character   1st Qu.:63.10   1st Qu.: 74.0   1st Qu.:   0.0   1st Qu.: 0.8775   1st Qu.:    4.685      1st Qu.:77.00   1st Qu.:     0.0  
##  Mode  :character   Median :2008   Mode  :character   Median :72.10   Median :144.0   Median :   3.0   Median : 3.7550   Median :   64.913      Median :92.00   Median :    17.0  
##                     Mean   :2008                      Mean   :69.22   Mean   :164.8   Mean   :  30.3   Mean   : 4.6029   Mean   :  738.251      Mean   :80.94   Mean   :  2419.6  
##                     3rd Qu.:2012                      3rd Qu.:75.70   3rd Qu.:228.0   3rd Qu.:  22.0   3rd Qu.: 7.7025   3rd Qu.:  441.534      3rd Qu.:97.00   3rd Qu.:   360.2  
##                     Max.   :2015                      Max.   :89.00   Max.   :723.0   Max.   :1800.0   Max.   :17.8700   Max.   :19479.912      Max.   :99.00   Max.   :212183.0  
##                                                       NA's   :10      NA's   :10                       NA's   :194                              NA's   :553                       
##       BMI        under.five.deaths     Polio       Total.expenditure   Diphtheria       HIV.AIDS           GDP              Population        thinness..1.19.years thinness.5.9.years
##  Min.   : 1.00   Min.   :   0.00   Min.   : 3.00   Min.   : 0.370    Min.   : 2.00   Min.   : 0.100   Min.   :     1.68   Min.   :3.400e+01   Min.   : 0.10        Min.   : 0.10     
##  1st Qu.:19.30   1st Qu.:   0.00   1st Qu.:78.00   1st Qu.: 4.260    1st Qu.:78.00   1st Qu.: 0.100   1st Qu.:   463.94   1st Qu.:1.958e+05   1st Qu.: 1.60        1st Qu.: 1.50     
##  Median :43.50   Median :   4.00   Median :93.00   Median : 5.755    Median :93.00   Median : 0.100   Median :  1766.95   Median :1.387e+06   Median : 3.30        Median : 3.30     
##  Mean   :38.32   Mean   :  42.04   Mean   :82.55   Mean   : 5.938    Mean   :82.32   Mean   : 1.742   Mean   :  7483.16   Mean   :1.275e+07   Mean   : 4.84        Mean   : 4.87     
##  3rd Qu.:56.20   3rd Qu.:  28.00   3rd Qu.:97.00   3rd Qu.: 7.492    3rd Qu.:97.00   3rd Qu.: 0.800   3rd Qu.:  5910.81   3rd Qu.:7.420e+06   3rd Qu.: 7.20        3rd Qu.: 7.20     
##  Max.   :87.30   Max.   :2500.00   Max.   :99.00   Max.   :17.600    Max.   :99.00   Max.   :50.600   Max.   :119172.74   Max.   :1.294e+09   Max.   :27.70        Max.   :28.60     
##  NA's   :34                        NA's   :19      NA's   :226       NA's   :19                       NA's   :448         NA's   :652         NA's   :34           NA's   :34        
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

![plot of chunk unnamed-chunk-9](figure/unnamed-chunk-9-1.png)
