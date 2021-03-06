---
title: "Linear Regression Course Project"
output: html_document
---
---
title: "Linear Regression Course Project"
output: pdf_document
---

##Summary
In this project I will be using the mtcars dataset in R to answer the question, "Is mpg affected by type of transmission: manual or automatic?". The dataset mtcars uses a set of 32 vehicles with 11 variables describing different features. Through the use of exploratory data analysis, statistical inference, and linear regression, I will determine the generalized affect of having a manual(am=1) or automatic(am=0) transmission on mpg. 

##Exploratory Data Analysis
The first step I took was to transorm the columns for cyl, am, gear and carb into factor variables and reassign them to the mtcars data frame. I then performed some elementary plot calls to see if there was an appreciable difference in means between the two factors of 'am': automatic, and manual.  
[1] ```boxplot(mpg~am, mtcars)```  
This graph clearly shows that there is evidence that the cars with manual transmission have a different mean mileage than with an automatic. Mpg depends heavily on weight, so to get an idea of the distributions between the transmissions I used  
[2] ```boxplot(wt~am, mtcars)```  
This plot also clearly shows that cars with a manual transmission are significantly lighter.  
```mean(mtcars[mtcars$am=="0",]$wt)```  
```[1] 3.768895```  
```mean(mtcars[mtcars$am=="1",]$wt)```  
```[1] 2.411```  
Here we see that the means differ by over 1300 lbs, which is considerably more than the differences in weight between transmissions.

##Statistical Inference
First I used the t.test to determine that the difference in mean was statistically significant with:  
```t.test(mtcars[mtcars$am=="0",]$mpg, mtcars[mtcars$am=="1",]$mpg)```  
yeilding a p-value of 0.0014, so the mean mile per gallon difference is significant. To test the signifigance of the difference in means I used the t.test:  
```t.test(mtcars[mtcars$am=="0",]$wt, mtcars[mtcars$am=="1",]$wt)```  
yeilding a p-value of 6.272e-06, so the difference in means is also statistically significant. One might infer that the automatic transmission is itself heavier than the manual, and that would be correct, but the difference in transmission weight(~100lbs) would not be significant next to the mean difference of ~1000lbs. 


##Linear Regression
To quantify the affect that transmission type has on mileage, I first fit a linear model with all of the variables with `fit <- lm(mpg~.,mtcars)`. To see how all the variables interact with mpg I used the code `vif(fit)` which determined that the variables cyl, disp, hp, and wt have the most interaction with the mgp variable. Disp and hp were clearly correlated, so I only used hp in the linear models following to reduce the R^2 inflation. With `model1 <- step(fit, direction="both")` R steps through the linear model with all the regressor variables in both directions and returns the linear model with the fewest variables leading to the best estimate of the dependant variable. Model1 here has regressors: cyl, hp, wt, and am. To deal with the information that weight is correlated with transmission type, I inserted a confounding variable to a second model to determine if it was significant enough to include in the model with the code:  
```model2 <- lm(mpg~am+wt+cyl+hp+am:wt, mtcars); anova(model1, model2)```  
When I used the R function, anova, I got a Pr(>F) value of 0.05828, meaning that addiing the confounding variable is right on the border of significance in the model. In the name of parsimony, I used the model without the confounding variable, model1.
A call of `summary(model1)` give us the coefficients of the model. The estimate of the Intercept is 33.708, with cyl6=-3.031 and cyl8=-2.164, so holding all else constant, we can clearly see we get our best mpg with a 4-cylinder engine. Weight has a -2.497 coefficient signifying as weight increases, mileage decreases strongly. H
orse power has a slightly negative coefficient, -0.032, suggesting that it has nearly no effect on mileage. Our coefficient on the am1 variable is really the one of interest here, where is says that, holding all other variables constant, it is expected that there is a generic increase in the prediction of mileage in a manual car versus an automatic. In this model, manual cars should have approximately 1.81 more miles per gallon.  
`plot(model1)` , shows the residual plots for the model chosen. The Residual vs Fitted [3] shows that the residuals are normally distributed along the fitted values. The Normal Q-Q [4] plot shows that in the center of the distribution, the model has the best fit, and as the residuals become more drasitc, the model fits slightly worse. The Scale-Location plot [5] shows again that the residuals are normally distributed, and the Residual vs Leverage plot [6] confirms that the outliers with large leverages are consistant between the different plots.

##Conclusion



##Appendix

[1] `{r, echo=FALSE} `
[2] `{r, echo=FALSE} `
[3] `{r, echo=FALSE} `
[4] `{r, echo=FALSE} `
[5] `{r, echo=FALSE} `
[6] `{r, echo=FALSE} `
