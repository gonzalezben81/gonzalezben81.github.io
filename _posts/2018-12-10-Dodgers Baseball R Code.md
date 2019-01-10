````

# Predictive Model for Los Angeles Dodgers Promotion and Attendance (R)

library(car)  # special functions for linear regression
library(lattice)  # graphics package
setwd("C:/Users/Ben/Desktop/")
# read in data and create a data frame called dodgers
dodgers <- read.csv("dodgers.csv")
attach(dodgers)
print(str(dodgers))  # check the structure of the data frame

summary(dodgers)

# dataset<-dodgers


sapply(dodgers, class)


hist(attend,xlab = "Attendance",main = "Histogram of Dodgers Attendance")

plot(dodgers$attend/1000~dodgers$temp,las=1,xlab = "Temperature",
     ylab = "Attendance(thousands)",col="blue",pch=19,
     main = "Temperature by Attendance(thousands)")


plot(dodgers$temp,dodgers$attend/1000,las=1,xlab = "Temperature",
     ylab = "Attendance(thousands)",col="blue",pch=19,
     main = "Temperature by Attendance(thousands)")


plot(dodgers$temp~dodgers$ordered_month,las=1,xlab = "Month",
     ylab = "Temp",col="blue",pch=19,
     main = "Month by Temp")


# define an ordered day-of-week variable ##############
# for plots and data summaries
dodgers$ordered_day_of_week <- with(data=dodgers,
                                    ifelse ((day_of_week == "Monday"),1,
                                    ifelse ((day_of_week == "Tuesday"),2,
                                    ifelse ((day_of_week == "Wednesday"),3,
                                    ifelse ((day_of_week == "Thursday"),4,
                                    ifelse ((day_of_week == "Friday"),5,
                                    ifelse ((day_of_week == "Saturday"),6,7)))))))
dodgers$ordered_day_of_week <- factor(dodgers$ordered_day_of_week, levels=1:7,
                                      labels=c("Mon", "Tue", "Wed", "Thur", "Fri", "Sat", "Sun"))

# exploratory data analysis with standard graphics: attendance by day of week
with(data=dodgers,plot(ordered_day_of_week, attend/1000, 
                       xlab = "Day of Week", ylab = "Attendance (thousands)", 
                       col = "violet", las = 1,main = "Dodgers Attendance (thousands) by Day of Week"))



##Bobblehead Attendance 
with(data=dodgers,plot(bobblehead, attend/1000, 
                       xlab = "Bobblehead", ylab = "Attendance (thousands)", 
                       col = "blue",las = 1,main="Bobblehead by Attendance(thousands)"))



##T-shirt Attendance
with(data=dodgers,plot(shirt, attend/1000, 
                       xlab = "Shirt", ylab = "Attendance (thousands)", 
                       col = "blue",las = 1,main="T-shirt Giveaway by Attendance(thousands)"))

##Fireworks Attendance 
with(data=dodgers,plot(fireworks, attend/1000, 
                       xlab = "Fireworks", ylab = "Attendance (thousands)", 
                       col = "blue",las = 1,main="Fireworks by Attendance(thousands)"))

##Cap Attendance 
with(data=dodgers,plot(cap, attend/1000, 
                       xlab = "Cap", ylab = "Attendance (thousands)", 
                       col = "blue",las = 1,main="Cap Giveaway by Attendance(thousands)"))

##Tables for Weekly Promotions Effect on Attendance ##################################

# when do the Dodgers use bobblehead promotions
with(dodgers, table(bobblehead,ordered_day_of_week)) # bobbleheads on Tuesday

##Caps
with(dodgers, table(dodgers$cap,ordered_day_of_week))

##T-shirts
with(dodgers, table(dodgers$shirt,ordered_day_of_week))

##Fireworks
with(dodgers, table(dodgers$fireworks,ordered_day_of_week)) ##Fireworks on Friday

# define an ordered month variable ################
# for plots and data summaries
dodgers$ordered_month <- with(data=dodgers,
                              ifelse ((month == "APR"),4,
                                      ifelse ((month == "MAY"),5,
                                              ifelse ((month == "JUN"),6,
                                                      ifelse ((month == "JUL"),7,
                                                              ifelse ((month == "AUG"),8,
                                                                      ifelse ((month == "SEP"),9,10)))))))
dodgers$ordered_month <- factor(dodgers$ordered_month, levels=4:10,
                                labels = c("April", "May", "June", "July", "Aug", "Sept", "Oct"))

# exploratory data analysis with standard R graphics: attendance by month 
with(data=dodgers,plot(ordered_month,attend/1000, xlab = "Month", 
                       ylab = "Attendance (thousands)", col = "light blue", las = 1,
                       main = "Monthly Attendance (thousands)"))




##Tables for Monthly Giveaways ###################################################


with(dodgers, table(bobblehead,ordered_month)) # bobbleheads on Tuesday

##Caps
with(dodgers, table(dodgers$cap,ordered_month))

##T-shirts
with(dodgers, table(dodgers$shirt,ordered_month))

##Fireworks
with(dodgers, table(dodgers$fireworks,ordered_month)) ##Fireworks on Friday




group.labels

# exploratory data analysis displaying many variables ########
# looking at attendance and conditioning on day/night
# the skies and whether or not fireworks are displayed
library(lattice) # used for plotting 
# let us prepare a graphical summary of the dodgers data
group.labels <- c("No Fireworks","Fireworks")
group.symbols <- c(21,24)
group.colors <- c("black","black") 
group.fill <- c("black","red")
xyplot(attend/1000 ~ temp | skies + day_night, 
       data = dodgers, groups = fireworks, pch = group.symbols, 
       aspect = 1, cex = 1.5, col = group.colors, fill = group.fill,
       layout = c(2, 2), type = c("p","g"),
       strip=strip.custom(strip.levels=TRUE,strip.names=FALSE, style=1),
       xlab = "Temperature (Degrees Fahrenheit)", 
       ylab = "Attendance (thousands)",
       key = list(space = "top", 
                  text = list(rev(group.labels),col = rev(group.colors)),
                  points = list(pch = rev(group.symbols), col = rev(group.colors),
                                fill = rev(group.fill))))  


##Cap Giveaways #######  
group.labels <- c("No Cap","Cap")
group.symbols <- c(21,24)
group.colors <- c("blue","blue") 
group.fill <- c("green","yellow")
xyplot(attend/1000 ~ temp | skies + day_night, 
       data = dodgers, groups = cap, pch = group.symbols, 
       aspect = 1, cex = 1.5, col = group.colors, fill = group.fill,
       layout = c(2, 2), type = c("p","g"),
       strip=strip.custom(strip.levels=TRUE,strip.names=FALSE, style=1),
       xlab = "Temperature (Degrees Fahrenheit)", 
       ylab = "Attendance (thousands)",
       key = list(space = "top", 
                  text = list(rev(group.labels),col = rev(group.colors)),
                  points = list(pch = rev(group.symbols), col = rev(group.colors),
                                fill = rev(group.fill)))) 


##T-shirt Giveaways #######
group.labels <- c("No Shirt","Shirt")
group.symbols <- c(21,24)
group.colors <- c("red","black") 
group.fill <- c("green","black")
xyplot(attend/1000 ~ temp | skies + day_night, 
       data = dodgers, groups = shirt, pch = group.symbols, 
       aspect = 1, cex = 1.5, col = group.colors, fill = group.fill,
       layout = c(2, 2), type = c("p","g"),
       strip=strip.custom(strip.levels=TRUE,strip.names=FALSE, style=1),
       xlab = "Temperature (Degrees Fahrenheit)", 
       ylab = "Attendance (thousands)",
       key = list(space = "top", 
                  text = list(rev(group.labels),col = rev(group.colors)),
                  points = list(pch = rev(group.symbols), col = rev(group.colors),
                                fill = rev(group.fill))))



##Bobblehead Giveaways ##############
group.labels <- c("No Bobblehead","Bobblehead")
group.symbols <- c(21,24)
group.colors <- c("black","black") 
group.fill <- c("blue","red")
xyplot(attend/1000 ~ temp | skies + day_night, 
       data = dodgers, groups = bobblehead, pch = group.symbols, 
       aspect = 1, cex = 1.5, col = group.colors, fill = group.fill,
       layout = c(2, 2), type = c("p","g"),
       strip=strip.custom(strip.levels=TRUE,strip.names=FALSE, style=1),
       xlab = "Temperature (Degrees Fahrenheit)", 
       ylab = "Attendance (thousands)",
       key = list(space = "top", 
                  text = list(rev(group.labels),col = rev(group.colors)),
                  points = list(pch = rev(group.symbols), col = rev(group.colors),
                                fill = rev(group.fill))))




# attendance by opponent and day/night game ########################
group.labels <- c("Day","Night")
group.symbols <- c(1,20)
group.symbols.size <- c(2,2.75)
bwplot(opponent ~ attend/1000, data = dodgers, groups = day_night, 
       xlab = "Attendance (thousands)",main="Attendance by Opponent",
       panel = function(x, y, groups, subscripts, ...) 
       {panel.grid(h = (length(levels(dodgers$opponent)) - 1), v = -1)
         panel.stripplot(x, y, groups = groups, subscripts = subscripts, 
                         cex = group.symbols.size, pch = group.symbols, col = "darkblue")
       },
       key = list(space = "top", 
                  text = list(group.labels,col = "black"),
                  points = list(pch = group.symbols, cex = group.symbols.size, 
                                col = "darkblue")))




##T-shirts effect on Attendance ########################################################
group.labels <- c("NO Shirt","Shirt")
group.symbols <- c(1,20)
group.symbols.size <- c(2,2.75)
bwplot(opponent ~ attend/1000, data = dodgers, groups = dodgers$shirt, 
       xlab = "Attendance (thousands)",main="Attendance by Opponent",
       panel = function(x, y, groups, subscripts, ...) 
       {panel.grid(h = (length(levels(dodgers$opponent)) - 1), v = -1)
         panel.stripplot(x, y, groups = groups, subscripts = subscripts, 
                         cex = group.symbols.size, pch = group.symbols, col = "darkgreen")
       },
       key = list(space = "top", 
                  text = list(group.labels,col = "black"),
                  points = list(pch = group.symbols, cex = group.symbols.size, 
                                col = "darkgreen")))




##Fireworks effect on Attendance ######################################################
group.labels <- c("NO Fireworks","Fireworks")
group.symbols <- c(1,20)
group.symbols.size <- c(2,2.75)
bwplot(opponent ~ attend/1000, data = dodgers, groups = dodgers$fireworks, 
       xlab = "Attendance (thousands)",main="Attendance by Opponent",
       panel = function(x, y, groups, subscripts, ...) 
       {panel.grid(h = (length(levels(dodgers$opponent)) - 1), v = -1)
         panel.stripplot(x, y, groups = groups, subscripts = subscripts, 
                         cex = group.symbols.size, pch = group.symbols, col = "darkred")
       },
       key = list(space = "top", 
                  text = list(group.labels,col = "black"),
                  points = list(pch = group.symbols, cex = group.symbols.size, 
                                col = "darkred")))



##Cap Effect on Attendance ##################################################
group.labels <- c("NO Cap","Cap")
group.symbols <- c(1,20)
group.symbols.size <- c(2,2.75)
bwplot(opponent ~ attend/1000, data = dodgers, groups = dodgers$cap, 
       xlab = "Attendance (thousands)",main="Attendance by Opponent",
       panel = function(x, y, groups, subscripts, ...) 
       {panel.grid(h = (length(levels(dodgers$opponent)) - 1), v = -1)
         panel.stripplot(x, y, groups = groups, subscripts = subscripts, 
                         cex = group.symbols.size, pch = group.symbols, col = "darkgreen")
       },
       key = list(space = "top", 
                  text = list(group.labels,col = "black"),
                  points = list(pch = group.symbols, cex = group.symbols.size, 
                                col = "darkgreen")))




##Temperature Effect on Attendance ##################################################
dodgers$highlow <- with(dodgers, ifelse(temp <=64,1, 
                                 ifelse(temp >=65 & temp <=76,2,3)))


dodgers$highlow <- factor(dodgers$highlow, levels=1:3,
                          labels = c("Cold", "Mild", "Hot"))






group.labels <- c("Cold: 64 or lower","Mild: 65-76","Hot: 77 and up")
group.symbols <- c(20,20,20)
group.symbols.size <- c(2,2,2)
col<-c("blue","lightblue","red")
bwplot(opponent ~ attend/1000, data = dodgers, groups = highlow, 
       xlab = "Attendance (thousands)",
       panel = function(x, y, groups, subscripts, ...) 
       {panel.grid(h = (length(levels(dodgers$opponent)) - 1), v = -1)
         panel.stripplot(x, y, groups = groups, subscripts = subscripts, 
                         cex = group.symbols.size, pch = group.symbols, col = col)
       },
       key = list(space = "top", 
                  text = list(group.labels,col = "black"),
                  points = list(pch = group.symbols, cex = group.symbols.size, 
                                col = col)))





##Training Set employ training-and-test regimen for model validation ############
set.seed(1234) # set seed for repeatability of training-and-test split
training_test <- c(rep(1,length=trunc((2/3)*nrow(dodgers))),
                   rep(2,length=(nrow(dodgers) - trunc((2/3)*nrow(dodgers)))))
dodgers$training_test <- sample(training_test) # random permutation 
dodgers$training_test <- factor(dodgers$training_test, 
                                levels=c(1,2), labels=c("TRAIN","TEST"))
dodgers.train <- subset(dodgers, training_test == "TRAIN")
print(str(dodgers.train)) # check training data frame
dodgers.test <- subset(dodgers, training_test == "TEST")
print(str(dodgers.test)) # check test data frame




##Booblehead Linear Models ###################################################

# specify a simple model with bobblehead entered last
my.model <- {attend ~ ordered_month + ordered_day_of_week + bobblehead}

# fit the model to the training set
train.model.fit <- lm(my.model, data = dodgers.train)
# summary of model fit to the training set
print(summary(train.model.fit))
# training set predictions from the model fit to the training set
dodgers.train$predict_attend <- predict(train.model.fit) 

# test set predictions from the model fit to the training set
dodgers.test$predict_attend <- predict(train.model.fit, 
                                       newdata = dodgers.test)

# compute the proportion of response variance
# accounted for when predicting out-of-sample
cat("\n","Proportion of Test Set Variance Accounted for: ",
    round((with(dodgers.test,cor(attend,predict_attend)^2)),
          digits=3),"\n",sep="")

# merge the training and test sets for plotting
dodgers.plotting.frame <- rbind(dodgers.train,dodgers.test)

# generate predictive modeling visual for management
group.labels <- c("No Bobbleheads","Bobbleheads")
group.symbols <- c(21,24)
group.colors <- c("black","black") 
group.fill <- c("black","red") 
xyplot(predict_attend/1000 ~ attend/1000 | training_test, 
       data = dodgers.plotting.frame, groups = bobblehead, cex = 2,
       pch = group.symbols, col = group.colors, fill = group.fill, 
       layout = c(2, 1), xlim = c(20,65), ylim = c(20,65), 
       aspect=1, type = c("p","g"),
       panel=function(x,y, ...)
       {panel.xyplot(x,y,...)
         panel.segments(25,25,60,60,col="black",cex=2)
       },
       strip=function(...) strip.default(..., style=1),
       xlab = "Actual Attendance (thousands)", 
       ylab = "Predicted Attendance (thousands)",
       key = list(space = "top", 
                  text = list(rev(group.labels),col = rev(group.colors)),
                  points = list(pch = rev(group.symbols), 
                                col = rev(group.colors),
                                fill = rev(group.fill))))            

# use the full data set to obtain an estimate of the increase in
# attendance due to bobbleheads, controlling for other factors 
my.model.fit <- lm(my.model, data = dodgers)  # use all available data
print(summary(my.model.fit))
# tests statistical significance of the bobblehead promotion
# type I anova computes sums of squares for sequential tests
print(anova(my.model.fit))  

cat("\n","Estimated Effect of Bobblehead Promotion on Attendance: ",
    round(my.model.fit$coefficients[length(my.model.fit$coefficients)],
          digits = 0),"\n",sep="")

# standard graphics provide diagnostic plots
plot(my.model.fit)

# additional model diagnostics drawn from the car package
library(car)
residualPlots(my.model.fit)
marginalModelPlots(my.model.fit)
print(outlierTest(my.model.fit))

# Suggestions for the student:
# Examine regression diagnostics for the fitted model.
# Examine other linear predictors and other explanatory variables.
# See if you can improve upon the model with variable transformations.




##Cap Linear Models ###################################################

# specify a simple model with bobblehead entered last
my.modelcap <- {attend ~ ordered_month + ordered_day_of_week + cap}

# fit the model to the training set
train.model.fitcap <- lm(my.modelcap, data = dodgers.train)
# summary of model fit to the training set
print(summary(train.model.fitcap))
# training set predictions from the model fit to the training set
dodgers.train$predict_attend <- predict(train.model.fitcap) 

# test set predictions from the model fit to the training set
dodgers.test$predict_attend <- predict(train.model.fitcap, 
                                       newdata = dodgers.test)

# compute the proportion of response variance
# accounted for when predicting out-of-sample
cat("\n","Proportion of Test Set Variance Accounted for: ",
    round((with(dodgers.test,cor(attend,predict_attend)^2)),
          digits=3),"\n",sep="")

# merge the training and test sets for plotting
dodgers.plotting.framecap <- rbind(dodgers.train,dodgers.test)

# generate predictive modeling visual for management
group.labels <- c("No Cap","Cap")
group.symbols <- c(21,24)
group.colors <- c("black","black") 
group.fill <- c("black","red")  
xyplot(predict_attend/1000 ~ attend/1000 | training_test, 
       data = dodgers.plotting.framecap, groups = cap, cex = 2,
       pch = group.symbols, col = group.colors, fill = group.fill, 
       layout = c(2, 1), xlim = c(20,65), ylim = c(20,65), 
       aspect=1, type = c("p","g"),
       panel=function(x,y, ...)
       {panel.xyplot(x,y,...)
         panel.segments(25,25,60,60,col="black",cex=2)
       },
       strip=function(...) strip.default(..., style=1),
       xlab = "Actual Attendance (thousands)", 
       ylab = "Predicted Attendance (thousands)",
       key = list(space = "top", 
                  text = list(rev(group.labels),col = rev(group.colors)),
                  points = list(pch = rev(group.symbols), 
                                col = rev(group.colors),
                                fill = rev(group.fill))))            

# use the full data set to obtain an estimate of the increase in
# attendance due to CAP, controlling for other factors 
my.model.fitcap <- lm(my.modelcap, data = dodgers)  # use all available data
print(summary(my.model.fitcap))
# tests statistical significance of the bobblehead promotion
# type I anova computes sums of squares for sequential tests
print(anova(my.model.fitcap))  

cat("\n","Estimated Effect of Cap Promotion on Attendance: ",
    round(my.model.fitcap$coefficients[length(my.model.fitcap$coefficients)],
          digits = 0),"\n",sep="")

# standard graphics provide diagnostic plots
plot(my.model.fitcap)

# additional model diagnostics drawn from the car package
library(car)
residualPlots(my.model.fitcap)
marginalModelPlots(my.model.fitcap)
print(outlierTest(my.model.fitcap))

# Suggestions for the student:
# Examine regression diagnostics for the fitted model.
# Examine other linear predictors and other explanatory variables.
# See if you can improve upon the model with variable transformations.







##Fireworks Linear Models ###################################################

# specify a simple model with bobblehead entered last
my.model3 <- {attend ~ ordered_month + ordered_day_of_week + fireworks}

# fit the model to the training set
train.model.fit3 <- lm(my.model3, data = dodgers.train)
# summary of model fit to the training set
print(summary(train.model.fit3))
# training set predictions from the model fit to the training set
dodgers.train$predict_attend <- predict(train.model.fit3) 

# test set predictions from the model fit to the training set
dodgers.test$predict_attend <- predict(train.model.fit3, 
                                       newdata = dodgers.test)

# compute the proportion of response variance
# accounted for when predicting out-of-sample
cat("\n","Proportion of Test Set Variance Accounted for: ",
    round((with(dodgers.test,cor(attend,predict_attend)^2)),
          digits=3),"\n",sep="")

# merge the training and test sets for plotting
dodgers.plotting.framecap <- rbind(dodgers.train,dodgers.test)

# generate predictive modeling visual for management
group.labels <- c("No Fireworks","Fireworks")
group.symbols <- c(21,24)
group.colors <- c("black","black") 
group.fill <- c("blue","green")  
xyplot(predict_attend/1000 ~ attend/1000 | training_test, 
       data = dodgers.plotting.framecap, groups = fireworks, cex = 2,
       pch = group.symbols, col = group.colors, fill = group.fill, 
       layout = c(2, 1), xlim = c(20,65), ylim = c(20,65), 
       aspect=1, type = c("p","g"),
       panel=function(x,y, ...)
       {panel.xyplot(x,y,...)
         panel.segments(25,25,60,60,col="black",cex=2)
       },
       strip=function(...) strip.default(..., style=1),
       xlab = "Actual Attendance (thousands)", 
       ylab = "Predicted Attendance (thousands)",
       key = list(space = "top", 
                  text = list(rev(group.labels),col = rev(group.colors)),
                  points = list(pch = rev(group.symbols), 
                                col = rev(group.colors),
                                fill = rev(group.fill))))            

# use the full data set to obtain an estimate of the increase in
# attendance due to CAP, controlling for other factors 
my.model.fit3 <- lm(my.model3, data = dodgers)  # use all available data
print(summary(my.model.fit3))
# tests statistical significance of the bobblehead promotion
# type I anova computes sums of squares for sequential tests
print(anova(my.model.fit3))  

cat("\n","Estimated Effect of Fireworks Promotion on Attendance: ",
    round(my.model.fit3$coefficients[length(my.model.fit3$coefficients)],
          digits = 0),"\n",sep="")

# standard graphics provide diagnostic plots
plot(my.model.fit3)

# additional model diagnostics drawn from the car package
library(car)
residualPlots(my.model.fit3)
marginalModelPlots(my.model.fit3)
print(outlierTest(my.model.fit3))

# Suggestions for the student:
# Examine regression diagnostics for the fitted model.
# Examine other linear predictors and other explanatory variables.
# See if you can improve upon the model with variable transformations.



##Shirt Linear Models ###################################################

# specify a simple model with shirts entered last
my.model4 <- {attend ~ ordered_month + ordered_day_of_week + shirt}

# fit the model to the training set
train.model.fit4 <- lm(my.model4, data = dodgers.train)
# summary of model fit to the training set
print(summary(train.model.fit4))
# training set predictions from the model fit to the training set
dodgers.train$predict_attend <- predict(train.model.fit4) 

# test set predictions from the model fit to the training set
dodgers.test$predict_attend <- predict(train.model.fit4, 
                                       newdata = dodgers.test)

# compute the proportion of response variance
# accounted for when predicting out-of-sample
cat("\n","Proportion of Test Set Variance Accounted for: ",
    round((with(dodgers.test,cor(attend,predict_attend)^2)),
          digits=3),"\n",sep="")

# merge the training and test sets for plotting
dodgers.plotting.frame4 <- rbind(dodgers.train,dodgers.test)

# generate predictive modeling visual for management
group.labels <- c("No Shirt","Shirt")
group.symbols <- c(21,24)
group.colors <- c("black","black") 
group.fill <- c("blue","green")  
xyplot(predict_attend/1000 ~ attend/1000 | training_test, 
       data = dodgers.plotting.framecap, groups = shirt, cex = 2,
       pch = group.symbols, col = group.colors, fill = group.fill, 
       layout = c(2, 1), xlim = c(20,65), ylim = c(20,65), 
       aspect=1, type = c("p","g"),
       panel=function(x,y, ...)
       {panel.xyplot(x,y,...)
         panel.segments(25,25,60,60,col="black",cex=2)
       },
       strip=function(...) strip.default(..., style=1),
       xlab = "Actual Attendance (thousands)", 
       ylab = "Predicted Attendance (thousands)",
       key = list(space = "top", 
                  text = list(rev(group.labels),col = rev(group.colors)),
                  points = list(pch = rev(group.symbols), 
                                col = rev(group.colors),
                                fill = rev(group.fill))))            

# use the full data set to obtain an estimate of the increase in
# attendance due to CAP, controlling for other factors 
my.model.fit4 <- lm(my.model4, data = dodgers)  # use all available data
print(summary(my.model.fit4))
# tests statistical significance of the bobblehead promotion
# type I anova computes sums of squares for sequential tests
print(anova(my.model.fit4))  

cat("\n","Estimated Effect of Shirt Promotion on Attendance: ",
    round(my.model.fit4$coefficients[length(my.model.fit4$coefficients)],
          digits = 0),"\n",sep="")

# standard graphics provide diagnostic plots
plot(my.model.fit4)

# additional model diagnostics drawn from the car package
library(car)
residualPlots(my.model.fit4)
marginalModelPlots(my.model.fit4)
print(outlierTest(my.model.fit4))

# Suggestions for the student:
# Examine regression diagnostics for the fitted model.
# Examine other linear predictors and other explanatory variables.
# See if you can improve upon the model with variable transformations.



##Multiple Giveaways: Linear Model Cap + Shirt ###################################################

# specify a simple model with shirts entered last
my.model5 <- {attend ~ ordered_month + ordered_day_of_week + cap + shirt}

# fit the model to the training set
train.model.fit5 <- lm(my.model5, data = dodgers.train)
# summary of model fit to the training set
print(summary(train.model.fit5))
# training set predictions from the model fit to the training set
dodgers.train$predict_attend <- predict(train.model.fit5) 

# test set predictions from the model fit to the training set
dodgers.test$predict_attend <- predict(train.model.fit5, 
                                       newdata = dodgers.test)

# compute the proportion of response variance
# accounted for when predicting out-of-sample
cat("\n","Proportion of Test Set Variance Accounted for: ",
    round((with(dodgers.test,cor(attend,predict_attend)^2)),
          digits=3),"\n",sep="")

# merge the training and test sets for plotting
dodgers.plotting.frame5 <- rbind(dodgers.train,dodgers.test)

# generate predictive modeling visual for management
group.labels <- c("No Shirt/Cap","Shirt/Cap")
group.symbols <- c(21,24)
group.colors <- c("black","black") 
group.fill <- c("blue","green")  
xyplot(predict_attend/1000 ~ attend/1000 | training_test, 
       data = dodgers.plotting.frame5, groups = shirt, cex = 2,
       pch = group.symbols, col = group.colors, fill = group.fill, 
       layout = c(2, 1), xlim = c(20,65), ylim = c(20,65), 
       aspect=1, type = c("p","g"),
       panel=function(x,y, ...)
       {panel.xyplot(x,y,...)
         panel.segments(25,25,60,60,col="black",cex=2)
       },
       strip=function(...) strip.default(..., style=1),
       xlab = "Actual Attendance (thousands)", 
       ylab = "Predicted Attendance (thousands)",
       key = list(space = "top", 
                  text = list(rev(group.labels),col = rev(group.colors)),
                  points = list(pch = rev(group.symbols), 
                                col = rev(group.colors),
                                fill = rev(group.fill))))            

# use the full data set to obtain an estimate of the increase in
# attendance due to CAP, controlling for other factors 
my.model.fit5 <- lm(my.model5, data = dodgers)  # use all available data
print(summary(my.model.fit5))
# tests statistical significance of the bobblehead promotion
# type I anova computes sums of squares for sequential tests
print(anova(my.model.fit5))  

cat("\n","Estimated Effect of Cap/Shirt Promotion on Attendance: ",
    round(my.model.fit5$coefficients[length(my.model.fit5$coefficients)],
          digits = 0),"\n",sep="")

# standard graphics provide diagnostic plots
plot(my.model.fit5)

# additional model diagnostics drawn from the car package
library(car)
residualPlots(my.model.fit5)
marginalModelPlots(my.model.fit5)
print(outlierTest(my.model.fit5))

# Suggestions for the student:
# Examine regression diagnostics for the fitted model.
# Examine other linear predictors and other explanatory variables.
# See if you can improve upon the model with variable transformations.


##Multiple Giveaways Two: Linear Shirt + Bobblehead ###################################################

# specify a simple model with shirts entered last
my.model6 <- {attend ~ ordered_month + ordered_day_of_week + shirt + bobblehead}

# fit the model to the training set
train.model.fit6 <- lm(my.model6, data = dodgers.train)
# summary of model fit to the training set
print(summary(train.model.fit6))
# training set predictions from the model fit to the training set
dodgers.train$predict_attend <- predict(train.model.fit6) 

# test set predictions from the model fit to the training set
dodgers.test$predict_attend <- predict(train.model.fit6, 
                                       newdata = dodgers.test)

# compute the proportion of response variance
# accounted for when predicting out-of-sample
cat("\n","Proportion of Test Set Variance Accounted for: ",
    round((with(dodgers.test,cor(attend,predict_attend)^2)),
          digits=3),"\n",sep="")

# merge the training and test sets for plotting
dodgers.plotting.frame6 <- rbind(dodgers.train,dodgers.test)

# generate predictive modeling visual for management
group.labels <- c("No Shirt/Bobblehead","Shirt/Bobblehead")
group.symbols <- c(21,24)
group.colors <- c("black","black") 
group.fill <- c("blue","green")  
xyplot(predict_attend/1000 ~ attend/1000 | training_test, 
       data = dodgers.plotting.frame6, groups = shirt, cex = 2,
       pch = group.symbols, col = group.colors, fill = group.fill, 
       layout = c(2, 1), xlim = c(20,65), ylim = c(20,65), 
       aspect=1, type = c("p","g"),
       panel=function(x,y, ...)
       {panel.xyplot(x,y,...)
         panel.segments(25,25,60,60,col="black",cex=2)
       },
       strip=function(...) strip.default(..., style=1),
       xlab = "Actual Attendance (thousands)", 
       ylab = "Predicted Attendance (thousands)",
       key = list(space = "top", 
                  text = list(rev(group.labels),col = rev(group.colors)),
                  points = list(pch = rev(group.symbols), 
                                col = rev(group.colors),
                                fill = rev(group.fill))))            

# use the full data set to obtain an estimate of the increase in
# attendance due to CAP, controlling for other factors 
my.model.fit6 <- lm(my.model6, data = dodgers)  # use all available data
print(summary(my.model.fit6))
# tests statistical significance of the bobblehead promotion
# type I anova computes sums of squares for sequential tests
print(anova(my.model.fit6))  

cat("\n","Estimated Effect of Shirt/Bobblehead Promotion on Attendance: ",
    round(my.model.fit6$coefficients[length(my.model.fit6$coefficients)],
          digits = 0),"\n",sep="")

# standard graphics provide diagnostic plots
plot(my.model.fit6)

# additional model diagnostics drawn from the car package
library(car)
residualPlots(my.model.fit6)
marginalModelPlots(my.model.fit6)
print(outlierTest(my.model.fit6))

# Suggestions for the student:
# Examine regression diagnostics for the fitted model.
# Examine other linear predictors and other explanatory variables.
# See if you can improve upon the model with variable transformations.



##Multiple Giveaways: Linear Model Cap + Bobblehead ###################################################

# specify a simple model with shirts entered last
my.model7 <- {attend ~ ordered_month + ordered_day_of_week + cap + bobblehead}

# fit the model to the training set
train.model.fit7 <- lm(my.model7, data = dodgers.train)
# summary of model fit to the training set
print(summary(train.model.fit7))
# training set predictions from the model fit to the training set
dodgers.train$predict_attend <- predict(train.model.fit7) 

# test set predictions from the model fit to the training set
dodgers.test$predict_attend <- predict(train.model.fit7, 
                                       newdata = dodgers.test)

# compute the proportion of response variance
# accounted for when predicting out-of-sample
cat("\n","Proportion of Test Set Variance Accounted for: ",
    round((with(dodgers.test,cor(attend,predict_attend)^2)),
          digits=3),"\n",sep="")

# merge the training and test sets for plotting
dodgers.plotting.frame7 <- rbind(dodgers.train,dodgers.test)

# generate predictive modeling visual for management
group.labels <- c("No Cap/Bobblehead","Cap/Bobblehead")
group.symbols <- c(21,24)
group.colors <- c("black","black") 
group.fill <- c("blue","green")  
xyplot(predict_attend/1000 ~ attend/1000 | training_test, 
       data = dodgers.plotting.frame6, groups = shirt, cex = 2,
       pch = group.symbols, col = group.colors, fill = group.fill, 
       layout = c(2, 1), xlim = c(20,65), ylim = c(20,65), 
       aspect=1, type = c("p","g"),
       panel=function(x,y, ...)
       {panel.xyplot(x,y,...)
         panel.segments(25,25,60,60,col="black",cex=2)
       },
       strip=function(...) strip.default(..., style=1),
       xlab = "Actual Attendance (thousands)", 
       ylab = "Predicted Attendance (thousands)",
       key = list(space = "top", 
                  text = list(rev(group.labels),col = rev(group.colors)),
                  points = list(pch = rev(group.symbols), 
                                col = rev(group.colors),
                                fill = rev(group.fill))))            

# use the full data set to obtain an estimate of the increase in
# attendance due to CAP, controlling for other factors 
my.model.fit7 <- lm(my.model7, data = dodgers)  # use all available data
print(summary(my.model.fit7))
# tests statistical significance of the bobblehead promotion
# type I anova computes sums of squares for sequential tests
print(anova(my.model.fit7))  

cat("\n","Estimated Effect of Shirt/Bobblehead Promotion on Attendance: ",
    round(my.model.fit7$coefficients[length(my.model.fit7$coefficients)],
          digits = 0),"\n",sep="")

# standard graphics provide diagnostic plots
plot(my.model.fit7)

# additional model diagnostics drawn from the car package
library(car)
residualPlots(my.model.fit7)
marginalModelPlots(my.model.fit7)
print(outlierTest(my.model.fit7))

# Suggestions for the student:
# Examine regression diagnostics for the fitted model.
# Examine other linear predictors and other explanatory variables.
# See if you can improve upon the model with variable transformations.


##Multiple Giveaways: Linear Model Fireworks + Bobblehead ###################################################

# specify a simple model with shirts entered last
my.model8 <- {attend ~ ordered_month + ordered_day_of_week + fireworks + bobblehead}

# fit the model to the training set
train.model.fit8 <- lm(my.model8, data = dodgers.train)
# summary of model fit to the training set
print(summary(train.model.fit8))
# training set predictions from the model fit to the training set
dodgers.train$predict_attend <- predict(train.model.fit8) 

# test set predictions from the model fit to the training set
dodgers.test$predict_attend <- predict(train.model.fit8, 
                                       newdata = dodgers.test)

# compute the proportion of response variance
# accounted for when predicting out-of-sample
cat("\n","Proportion of Test Set Variance Accounted for: ",
    round((with(dodgers.test,cor(attend,predict_attend)^2)),
          digits=3),"\n",sep="")

# merge the training and test sets for plotting
dodgers.plotting.frame8 <- rbind(dodgers.train,dodgers.test)

# generate predictive modeling visual for management
group.labels <- c("No Shirt/Bobblehead","Shirt/Bobblehead")
group.symbols <- c(21,24)
group.colors <- c("black","black") 
group.fill <- c("blue","green")  
xyplot(predict_attend/1000 ~ attend/1000 | training_test, 
       data = dodgers.plotting.frame8, groups = shirt, cex = 2,
       pch = group.symbols, col = group.colors, fill = group.fill, 
       layout = c(2, 1), xlim = c(20,85), ylim = c(20,85), 
       aspect=1, type = c("p","g"),
       panel=function(x,y, ...)
       {panel.xyplot(x,y,...)
         panel.segments(25,25,80,80,col="black",cex=2)
       },
       strip=function(...) strip.default(..., style=1),
       xlab = "Actual Attendance (thousands)", 
       ylab = "Predicted Attendance (thousands)",
       key = list(space = "top", 
                  text = list(rev(group.labels),col = rev(group.colors)),
                  points = list(pch = rev(group.symbols), 
                                col = rev(group.colors),
                                fill = rev(group.fill))))            

# use the full data set to obtain an estimate of the increase in
# attendance due to CAP, controlling for other factors 
my.model.fit8 <- lm(my.model8, data = dodgers)  # use all available data
print(summary(my.model.fit8))
# tests statistical significance of the bobblehead promotion
# type I anova computes sums of squares for sequential tests
print(anova(my.model.fit8))  

cat("\n","Estimated Effect of Shirt/Bobblehead Promotion on Attendance: ",
    round(my.model.fit8$coefficients[length(my.model.fit8$coefficients)],
          digits = 0),"\n",sep="")

# standard graphics provide diagnostic plots
plot(my.model.fit8)

# additional model diagnostics drawn from the car package
library(car)
residualPlots(my.model.fit8)
marginalModelPlots(my.model.fit8)
print(outlierTest(my.model.fit8))

# Suggestions for the student:
# Examine regression diagnostics for the fitted model.
# Examine other linear predictors and other explanatory variables.
# See if you can improve upon the model with variable transformations.


##Multiple Giveaways: Linear Model Cap + Fireworks ###################################################

# specify a simple model with shirts entered last
my.model9 <- {attend ~ ordered_month + ordered_day_of_week + cap + fireworks}

# fit the model to the training set
train.model.fit9 <- lm(my.model9, data = dodgers.train)
# summary of model fit to the training set
print(summary(train.model.fit9))
# training set predictions from the model fit to the training set
dodgers.train$predict_attend <- predict(train.model.fit9) 

# test set predictions from the model fit to the training set
dodgers.test$predict_attend <- predict(train.model.fit9, 
                                       newdata = dodgers.test)

# compute the proportion of response variance
# accounted for when predicting out-of-sample
cat("\n","Proportion of Test Set Variance Accounted for: ",
    round((with(dodgers.test,cor(attend,predict_attend)^2)),
          digits=3),"\n",sep="")

# merge the training and test sets for plotting
dodgers.plotting.frame9 <- rbind(dodgers.train,dodgers.test)

# generate predictive modeling visual for management
group.labels <- c("No Shirt/Bobblehead","Shirt/Bobblehead")
group.symbols <- c(21,24)
group.colors <- c("black","black") 
group.fill <- c("blue","green")  
xyplot(predict_attend/1000 ~ attend/1000 | training_test, 
       data = dodgers.plotting.frame9, groups = shirt, cex = 2,
       pch = group.symbols, col = group.colors, fill = group.fill, 
       layout = c(2, 1), xlim = c(20,95), ylim = c(20,95), 
       aspect=1, type = c("p","g"),
       panel=function(x,y, ...)
       {panel.xyplot(x,y,...)
         panel.segments(25,25,90,90,col="black",cex=2)
       },
       strip=function(...) strip.default(..., style=1),
       xlab = "Actual Attendance (thousands)", 
       ylab = "Predicted Attendance (thousands)",
       key = list(space = "top", 
                  text = list(rev(group.labels),col = rev(group.colors)),
                  points = list(pch = rev(group.symbols), 
                                col = rev(group.colors),
                                fill = rev(group.fill))))            

# use the full data set to obtain an estimate of the increase in
# attendance due to CAP, controlling for other factors 
my.model.fit9 <- lm(my.model9, data = dodgers)  # use all available data
print(summary(my.model.fit9))
# tests statistical significance of the bobblehead promotion
# type I anova computes sums of squares for sequential tests
print(anova(my.model.fit9))  

cat("\n","Estimated Effect of Shirt/Bobblehead Promotion on Attendance: ",
    round(my.model.fit9$coefficients[length(my.model.fit9$coefficients)],
          digits = 0),"\n",sep="")

# standard graphics provide diagnostic plots
plot(my.model.fit9)

# additional model diagnostics drawn from the car package
library(car)
residualPlots(my.model.fit9)
marginalModelPlots(my.model.fit9)
print(outlierTest(my.model.fit9))


##Multiple Giveaways: Linear Model Shirt + Fireworks ###################################################

# specify a simple model with shirts entered last
my.model10 <- {attend ~ ordered_month + ordered_day_of_week + shirt + fireworks}

# fit the model to the training set
train.model.fit10 <- lm(my.model10, data = dodgers.train)
# summary of model fit to the training set
print(summary(train.model.fit10))
# training set predictions from the model fit to the training set
dodgers.train$predict_attend <- predict(train.model.fit10) 

# test set predictions from the model fit to the training set
dodgers.test$predict_attend <- predict(train.model.fit10, 
                                       newdata = dodgers.test)

# compute the proportion of response variance
# accounted for when predicting out-of-sample
cat("\n","Proportion of Test Set Variance Accounted for: ",
    round((with(dodgers.test,cor(attend,predict_attend)^2)),
          digits=3),"\n",sep="")

# merge the training and test sets for plotting
dodgers.plotting.frame10 <- rbind(dodgers.train,dodgers.test)

# generate predictive modeling visual for management
group.labels <- c("No Shirt/Bobblehead","Shirt/Bobblehead")
group.symbols <- c(21,24)
group.colors <- c("black","black") 
group.fill <- c("blue","green")  
xyplot(predict_attend/1000 ~ attend/1000 | training_test, 
       data = dodgers.plotting.frame10, groups = shirt, cex = 2,
       pch = group.symbols, col = group.colors, fill = group.fill, 
       layout = c(2, 1), xlim = c(20,105), ylim = c(20,105), 
       aspect=1, type = c("p","g"),
       panel=function(x,y, ...)
       {panel.xyplot(x,y,...)
         panel.segments(25,25,100,100,col="black",cex=2)
       },
       strip=function(...) strip.default(..., style=1),
       xlab = "Actual Attendance (thousands)", 
       ylab = "Predicted Attendance (thousands)",
       key = list(space = "top", 
                  text = list(rev(group.labels),col = rev(group.colors)),
                  points = list(pch = rev(group.symbols), 
                                col = rev(group.colors),
                                fill = rev(group.fill))))            

# use the full data set to obtain an estimate of the increase in
# attendance due to CAP, controlling for other factors 
my.model.fit10 <- lm(my.model10, data = dodgers)  # use all available data
print(summary(my.model.fit10))
# tests statistical significance of the bobblehead promotion
# type I anova computes sums of squares for sequential tests
print(anova(my.model.fit10))  

cat("\n","Estimated Effect of Shirt/Bobblehead Promotion on Attendance: ",
    round(my.model.fit10$coefficients[length(my.model.fit10$coefficients)],
          digits = 0),"\n",sep="")

# standard graphics provide diagnostic plots
plot(my.model.fit10)

# additional model diagnostics drawn from the car package
library(car)
residualPlots(my.model.fit10)
marginalModelPlots(my.model.fit10)
print(outlierTest(my.model.fit10))



## Dodgers Random Forest:150 #############################################
#rm(list = ls())
# setwd("C:/Users/stlgonzb/Desktop/")
# # read in data and create a data frame called dodgers
# dodgers <- read.csv("dodgers.csv")
# attach(dodgers)
# print(str(dodgers))

par(mfrow=c(1,1))
library(tree)
dodgersfortree2<-dodgers[,-c(2,5,16)]
names(dodgers)
library(randomForest)
attach(dodgersfortree2)

lstMSEs=numeric()
set.seed(1)
maxnumpreds=ncol(dodgersfortree2)-1
maxnumtrees=150

for(numpreds in 1:maxnumpreds){
  for(numtrees in 1:maxnumtrees){
    
    nrow(dodgers)
    train=sample(1:nrow(dodgersfortree2),nrow(dodgersfortree2)/2)
    
    
    model.bagged=randomForest(attend~.,data = dodgersfortree2,subset = train,mtry=numpreds,ntree=numtrees,importance=TRUE)
    
    
    
    pred.vals.bagged=predict(model.bagged,newdata = dodgersfortree2[-train])
    testvals=dodgers$attend[-train]
    mse=mean((pred.vals.bagged - testvals)^2)
    lstMSEs=rbind(lstMSEs,mse)
    print(paste("     Processed Trees:",numtrees))
  }
  print(paste("     Processed Predictors:",numpreds))
}
title(main = "Dodgers Decision Tree 12.73% Variance Explained
      Max Trees = 500",outer = TRUE,line=-1)
matMSEs=matrix(lstMSEs,nrow = maxnumpreds,ncol=maxnumtrees)

min(lstMSEs)
min(matMSEs)
lstMSEs

loc=which(matMSEs==min(matMSEs),arr.ind=TRUE)
print(paste("The optimal configuration is",loc[1],"predictors and",loc[2], "trees"))
length(lstMSEs)
print(paste("        Processed Trees:", numtrees))
print(paste("        Processed Predictors:",numpreds))
matMSEs[loc[1],loc[2]]



which(matMSEs==min(matMSEs),arr.ind = TRUE)
importance(model.bagged)
tree.dodgers2=tree(attend~.,data = dodgersfortree2)
plot(model.bagged)
plot(tree.dodgers2)
text(tree.dodgers2,pretty = 0)
varImpPlot(model.bagged)
model.bagged
min(lstMSEs)
summary(tree.dodgers2)



## Dodgers Random Forest:500 #############################################
#rm(list = ls())
# setwd("C:/Users/stlgonzb/Desktop/")
# # read in data and create a data frame called dodgers
# dodgers <- read.csv("dodgers.csv")
# attach(dodgers)
# print(str(dodgers))

par(mfrow=c(1,1))
library(tree)
dodgersfortree3<-dodgers[,-c(2,5,16)]
names(dodgers)
library(randomForest)
attach(dodgersfortree3)

lstMSEs=numeric()
set.seed(1)
maxnumpreds=ncol(dodgersfortree3)-1
maxnumtrees=500

for(numpreds in 1:maxnumpreds){
  for(numtrees in 1:maxnumtrees){
    
    nrow(dodgers)
    train=sample(1:nrow(dodgersfortree3),nrow(dodgersfortree3)/2)
    
    
    model.bagged=randomForest(attend~.,data = dodgersfortree3,subset = train,mtry=numpreds,ntree=numtrees,importance=TRUE)
    
    
    
    pred.vals.bagged=predict(model.bagged,newdata = dodgersfortree3[-train])
    testvals=dodgers$attend[-train]
    mse=mean((pred.vals.bagged - testvals)^2)
    lstMSEs=rbind(lstMSEs,mse)
    print(paste("     Processed Trees:",numtrees))
  }
  print(paste("     Processed Predictors:",numpreds))
}
title(main = "Dodgers Decision Tree 12.73% Variance Explained
      Max Trees = 500",outer = TRUE,line=-1)
matMSEs=matrix(lstMSEs,nrow = maxnumpreds,ncol=maxnumtrees)

min(lstMSEs)
min(matMSEs)
lstMSEs

loc=which(matMSEs==min(matMSEs),arr.ind=TRUE)
print(paste("The optimal configuration is",loc[1],"predictors and",loc[2], "trees"))
length(lstMSEs)
print(paste("        Processed Trees:", numtrees))
print(paste("        Processed Predictors:",numpreds))
matMSEs[loc[1],loc[2]]



which(matMSEs==min(matMSEs),arr.ind = TRUE)
importance(model.bagged)
tree.dodgers3=tree(attend~.,data = dodgersfortree3)
plot(model.bagged)
plot(tree.dodgers3)
text(tree.dodgers3,pretty = 0)
varImpPlot(model.bagged)
model.bagged
min(lstMSEs)
summary(tree.dodgers3)

## Dodgers Random Forest:1000 #############################################
#rm(list = ls())
# setwd("C:/Users/stlgonzb/Desktop/")
# # read in data and create a data frame called dodgers
# dodgers <- read.csv("dodgers.csv")
# attach(dodgers)
# print(str(dodgers))

par(mfrow=c(1,1))
library(tree)
dodgersfortree<-dodgers[,-c(2,5,16)]
names(dodgers)
library(randomForest)
attach(dodgersfortree)

lstMSEs=numeric()
set.seed(1)
maxnumpreds=ncol(dodgersfortree)-1
maxnumtrees=1000

for(numpreds in 1:maxnumpreds){
  for(numtrees in 1:maxnumtrees){
    
    nrow(dodgers)
    train=sample(1:nrow(dodgersfortree),nrow(dodgersfortree)/2)
    
    
    model.bagged=randomForest(attend~.,data = dodgersfortree,subset = train,mtry=numpreds,ntree=numtrees,importance=TRUE)
    
    
    
    pred.vals.bagged=predict(model.bagged,newdata = dodgersfortree[-train])
    testvals=dodgers$attend[-train]
    mse=mean((pred.vals.bagged - testvals)^2)
    lstMSEs=rbind(lstMSEs,mse)
    print(paste("     Processed Trees:",numtrees))
  }
  print(paste("     Processed Predictors:",numpreds))
}
title(main = "Dodgers Decision Tree 12.73% Variance Explained
      Max Trees = 500",outer = TRUE,line=-1)
matMSEs=matrix(lstMSEs,nrow = maxnumpreds,ncol=maxnumtrees)

min(lstMSEs)
min(matMSEs)
lstMSEs

loc=which(matMSEs==min(matMSEs),arr.ind=TRUE)
print(paste("The optimal configuration is",loc[1],"predictors and",loc[2], "trees"))
length(lstMSEs)
print(paste("        Processed Trees:", numtrees))
print(paste("        Processed Predictors:",numpreds))
matMSEs[loc[1],loc[2]]



which(matMSEs==min(matMSEs),arr.ind = TRUE)
importance(model.bagged)
tree.dodgers1=tree(attend~.,data = dodgersfortree)
plot(model.bagged)
plot(tree.dodgers1)
text(tree.dodgers1,pretty = 0)
varImpPlot(model.bagged)
model.bagged
min(lstMSEs)
summary(tree.dodgers1)


````
