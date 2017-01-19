Does Pollution Affect Mortality?
========================================================
author: Adam Glover
date: 1/6/17
autosize: true

Introduction
========================================================
Researchers at General Motors collected data on 60 U.S. Standard Metropolitan Statistical Areas (SMSA's) in a study of whether air pollution contributes to mortality.

I will attempt to use this dataset to answer the question, Does Pollition Affect Mortality? If not what does?


Summary of dataset
========================================================
The following are distributions of variables excluding polution variables

```r
mortality <- read.csv('/Users/ag/Desktop/mortality.csv')
par(mfrow=c(3,3))
hist(mortality$JanTemp, main= "Jan Temp")
hist(mortality$JulyTemp, main= "July Temp")
hist(mortality$RelHum, main= "Relative Humidity") 
hist(mortality$X.NonWhite, main = "Percentage of Nonwhites")
hist(mortality$Education, main = "Median Education")
hist(mortality$PopDensity, main = "Population Density")
hist(mortality$Rain, main = "Rain")
hist(mortality$X.WC, main = "Percentage of Whites Collar Workers")
hist(mortality$pop, main = "Population")
```

![plot of chunk unnamed-chunk-1](mortality-figure/unnamed-chunk-1-1.png)

Analysis of Dependent Variable - Age adjusted mortality
========================================================
The dependent variable is age adjusted mortality.

Age adjusting rates is a way to make fairer comparisons between groups with different age distributions.

- Low skewness and kurtosis values
- No need for transformation



```r
library('Hmisc')
library('psych')
mortality <- read.csv('/Users/ag/Desktop/mortality.csv')
hist(mortality$Mortality, main = "Age adjusted mortality")
```

![plot of chunk unnamed-chunk-2](mortality-figure/unnamed-chunk-2-1.png)

```r
describe(mortality$Mortality)
```

```
   vars  n   mean    sd median trimmed   mad    min     max  range skew
X1    1 60 940.35 62.22 943.68  940.04 65.66 790.73 1113.16 322.43 0.09
   kurtosis   se
X1    -0.05 8.03
```
Analysis of Independent Variables
========================================================
The independent variables include all pollution variables (HCPot, NOxPot, SO2Pot, NOx)

- High skewness and kurtosis values
- Require log transformations


```r
library('Hmisc')
library('psych')
mortality <- read.csv('/Users/ag/Desktop/mortality.csv')
par(mfrow=c(2,2))
hist(mortality$HCPot, main = "HC pollution potential")
hist(mortality$NOxPot, main = "Nitrous Oxide pollution potential")
hist(mortality$S02Pot, main = "Sulfur Dioxide pollution potential")
hist(mortality$NOx, main = "Nitous Oxide")
```

![plot of chunk unnamed-chunk-3](mortality-figure/unnamed-chunk-3-1.png)

```r
describe(mortality[14:17])
```

```
       vars  n  mean    sd median trimmed   mad min max range skew
HCPot     1 60 37.85 91.98   14.5   18.58 12.60   1 648   647 5.32
NOxPot    2 60 22.60 46.36    9.0   13.17  8.90   1 319   318 4.91
S02Pot    3 60 53.77 63.39   30.0   41.10 32.62   1 278   277 1.82
NOx       4 60 22.60 46.36    9.0   13.17  8.90   1 319   318 4.91
       kurtosis    se
HCPot     30.61 11.87
NOxPot    26.65  5.98
S02Pot     2.96  8.18
NOx       26.65  5.98
```

Log transformation for pollution variables 
========================================================

```r
mortality <- read.csv('/Users/ag/Desktop/mortality.csv')
par(mfrow=c(2,2))
hist(log(mortality$HCPot))
hist(log(mortality$NOxPot))
hist(log(mortality$S02Pot))
hist(log(mortality$NOx))
```

![plot of chunk unnamed-chunk-4](mortality-figure/unnamed-chunk-4-1.png)
Correlations
========================================================
Multicollinearity issues between HCPot, NOx, and NOxPot variables.

Unsure how multicollinearty affects predictions or rsquared if variables are used.

```r
library('corrplot')
mortality <- read.csv('/Users/ag/Desktop/mortality.csv')
correlation <- cor(mortality[,c("Education","HCPot","income","JanTemp","JulyTemp","Mortality","NOx","NOxPot","pop","pop.house","PopDensity","Rain","RelHum","S02Pot","X.NonWhite","X.WC")], use="complete")
corrplot(correlation)
```

![plot of chunk unnamed-chunk-5](mortality-figure/unnamed-chunk-5-1.png)
Modeling
========================================================
Procedure - Stepwise Backward Elimination Regression


```r
mortality <- read.csv('/Users/ag/Desktop/mortality.csv')
fit <- lm(Mortality ~ Education+JanTemp+Rain+log(mortality$X.NonWhite), data=mortality)
summary(fit)
```

```

Call:
lm(formula = Mortality ~ Education + JanTemp + Rain + log(mortality$X.NonWhite), 
    data = mortality)

Residuals:
    Min      1Q  Median      3Q     Max 
-92.338 -20.866   3.524  24.513 100.360 

Coefficients:
                           Estimate Std. Error t value Pr(>|t|)    
(Intercept)               1122.5996    89.9133  12.485  < 2e-16 ***
Education                  -24.1866     7.1961  -3.361  0.00142 ** 
JanTemp                     -1.6368     0.5838  -2.804  0.00696 ** 
Rain                         1.1430     0.5236   2.183  0.03332 *  
log(mortality$X.NonWhite)   43.9467     6.8117   6.452 2.97e-08 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 40.38 on 55 degrees of freedom
Multiple R-squared:  0.6074,	Adjusted R-squared:  0.5788 
F-statistic: 21.27 on 4 and 55 DF,  p-value: 1.208e-10
```

```r
plot(fit)
```

![plot of chunk unnamed-chunk-6](mortality-figure/unnamed-chunk-6-1.png)![plot of chunk unnamed-chunk-6](mortality-figure/unnamed-chunk-6-2.png)![plot of chunk unnamed-chunk-6](mortality-figure/unnamed-chunk-6-3.png)![plot of chunk unnamed-chunk-6](mortality-figure/unnamed-chunk-6-4.png)
