---
title: "Statistical-Inference-Course-Project Part 2"
author: "Yigang"
output:
  html_document:
    keep_md: true
---
# Part 2 Basic Inferential Data Analysis 

### Load data and get an overview of the date set


```r
#?ToothGrowth
#The response is the length of odontoblasts (cells responsible for tooth growth) in 60 guinea pigs. Each animal received one of three dose levels of vitamin C (0.5, 1, and 2 mg/day) by one of two delivery methods, orange juice or ascorbic acid (a form of vitamin C and coded as VC).

data("ToothGrowth")
head(ToothGrowth)
```

```
##    len supp dose
## 1  4.2   VC  0.5
## 2 11.5   VC  0.5
## 3  7.3   VC  0.5
## 4  5.8   VC  0.5
## 5  6.4   VC  0.5
## 6 10.0   VC  0.5
```

```r
summary(ToothGrowth)
```

```
##       len        supp         dose      
##  Min.   : 4.20   OJ:30   Min.   :0.500  
##  1st Qu.:13.07   VC:30   1st Qu.:0.500  
##  Median :19.25           Median :1.000  
##  Mean   :18.81           Mean   :1.167  
##  3rd Qu.:25.27           3rd Qu.:2.000  
##  Max.   :33.90           Max.   :2.000
```

### Visualizate the data set for anaylysis 


```r
# make dose as a factor has three levels
ToothGrowth$dose <- as.factor(ToothGrowth$dose)
```


```r
#plot teeth length ~ dose level by supplement type
library("ggplot2")
ggplot(ToothGrowth, aes(x=dose, y=len, fill=supp))+
        geom_boxplot()+
        facet_grid(.~supp)
```

![](Statistical-Inference-Course-Project-Part-2_files/figure-html/unnamed-chunk-3-1.png)<!-- -->


```r
#plot teeth length ~ supplement type by dose level
ggplot(ToothGrowth, aes(x=supp, y=len, fill=supp))+
        geom_boxplot()+
        facet_grid(.~dose)
```

![](Statistical-Inference-Course-Project-Part-2_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

- Discuss: Dose level and teeth length have a positive relationship for either supplement

### Hypothesis Tests

Use hypothesis tests to compare tooth growth by supp and dose

- Null Hypothesis: Dose type or delivery methods of Vitamin C has no effect on tooth growth
- significance level alpha = 0.05


```r
t.test(len ~ supp, data = ToothGrowth)
```

```
## 
## 	Welch Two Sample t-test
## 
## data:  len by supp
## t = 1.9153, df = 55.309, p-value = 0.06063
## alternative hypothesis: true difference in means is not equal to 0
## 95 percent confidence interval:
##  -0.1710156  7.5710156
## sample estimates:
## mean in group OJ mean in group VC 
##         20.66333         16.96333
```

- Discuss: The overall result shows that p-value = 0.06063 is greater then 0.05 significance level, hence we do not reject the null hypothesis.


```r
#T test at dose level 0.5
dose1 <- subset(ToothGrowth, dose %in% c(0.5) ) 
t.test(len ~ supp, data = dose1)
```

```
## 
## 	Welch Two Sample t-test
## 
## data:  len by supp
## t = 3.1697, df = 14.969, p-value = 0.006359
## alternative hypothesis: true difference in means is not equal to 0
## 95 percent confidence interval:
##  1.719057 8.780943
## sample estimates:
## mean in group OJ mean in group VC 
##            13.23             7.98
```

- Discuss: The p-value = 0.006359 at dose level 0.5 is smaller then 0.05 significance level, hence we can reject the null hypothesis.


```r
#T test at dose level 0.1
dose1 <- subset(ToothGrowth, dose %in% c(1.0) ) 
t.test(len ~ supp, data = dose1)
```

```
## 
## 	Welch Two Sample t-test
## 
## data:  len by supp
## t = 4.0328, df = 15.358, p-value = 0.001038
## alternative hypothesis: true difference in means is not equal to 0
## 95 percent confidence interval:
##  2.802148 9.057852
## sample estimates:
## mean in group OJ mean in group VC 
##            22.70            16.77
```

- Discuss: The p-value = 0.001038 at dose level 1.0 is smaller then 0.05 significance 
level, hence we can reject the null hypothesis.


```r
#T test at dose level 2
dose1 <- subset(ToothGrowth, dose %in% c(2.0) ) 
t.test(len ~ supp, data = dose1)
```

```
## 
## 	Welch Two Sample t-test
## 
## data:  len by supp
## t = -0.046136, df = 14.04, p-value = 0.9639
## alternative hypothesis: true difference in means is not equal to 0
## 95 percent confidence interval:
##  -3.79807  3.63807
## sample estimates:
## mean in group OJ mean in group VC 
##            26.06            26.14
```

- Discuss: The p-value = 0.9639 at dose level 2.0 is greater then 0.05 significance 
level, hence we can not reject the null hypothesis.

### Conclusions

- Dose level and teeth length have a positive relationship for either supplement
- Dose type or delivery methods of Vitamin C has no effect on tooth growth on dose level at 2.0
- Dose type or delivery methods of Vitamin C do have effect on tooth growth on dose level at 0.5 and 1.0



























