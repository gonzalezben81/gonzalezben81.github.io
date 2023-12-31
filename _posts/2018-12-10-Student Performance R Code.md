````
##Student Performance Dataset-Ben Gonzalez ##########################
## Learning Techniques Utilized-Simple Linear Regression, Multiple Linear Regression,
## Plot Functions, Validation Set Approaches, Subset Selection Methods, Tree-Based Approaches
## Generalized Additive Models, Classification was not able to be utilized due to the outcome
## variable being continous 

Student_Performance_Ben_Gonzalez <-read.csv("Student_Performance_Ben_Gonzalez.csv",header = T,sep = ";")
attach(Student_Performance_Ben_Gonzalez)
fix(Student_Performance_Ben_Gonzalez)
names(Student_Performance_Ben_Gonzalez)
summary(Student_Performance_Ben_Gonzalez)


##Student Performance Plots################################################################

##Plots for Student Performance
plot(Mjob,G3)
plot(health,G3)
plot(absences,G3)
plot(guardian,G3)
plot(traveltime,G3)
plot(internet,G3)
plot(studytime,G3)
plot(studytime,G1)
plot(studytime,G2)
plot(romantic,G3)
plot(failures,G3)
plot(failures,G1)
plot(failures,G2)
plot(goout,G3)
plot(Walc,G3)
plot(Dalc,G3)
plot(G1,G3)

##Student Performance Plots with Labels##################################

#Plots for Student Performance Dataset with labels
plot(schoolsup,G3,xlab="Extra Educational Support",ylab="Final Grade")
plot(famsup,G3,xlab="Family Educational Support",ylab="Final Grade")
plot(activities,G3,xlab="Extracurricular Activities",ylab="Final Grade")
plot(nursery,G3,xlab="Attended Nursery School",ylab="Final Grade")
plot(Dalc,G3,xlab="Workday Alcohol Consumption 1-Very Low   5-Very High",ylab="Final Grade")
plot(famrel,G3,xlab="Quality of Family Relationships",ylab="Final Grade",main = "1=Very Bad   5=Excellent")
plot(goout,G3,xlab="Go Out With Friends",ylab="Final Grade")
plot(Pstatus,G3,xlab="Parental Cohabitation",ylab="Final Grade")
plot(Medu,G3,xlab="Mother's Education",ylab="Final Grade")
plot(Fedu,G3,xlab="Father's Education",ylab="Final Grade")
plot(age,G3,xlab="Age",ylab="Final Grade")
plot(internet,G3,xlab="Internet Available to Student",ylab="Final Grade",col="blue")
plot(Mjob,G3,xlab="Mother's Job: At-Home, Health, Other, Services, Teacher",ylab="Final Grade (G3)", main="Mother's Job and Final Grade",col="light green")
summary(Mjob)



##Student Performance Dataset Simple Linear Regression Models#############################

## Simple Linear Regression
schoolmodel.1=lm(G3~school,data = Student_Performance_Ben_Gonzalez)
schoolmodel.1
schoolmodel.2=lm(G3~sex,data = Student_Performance_Ben_Gonzalez)
schoolmodel.2
schoolmodel.3=lm(G3~address,data = Student_Performance_Ben_Gonzalez)
schoolmodel.3
schoolmodel.4=lm(G3~famsize,data = Student_Performance_Ben_Gonzalez)
schoolmodel.4
schoolmodel.5=lm(G3~Pstatus,data = Student_Performance_Ben_Gonzalez)
schoolmodel.5
schoolmodel.6=lm(G3~Medu,data = Student_Performance_Ben_Gonzalez)
schoolmodel.6
schoolmodel.7=lm(G3~Fedu,data = Student_Performance_Ben_Gonzalez)
schoolmodel.7
schoolmodel.8=lm(G3~Mjob,data = Student_Performance_Ben_Gonzalez)
schoolmodel.8
schoolmodel.9=lm(G3~Fjob,data = Student_Performance_Ben_Gonzalez)
schoolmodel.9
schoolmodel.10=lm(G3~reason,data = Student_Performance_Ben_Gonzalez)
schoolmodel.10
schoolmodel.11=lm(G3~guardian,data = Student_Performance_Ben_Gonzalez)
schoolmodel.11
schoolmodel.12=lm(G3~traveltime,data = Student_Performance_Ben_Gonzalez)
schoolmodel.12
schoolmodel.13=lm(G3~studytime,data = Student_Performance_Ben_Gonzalez)
schoolmodel.13
schoolmodel.14=lm(G3~failures,data = Student_Performance_Ben_Gonzalez)
schoolmodel.14
schoolmodel.15=lm(G3~schoolsup,data = Student_Performance_Ben_Gonzalez)
schoolmodel.15
schoolmodel.16=lm(G3~famsup,data = Student_Performance_Ben_Gonzalez)
schoolmodel.16
schoolmodel.17=lm(G3~paid,data = Student_Performance_Ben_Gonzalez)
schoolmodel.17
schoolmodel.18=lm(G3~activities,data = Student_Performance_Ben_Gonzalez)
schoolmodel.18
schoolmodel.19=lm(G3~nursery,data = Student_Performance_Ben_Gonzalez)
schoolmodel.19
schoolmodel.20=lm(G3~higher,data = Student_Performance_Ben_Gonzalez)
schoolmodel.20
schoolmodel.21=lm(G3~internet,data = Student_Performance_Ben_Gonzalez)
schoolmodel.21
schoolmodel.22=lm(G3~romantic,data = Student_Performance_Ben_Gonzalez)
schoolmodel.22
schoolmodel.23=lm(G3~famrel,data = Student_Performance_Ben_Gonzalez)
schoolmodel.23
schoolmodel.24=lm(G3~freetime,data = Student_Performance_Ben_Gonzalez)
schoolmodel.24
schoolmodel.25=lm(G3~goout,data = Student_Performance_Ben_Gonzalez)
schoolmodel.25
schoolmodel.26=lm(G3~Dalc,data = Student_Performance_Ben_Gonzalez)
schoolmodel.26
schoolmodel.27=lm(G3~Walc,data = Student_Performance_Ben_Gonzalez)
schoolmodel.27
schoolmodel.28=lm(G3~health,data = Student_Performance_Ben_Gonzalez)
schoolmodel.28
schoolmodel.29=lm(G3~absences,data = Student_Performance_Ben_Gonzalez)
schoolmodel.29
schoolmodel.30=lm(G3~G1,data = Student_Performance_Ben_Gonzalez)
schoolmodel.30
schoolmodel.31=lm(G3~G2,data = Student_Performance_Ben_Gonzalez)
schoolmodel.31
schoolmodel.32=lm(G3~age,data = Student_Performance_Ben_Gonzalez)
schoolmodel.32


## Student Performance Multiple Linear Regression Models ##################################
schoolmodelmultiple1.1=lm(G3~.,data = Student_Performance_Ben_Gonzalez)
summary(schoolmodelmultiple1.1)
studentmodel.1=lm(G3~.,data = Student_Performance_Ben_Gonzalez)
summary(studentmodel.1)
studenmodel.2=lm(G3~Fjob+Mjob+G2+G1+absences+famrel+activities+age,data = Student_Performance_Ben_Gonzalez)
summary(studenmodel.2)
studentmodel.3=lm(G3~G2+G1+absences+age+activities+Mjob,data = Student_Performance_Ben_Gonzalez)
summary(studentmodel.3)

## Student Perfromance Resampling Methods #################################################
#Cross-Validation Approach
set.seed(1)
dim(Student_Performance_Ben_Gonzalez)
train=sample(395,185)
lmcv.fit1=lm(G3~.,data = Student_Performance_Ben_Gonzalez,subset = train)
mean((G3-predict(lmcv.fit1,Student_Performance_Ben_Gonzalez))[-train]^2)

#Leave-One-Out-Cross-Validation
glm.fit=glm(G3~.,Student_Performance_Ben_Gonzalez)
coef(glm.fit)
library(boot)
glm.fit=glm(G3~.,data = Student_Performance_Ben_Gonzalez)
cv.err=cv.glm(Student_Performance_Ben_Gonzalez,glm.fit)
cv.err$delta


## Student Performance K-Fold Cross Validation ##############################################
cv.error=rep(0,5)
for (i in 1:5){
  glm.fit=glm(G3~poly(G2,i),data = Student_Performance_Ben_Gonzalez)
  cv.error[i]=cv.glm(Student_Performance_Ben_Gonzalez,glm.fit)$delta[1]
}
cv.error



###Student Performance Dataset Subset Non-Linear Approaches########################################

##Subset selection including forward selection modeling for Student Performance Dataset #############
library(leaps)

studentmodel.1=regsubsets(G3~.,data = Student_Performance_Ben_Gonzalez)
studentmodel.2=regsubsets(G3~.,data = Student_Performance_Ben_Gonzalez,nvmax = 32,method = "forward")
studentmodel.3=regsubsets(G3~.,data = Student_Performance_Ben_Gonzalez,nvmax = 32,method = "backward")

#Student Model 1
student.summary1=summary(studentmodel.1)
student.summary1
student.summary1$rsq
student.summary1$adjr2
student.summary1$bic
which.max(student.summary1$rss)
which.min(student.summary1$bic)
which.max(student.summary1$adjr2)

#Student Model 2
student.summary2=summary(studentmodel.2)
student.summary2
student.summary2$rsq
student.summary2$adjr2
which.max(student.summary2$adjr2)
student.summary2$rss
student.summary2$bic
which.min(student.summary2$bic)
which.max(student.summary2$adjr2)

#Student Model 3
student.summary3=summary(studentmodel.3)
student.summary3
student.summary3$rsq
student.summary3$adjr2
which.max(student.summary3$adjr2)
student.summary3$rss
student.summary3$bic
which.min(student.summary3$bic)
which.max(student.summary3$adjr2)

#Student Summary Model  1
student.summary1=summary(studentmodel.1)
student.summary1
student.summary1$rsq
student.summary1$adjr2
student.summary1$rss
which.max(student.summary1$adjr2)
student.summary1$bic
which.min(student.summary1$bic)
plot(student.summary1$bic,xlab = "Number of Variables",ylab = "Student Model 1 BIC",type = "o")
points(5,student.summary1$bic[5],col="blue",cex=2,pch=20)
which.max(student.summary1$adjr2)
plot(student.summary1$adjr2,xlab = "Number of Variables",ylab = "Student Model 1 Adjusted R-Squared",type = "o")
points(8,student.summary1$adjr2[8],col="blue",cex=2,pch=20)
which.min(student.summary1$rss)
plot(student.summary1$rss,xlab = "Number of Variables",ylab = "Student Model 1 RSS",type = "o")
points(8,student.summary1$rss[8],col="blue",cex=2,pch=20)
coef(studentmodel.2,8)

#Student Summary Model 2
student.summary2=summary(studentmodel.2)
student.summary2
student.summary2$rsq
student.summary2$adjr2
student.summary2$rss
which.max(student.summary2$adjr2)
student.summary2$bic
which.min(student.summary2$bic)
plot(student.summary2$bic,xlab = "Number of Variables",ylab = "Student Model 2 BIC",type = "o")
points(5,student.summary2$bic[5],col="blue",cex=2,pch=20)
which.max(student.summary2$adjr2)
plot(student.summary2$adjr2,xlab = "Number of Variables",ylab = "Student Model 2 Adjusted R-Squared",type = "o")
points(13,student.summary2$adjr2[13],col="blue",cex=2,pch=20)
which.min(student.summary2$rss)
plot(student.summary2$rss,xlab = "Number of Variables",ylab = "Student Model 2 RSS",type = "o")
points(32,student.summary2$rss[32],col="blue",cex=2,pch=20)
coef(studentmodelfit.2,5)

#Student Summary Model 3
student.summary3=summary(studentmodel.3)
student.summary3
student.summary3$rsq
student.summary3$adjr2
student.summary3$rss
which.max(student.summary3$adjr2)
student.summary3$bic
which.min(student.summary3$bic)
plot(student.summary3$bic,xlab = "Number of Variables",ylab = "Student Model 3 BIC",type = "o")
points(5,student.summary3$bic[5],col="blue",cex=2,pch=20)
which.max(student.summary3$adjr2)
plot(student.summary3$adjr2,xlab = "Number of Variables",ylab = "Student Model 3 Adjusted R-Squared",type = "o")
points(13,student.summary3$adjr2[13],col="blue",cex=2,pch=20)
which.min(student.summary3$rss)
plot(student.summary3$rss,xlab = "Number of Variables",ylab = "Student Model 3 RSS",type = "o")
points(32,student.summary3$rss[32],col="blue",cex=2,pch=20)
coef(studentmodel.3,5)


##Student Performance Generalized Additive Models ######################
library(gam)
train=sample(c(TRUE,FALSE),nrow(Student_Performance_Ben_Gonzalez),rep=TRUE)
test=-train
## Student Performance GAM Spline Based Approach
gam.studentperformance1=gam(G3~activities+s(age,2)+s(famrel,2)+s(absences,2)+s(G1,2)+s(G2,2),data = Student_Performance_Ben_Gonzalez)
plot(gam.studentperformance1,se=TRUE,col="red")
summary(gam.studentperformance1)

#Student Performance GAM with Polynomial Regression to the 3rd Power
gam.studentperformancelm2=lm(G3~activities+poly(age,2)+poly(famrel,2)+poly(absences,2)+poly(G1,2)+G2,data = Student_Performance_Ben_Gonzalez)
summary(gam.studentperformancelm2)
studentperformancelm2
plot(studentperformancelm2)
studentperformancelm2

## Student Performance GAM with Polynomial Regression to the 3rd Power
gam.studentperformance3=lm(G3~activities+poly(age,3)+poly(famrel,3)+poly(absences,3)+poly(G1,3)+G2,data = Student_Performance_Ben_Gonzalez)
summary(gam.studentperformance3)

gam.studentperformance4=lm(G3~activities+poly(age,4)+poly(famrel,4)+poly(absences,4)+poly(G1,4)+G2,data = Student_Performance_Ben_Gonzalez)
summary(gam.studentperformance4)

gam.studentperformance5=gam(G3~activities+poly(age,7)+famrel+poly(absences,4)+G1+G2,data = Student_Performance_Ben_Gonzalez)
gam.studentperformance6=gam(G3~activities+poly(age,7)+famrel+poly(absences,4)+G1+G2,data = Student_Performance_Ben_Gonzalez)

anova(gam.studentperformance1,gam.studentperformance3,gam.studentperformance4,gam.studentperformance5)
gam.studentperformance5
plot.gam(gam.studentperformance5,se=TRUE,col="blue")

anova(gam.studentperformance1,gam.st)
#Nonlinear relationships for Age
fit1a=lm(G3~poly(age,1,raw = T),data = Student_Performance_Ben_Gonzalez)
fit2a=lm(G3~poly(age,2,raw = T),data = Student_Performance_Ben_Gonzalez)
fit3a=lm(G3~poly(age,3,raw = T),data = Student_Performance_Ben_Gonzalez)
fit4a=lm(G3~poly(age,4,raw = T),data = Student_Performance_Ben_Gonzalez)
fit5a=lm(G3~poly(age,5,raw = T),data = Student_Performance_Ben_Gonzalez)
fit6a=lm(G3~poly(age,6,raw = T),data = Student_Performance_Ben_Gonzalez)
fit7a=lm(G3~poly(age,7,raw = T),data = Student_Performance_Ben_Gonzalez)
fit8a=lm(G3~poly(age,8,raw = T),data = Student_Performance_Ben_Gonzalez)
anova(fit1a,fit2a,fit3a,fit4a,fit5a,fit6a,fit7a,fit8a)
plot(age,G3)

#Nonlinear relationships for Famrel
fit1r=lm(G3~poly(famrel,1,raw = T),data = Student_Performance_Ben_Gonzalez)
fit2r=lm(G3~poly(famrel,2,raw = T),data = Student_Performance_Ben_Gonzalez)
fit3r=lm(G3~poly(famrel,3,raw = T),data = Student_Performance_Ben_Gonzalez)
fit4r=lm(G3~poly(famrel,4,raw = T),data = Student_Performance_Ben_Gonzalez)
fit5r=lm(G3~poly(famrel,5,raw = T),data = Student_Performance_Ben_Gonzalez)
fit6r=lm(G3~poly(famrel,6,raw = T),data = Student_Performance_Ben_Gonzalez)
fit7r=lm(G3~poly(famrel,7,raw = T),data = Student_Performance_Ben_Gonzalez)
fit8r=lm(G3~poly(famrel,8,raw = T),data = Student_Performance_Ben_Gonzalez)
anova(fit1r,fit2r,fit3r,fit4r,fit5r,fit6r,fit7r,fit8r)
plot(famrel,G3)

#Nonlinear relationships for Absences
fit1b=lm(G3~poly(absences,1,raw = T),data = Student_Performance_Ben_Gonzalez)
fit2b=lm(G3~poly(absences,2,raw = T),data = Student_Performance_Ben_Gonzalez)
fit3b=lm(G3~poly(absences,3,raw = T),data = Student_Performance_Ben_Gonzalez)
fit4b=lm(G3~poly(absences,4,raw = T),data = Student_Performance_Ben_Gonzalez)
fit5b=lm(G3~poly(absences,5,raw = T),data = Student_Performance_Ben_Gonzalez)
fit6b=lm(G3~poly(absences,6,raw = T),data = Student_Performance_Ben_Gonzalez)
fit7b=lm(G3~poly(absences,7,raw = T),data = Student_Performance_Ben_Gonzalez)
fit8b=lm(G3~poly(absences,8,raw = T),data = Student_Performance_Ben_Gonzalez)
anova(fit1b,fit2b,fit3b,fit4b,fit5b,fit6b,fit7b,fit8b)
plot(absences,G3)

#Nonlinear relationships for G1
fit1g=lm(G3~poly(G1,1,raw = T),data = Student_Performance_Ben_Gonzalez)
fit2g=lm(G3~poly(G1,2,raw = T),data = Student_Performance_Ben_Gonzalez)
fit3g=lm(G3~poly(G1,3,raw = T),data = Student_Performance_Ben_Gonzalez)
fit4g=lm(G3~poly(G1,4,raw = T),data = Student_Performance_Ben_Gonzalez)
fit5g=lm(G3~poly(G1,5,raw = T),data = Student_Performance_Ben_Gonzalez)
fit6g=lm(G3~poly(G1,6,raw = T),data = Student_Performance_Ben_Gonzalez)
fit7g=lm(G3~poly(G1,7,raw = T),data = Student_Performance_Ben_Gonzalez)
fit8g=lm(G3~poly(G1,8,raw = T),data = Student_Performance_Ben_Gonzalez)
anova(fit1g,fit2g,fit3g,fit4g,fit5g,fit6g,fit7g,fit8g)
plot(G1,G3)

####Student Performance Dataset Tree Based Approaches########################################


## Student Performance Random Forest #############################################
library(tree)
names(Student_Performance_Ben_Gonzalez)
library(randomForest)
attach(Student_Performance_Ben_Gonzalez)

lstMSEs=numeric()
set.seed(1)
maxnumpreds=ncol(Student_Performance_Ben_Gonzalez)-1
maxnumtrees=10

for(numpreds in 1:maxnumpreds){
  for(numtrees in 1:maxnumtrees){
    
    nrow(Student_Performance_Ben_Gonzalez)
    train=sample(1:nrow(Student_Performance_Ben_Gonzalez),nrow(Student_Performance_Ben_Gonzalez)/2)
    
    
    model.bagged=randomForest(G3~.,data = Student_Performance_Ben_Gonzalez,subset = train,mtry=numpreds,ntree=numtrees,importance=TRUE)
    
    
    
    pred.vals.bagged=predict(model.bagged,newdata = Student_Performance_Ben_Gonzalez[-train])
    testvals=Student_Performance_Ben_Gonzalez$G3[-train]
    mse=mean((pred.vals.bagged - testvals)^2)
    lstMSEs=rbind(lstMSEs,mse)
    print(paste("     Processed Trees:",numtrees))
  }
  print(paste("     Processed Predictors:",numpreds))
}

matMSEs=matrix(lstMSEs,nrow = maxnumpreds,ncol=maxnumtrees)


print(paste("The optimal configuration is",loc[1],"predictors and",loc[2], "trees"))
length(lstMSEs)
list(lstMSEs)

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
tree.student1=tree(G3~.,data = Student_Performance_Ben_Gonzalez)
plot(model.bagged)
plot(tree.student1)
text(tree.student1,pretty = 0)
varImpPlot(model.bagged)
model.bagged
min(lstMSEs)

# Student Performance Random Forest with K-Fold CV Approach###########################

library(randomForest)
library(tree)
attach(Student_Performance_Ben_Gonzalez)
lstMSEs <- numeric()
set.seed(1)
maxnumpreds <- ncol(Student_Performance_Ben_Gonzalez) - 1
maxnumtrees <- 10

samplesize <- dim(Student_Performance_Ben_Gonzalez)[1] 
numfolds <- 10

quotient <- samplesize %/% numfolds 
remainder <- samplesize %% numfolds 


lstsizes <- rep(quotient,numfolds)
if (remainder > 0) {
  for (i in 1:remainder){
    lstsizes[i] <- lstsizes[i]+1
  }
}
start <- 1

for(numpreds in 1:maxnumpreds){
  for(numtrees in 1:maxnumtrees){
    train <- sample(1:nrow(Student_Performance_Ben_Gonzalez), nrow(Student_Performance_Ben_Gonzalez)/2) 
    model.bagged.2 <- randomForest(G3~.,data=Student_Performance_Ben_Gonzalez,subset=train,mtry=numpreds,ntree=numtrees,importance=TRUE) 
    
    pred.vals.bagged <- predict(model.bagged.2, newdata=Student_Performance_Ben_Gonzalez[-train,])
    testvals <- Student_Performance_Ben_Gonzalez$G3[-train]
    mse <- mean((pred.vals.bagged - testvals)^2)
    lstMSEs <- rbind(lstMSEs, mse)
    
    print(paste("    Processed trees:", numtrees))
  }
  print(paste("Processed predictors:", numpreds))
}

matMSEs <- matrix(lstMSEs,nrow=maxnumpreds,ncol=maxnumtrees)
location <- which(matMSEs == min(matMSEs), arr.ind=TRUE)
print(paste("Optimal number of predictors:", location[1],
            "  optimal number of trees:", location[2]))
tree.student2=tree(G3~.,data = Student_Performance_Ben_Gonzalez)
plot(model.bagged.2)
plot(tree.student2)
text(tree.student2,pretty = 0)
varImpPlot(model.bagged.2)
importance(model.bagged.2)
model.bagged.2
min(lstMSEs)

## Student Performance Boosting K-Fold CV Approach ########################################

library(gbm)
library(ISLR)
library(randomForest)
attach(Student_Performance_Ben_Gonzalez)
set.seed(1)
lstMSEs <- numeric()

samplesize <- dim(Student_Performance_Ben_Gonzalez)[1] 
numfolds <- 10

quotient <- samplesize %/% numfolds 
remainder <- samplesize %% numfolds 


lstsizes <- rep(quotient,numfolds)
if (remainder > 0) {
  for (i in 1:remainder){
    lstsizes[i] <- lstsizes[i]+1
  }
}
start <- 1
maxnumtrees <- 10
maxinteractiondepth <- 6


for(numtrees in 1:maxnumtrees){
  for(intdepth in 1:maxinteractiondepth)
  {
    
    
    train <- sample(1:nrow(Student_Performance_Ben_Gonzalez), nrow(Student_Performance_Ben_Gonzalez)/2)
    
    
    model.boosted.studentcv.model <- gbm(G3~.,
                                         data=Student_Performance_Ben_Gonzalez[train, ],
                                         distribution="gaussian",
                                         n.trees=numtrees,
                                         interaction.depth=intdepth)
    
    
    
    pred.vals.boosted.studentcv.model <- predict(model.boosted.studentcv.model,
                                                 newdata=Student_Performance_Ben_Gonzalez[-train,],
                                                 n.trees=numtrees)
    
    testvals <- Student_Performance_Ben_Gonzalez$G3[-train]
    
    mse <- mean((pred.vals.boosted.studentcv.model - testvals)^2)
    
    lstMSEs <- rbind(lstMSEs, mse)
    
    print(paste("      Processed depth:", intdepth))
  }
  print(paste("Processed trees:", numtrees))
}

matMSEs <- matrix(lstMSEs,nrow=maxnumtrees,ncol=maxinteractiondepth)


location.best <- which(matMSEs == min(matMSEs), arr.ind=TRUE)


print(paste("Optimal number of trees:", location.best[1],"  optimal interaction depth:", location.best[2]))


location.worst <- which(matMSEs == max(matMSEs), arr.ind=TRUE)


print(paste("Optimal number of trees:", location.worst[1],"  optimal interaction depth:", location.worst[2]))


summary(model.boosted.studentcv.model)
model.boosted.studentcv.model
min(lstMSEs)

## Student Performance Linear Model K-Fold CV Approach ####################################

library(ISLR)
names(Student_Performance_Ben_Gonzalez)
attach(Student_Performance_Ben_Gonzalez)

lstMSEs=numeric()
set.seed(1)
maxnumpreds=ncol(Student_Performance_Ben_Gonzalez)-1
maxnumtrees=10
samplesize <- dim(Student_Performance_Ben_Gonzalez)[1] 
numfolds <- 10

quotient <- samplesize %/% numfolds
remainder <- samplesize %% numfolds 


lstsizes <- rep(quotient,numfolds)
if (remainder > 0) {
  for (i in 1:remainder){
    lstsizes[i] <- lstsizes[i]+1
  }
}

for(numpreds in 1:maxnumpreds){
  for(numtrees in 1:maxnumtrees){
    
    nrow(College)
    train=sample(1:nrow(Student_Performance_Ben_Gonzalez),nrow(Student_Performance_Ben_Gonzalez)/2)
    
    
    model.linearKFoldCV=lm(G3~.,data = Student_Performance_Ben_Gonzalez,subset = train,mtry=numpreds,ntree=numtrees,importance=TRUE)
    
    
    pred.valskfoldcvlinear.bagged=predict(model.linearKFoldCV,newdata = Student_Performance_Ben_Gonzalez[-train])
    testvals=College$PhD[-train]
    mse=mean((pred.valskfoldcvlinear.bagged - testvals)^2)
    lstMSEs=rbind(lstMSEs,mse)
    print(paste("     Processed Trees:",numtrees))
  }
  print(paste("     Processed Predictors:",numpreds))
}

matMSEs=matrix(lstMSEs,nrow = maxnumpreds,ncol=maxnumtrees)


print(paste("The optimal configuration is",loc[1],"predictors and",loc[2], "trees"))
length(lstMSEs)
list(lstMSEs)

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
summary(model.linearKFoldCV)
model.linearKFoldCV
min(lstMSEs)

## End of Student Performance Dataset Modeling ###################
````
