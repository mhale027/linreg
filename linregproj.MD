---
title: "Linear Regression Course Project"
output: html_document
---

##Summary
In this project I will be using the mtcars dataset in R to determine if the affect of transmission type on mile per gallon ratings. The dataset mtcars uses a set of 32 vehicles with 11 variables describing different features. Through the use of exploratory data analysis, statistical inference, and linear regression, I will determine the generalized affect of having a manual(am=1) or automatic(am=0) transmission on mpg. 

##Exploratory Data Analysis
The first step I took was to perform some elementary plot calls to see if there was an appreciable difference in means between the two factors of 'am': 0-automatic, and 1-manual. 
[1] ```boxplot(mpg~am, mtcars)``` 
This graph clearly shows that there is evidence that the cars with manual transmission have a different mean mileage than with an automatic. Mpg depends heavily on weight, so to get an idea of the distributions between the transmissions I used 
[2] ```boxplot(wt~am, mtcars)```
This plot also clearly shows that cars with a manual transmission are significantly lighter.
```mean(mtcars[mtcars$am=="0",]$wt)
[1] 3.768895
 mean(mtcars[mtcars$am=="1",]$wt)
[1] 2.411```
Here we see that the means differ by over 1300 lbs, which is considerably more than the differences in weight between transmissions.

##Statistical Inference
First I used the t.test to determine that the difference in mean was statistically significant with: ```t.test(mtcars[mtcars$am=="0",]$mpg, mtcars[mtcars$am=="1",]$mpg)```, yeilding a p-value of 3.715e-14, so the mean mile per gallon difference is significant. To test the signifigance of the difference in means I used the t.test: ```t.test(mtcars[mtcars$am=="0",]$wt, mtcars[mtcars$am=="1",]$wt)```, yeilding a p-value of 6.272e-06, so the difference in means is also statistically significant. One might infer that the automatic transmission is itself heavier than the manual, and that would be correct, but the difference in transmission weight(~100lbs) would not be significant next to the mean difference of ~1000lbs. 


##Linear Regression



##Conclusion



##Appendix









```{r, echo=TRUE}
plot(cars)
```
