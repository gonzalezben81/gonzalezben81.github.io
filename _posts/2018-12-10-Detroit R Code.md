````
## Detroit Dataset-Ben Gonzalez #######################################

## Learning Techniques Utilized-Correlation,Simple Linear Regression, Multiple Linear Regression,
## Plot Functions, Validation Set Approaches, Subset Selection Methods, Tree-Based Approaches
## Generalized Additive Models, Classification was not able to be utilized due to the outcome
## variable being continous 

Detroit_Data_Ben_Gonzalez=read.csv("Detroit_Data_Ben_Gonzalez.csv",header = T,na.strings = "?")
attach(Detroit_Data_Ben_Gonzalez)
fix(Detroit_Data_Ben_Gonzalez)
names(Detroit_Data_Ben_Gonzalez)
detroitmultiplemodel.1=lm(HOM~.,data = Detroit_Data_Ben_Gonzalez)
detroitmultiplemodel.2=lm(HOM~UEMP+ASR,data = Detroit_Data_Ben_Gonzalez)
summary(detroitmultiplemodel.2)
summary(detroitmultiplemodel.1)


## Plots for Detroit Dataset ##########################################
#Plot 1
plot(HOM,FTP,xlab = "Homicides",ylab = "Full Time Police", type = "o")
#Plot 2
plot(HOM,UEMP,xlab = "Homicides",ylab = "Unemployment Percentage", type = "o")
#Plot 3
plot(HOM,MAN,xlab = "Homicides",ylab = "Manufacturing Workers", type = "o")
#Plot 4
plot(HOM,LIC,xlab = "Homicides",ylab = "Handgun Licenses per 100,000", type = "o")
#Plot 5
plot(HOM,GR,xlab = "White Males",ylab = "Gun Registrations", type = "o")
#Plot 6
plot(HOM,CLEAR,xlab = "Homicides",ylab = "% Homicides Cleared by Arrests",main="Homicides Cleared by Arrests", type = "o")
#Plot 7
plot(HOM,WM,xlab = "Homicides",ylab = "Number of White Males in Population", type = "o")
#Plot 8
plot(HOM,NMAN,xlab = "Homicides",ylab = "Number of Non-Manufacturing Workers", type = "o")
#Plot 9
plot(HOM,GOV,xlab = "Homicides",ylab = "Number of Government Workers", type = "o")
#Plot 10
plot(HOM,HE,xlab = "Homicides",ylab = "Hourly Earnings", type = "o")
#Plot 11
plot(HOM,WE,xlab = "Homicides",ylab = "Weekly Earnings", type = "o")
#Plot 12
plot(HOM,ACC,xlab = "Homicides",ylab = "Death Rate in Accidents", type = "o")
#Plot 13
plot(HOM,ASR,xlab = "Homicides",ylab = "Number of Assaults", type = "o")


## Correlations for Detroit Dataset ##################################
cor(Detroit_Data_Ben_Gonzalez)
cor(HOM,FTP)
cor(HOM,UEMP)
cor(HOM,MAN)
cor(HOM,LIC)
cor(HOM,GR)
cor(HOM,CLEAR)
cor(HOM,WM)
cor(HOM,NMAN)
cor(HOM,GOV)
cor(HOM,HE)
cor(HOM,WE)
cor(HOM,ACC)
cor(HOM,ASR)


#Simple Linear Regression for Detroit Dataset #########################
lm.fitdetroit1=lm(HOM~FTP,data = Detroit_Data_Ben_Gonzalez)
summary(lm.fitdetroit1)
lm.fitdetroit2=lm(HOM~UEMP,data = Detroit_Data_Ben_Gonzalez)
summary(lm.fitdetroit2)
lm.fitdetroit3=lm(HOM~MAN,data = Detroit_Data_Ben_Gonzalez)
summary(lm.fitdetroit3)
lm.fitdetroit4=lm(HOM~LIC,data = Detroit_Data_Ben_Gonzalez)
summary(lm.fitdetroit4)
lm.fitdetroit5=lm(HOM~GR,data = Detroit_Data_Ben_Gonzalez)
summary(lm.fitdetroit5)
lm.fitdetroit6=lm(HOM~CLEAR,data = Detroit_Data_Ben_Gonzalez)
summary(lm.fitdetroit6)
lm.fitdetroit7=lm(HOM~WM,data = Detroit_Data_Ben_Gonzalez)
summary(lm.fitdetroit7)
lm.fitdetroit8=lm(HOM~NMAN,data = Detroit_Data_Ben_Gonzalez)
summary(lm.fitdetroit8)
lm.fitdetroit9=lm(HOM~GOV,data = Detroit_Data_Ben_Gonzalez)
summary(lm.fitdetroit9)
lm.fitdetroit10=lm(HOM~HE,data = Detroit_Data_Ben_Gonzalez)
summary(lm.fitdetroit10)
lm.fitdetroit11=lm(HOM~WE,data = Detroit_Data_Ben_Gonzalez)
summary(lm.fitdetroit11)
lm.fitdetroit12=lm(HOM~ACC,data = Detroit_Data_Ben_Gonzalez)
summary(lm.fitdetroit12)
lm.fitdetroit13=lm(HOM~ASR,data = Detroit_Data_Ben_Gonzalez)
summary(lm.fitdetroit13)

#The (.) method for multiple linear regression could not be used
#for the Detroit Dataset due to the fact it has more variables than observations
model.1=lm(HOM~.,data = Detroit_Data_Ben_Gonzalez)
summary(model.1)


##Detroit Multiple Linear Regression####################################
detroitlm=lm(HOM~FTP+MAN+LIC+GR+WM+NMAN+GOV+HE+WE+ASR,data = Detroit_Data_Ben_Gonzalez)
summary(detroitlm)
detroitlm2=lm(HOM~NMAN+GOV+HE+WE+ACC+ASR,data = Detroit_Data_Ben_Gonzalez)
summary(detroitlm2)
detroitlm3=lm(HOM~LIC+FTP+GR+HE+WE+NMAN+ASR,data = Detroit_Data_Ben_Gonzalez)
summary(detroitlm3)

## Detroit Subset Model Selection ######################### 
library(leaps)
#Model 1
detroitmodelfit.1=regsubsets(HOM~.,data = Detroit_Data_Ben_Gonzalez,method = "forward")
summary(detroitmodelfit.1)
detroit.summary1=summary(detroitmodelfit.1)
summary(detroit.summary1)
#Model 2
detroitmodelfit.2=regsubsets(HOM~.,data = Detroit_Data_Ben_Gonzalez,nvmax = 12)
detroit.summary2=summary(detroitmodelfit.2)
summary(detroitmodelfit.2)
#Model 3
detroitmodelfit.3=regsubsets(HOM~.,data = Detroit_Data_Ben_Gonzalez,method = "backward")
summary(detroitmodelfit.3)


#Detroit Model  1
detroit.summary1=summary(detroitmodelfit.1)
detroit.summary1
detroit.summary1$rsq
detroit.summary1$adjr2
detroit.summary1$rss
which.max(detroit.summary1$adjr2)
detroit.summary1$bic
which.min(detroit.summary1$bic)
plot(detroit.summary1$bic,xlab = "Number of Variables",ylab = "Detroit Model 1 BIC",type = "o")
points(8,detroit.summary1$bic[8],col="blue",cex=2,pch=20)
which.max(detroit.summary1$adjr2)
plot(detroit.summary2$adjr2,xlab = "Number of Variables",ylab = "Detroit Model 1 Adjusted R-Squared",type = "o")
points(7,detroit.summary1$adjr2[7],col="blue",cex=2,pch=20)
which.min(detroit.summary1$rss)
plot(detroit.summary1$rss,xlab = "Number of Variables",ylab = "Detroit Model 1 RSS",type = "o")
points(8,detroit.summary1$rss[8],col="blue",cex=2,pch=20)
coef(detroitmodelfit.1,8)

#Detroit Model 2
detroit.summary2=summary(detroitmodelfit.2)
detroit.summary2
detroit.summary2$rsq
detroit.summary2$adjr2
which.max(detroit.summary2$adjr2)
detroit.summary2$bic
which.min(detroit.summary2$bic)
plot(detroit.summary2$bic,xlab = "Number of Variables",ylab = "Detroit Model 2 BIC",type = "o")
points(12,student.summary2$bic[12],col="green",cex=2,pch=20)
which.max(detroit.summary2$adjr2)
plot(detroit.summary2$adjr2,xlab = "Number of Variables",ylab = "Detroit Model 2 Adjusted R-Squared",type = "o")
points(11,detroit.summary2$adjr2[11],col="green",cex=2,pch=20)
which.min(detroit.summary2$rss)
plot(detroit.summary2$rss,xlab = "Number of Variables",ylab = " Detroit Model 2 RSS",type = "o")
points(12,detroit.summary2$rss[12],col="green",cex=2,pch=20)
coef(detroitmodelfit.2,12)

#Detroit Model 3
detroit.summary3=summary(detroitmodelfit.3)
detroit.summary3
detroit.summary3$rsq
detroit.summary3$adjr2
which.max(detroit.summary3$adjr2)
detroit.summary3$bic
which.min(detroit.summary3$bic)
plot(detroit.summary3$bic,xlab = "Number of Variables",ylab = "Detroit Model 3 BIC",type = "o")
points(8,detroit.summary3$bic[8],col="green",cex=2,pch=20)
which.max(detroit.summary3$adjr2)
plot(detroit.summary3$adjr2,xlab = "Number of Variables",ylab = "Detroit Model 3 Adjusted R-Squared",type = "o")
points(8,detroit.summary3$adjr2[8],col="green",cex=2,pch=20)
which.min(detroit.summary3$rss)
plot(detroit.summary3$rss,xlab = "Number of Variables",ylab = " Detroit Model 3 RSS",type = "o")
points(8,detroit.summary3$rss[8],col="green",cex=2,pch=20)
coef(detroitmodelfit.3,8)



## Detroit GAM (Generalized Additive Model) Models ############################
library(splines)
install.packages("gam")
library(gam)
## Detroit GAM 1
gam.detroitmodel11=lm(HOM~s(UEMP,2)+s(LIC,1)+WE+s(HE,2)+ASR+s(NMAN,1)+s(MAN,1)+ASR,data = Detroit_Data_Ben_Gonzalez)
anova(gam.detroitmodel11)
summary(gam.detroitmodel11)
plot(gam.detroitmodel11,se=TRUE,col="blue")

## Detroit GAM 2
gam.detroitmodel22=lm(HOM~s(MAN,1)+s(LIC,1)+s(WM,1)+s(NMAN,1)+s(HE,2)+s(WE,2),data = Detroit_Data_Ben_Gonzalez)
anova(gam.detroitmodel22)
plot(gam.detroitmodel22,se=TRUE,col="blue")
summary(gam.detroitmodel22)

## Detroit GAM 3
gam.detroitmodel33=lm(HOM~s(FTP,2)+s(LIC,1)+s(GR,1)+s(NMAN,1)+s(GOV,1)+s(HE,1)+s(WE,1)+s(ASR,1),data = Detroit_Data_Ben_Gonzalez)
anova(gam.detroitmodel33)
summary(gam.detroitmodel33)
plot(gam.detroitmodel33,se=TRUE,col="blue")

## Detroit GAM 4
gam.detroitmodel44=lm(HOM~FTP+LIC+NMAN+poly(GOV,2)+poly(HE,3)+WE+ASR,data = Detroit_Data_Ben_Gonzalez)
anova(gam.detroitmodel44)
summary(gam.detroitmodel44)
plot.gam(gam.detroitmodel44,se=TRUE,col="blue")


gam.detroitmodel55=lm(HOM~poly(FTP,2)+GR+poly(LIC,2)+NMAN+GOV+HE+WE+ASR,data = Detroit_Data_Ben_Gonzalez)
anova(gam.detroitmodel55)
summary(gam.detroitmodel55)
plot(gam.detroitmodel55,se=TRUE,col="blue")

anova(gam.detroitmodel11,gam.detroitmodel22,gam.detroitmodel33,gam.detroitmodel44,gam.detroitmodel55,test = "F")
##Non-Linear Relationships
#Nonlinear relationships for Full Time Police
fit1T=lm(HOM~poly(FTP,1,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit2T=lm(HOM~poly(FTP,2,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit3T=lm(HOM~poly(FTP,3,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit4T=lm(HOM~poly(FTP,4,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit5T=lm(HOM~poly(FTP,5,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit6T=lm(HOM~poly(FTP,6,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit7T=lm(HOM~poly(FTP,7,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit8T=lm(HOM~poly(FTP,8,raw = T),data = Detroit_Data_Ben_Gonzalez)
anova(fit1T,fit2T,fit3T,fit4T,fit5T,fit6T,fit7T,fit8T)
plot(HOM,FTP)

#Nonlinear relationships for Gun Licenses
fit1L=lm(HOM~poly(LIC,1,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit2L=lm(HOM~poly(LIC,2,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit3L=lm(HOM~poly(LIC,3,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit4L=lm(HOM~poly(LIC,4,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit5L=lm(HOM~poly(LIC,5,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit6L=lm(HOM~poly(LIC,6,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit7L=lm(HOM~poly(LIC,7,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit8L=lm(HOM~poly(LIC,8,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit9L=lm(HOM~poly(LIC,9,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit10L=lm(HOM~poly(LIC,10,raw = T),data = Detroit_Data_Ben_Gonzalez)
anova(fit1L,fit2L,fit3L,fit4L,fit5L,fit6L,fit7L,fit8L,fit9L,fit10L)
plot(HOM,LIC)

## Nonlinear Relationship for Gun Registrations
fit1gr=lm(HOM~poly(GR,1,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit2gr=lm(HOM~poly(GR,2,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit3gr=lm(HOM~poly(GR,3,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit4gr=lm(HOM~poly(GR,4,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit5gr=lm(HOM~poly(GR,5,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit6gr=lm(HOM~poly(GR,6,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit7gr=lm(HOM~poly(GR,7,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit8gr=lm(HOM~poly(GR,8,raw = T),data = Detroit_Data_Ben_Gonzalez)
anova(fit1gr,fit2gr,fit3gr,fit4gr,fit5gr,fit6gr,fit7gr,fit8gr)
plot(HOM,WE)

#Nonlinear relationships for NonManufacturing

fit1n=lm(HOM~poly(NMAN,1,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit2n=lm(HOM~poly(NMAN,2,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit3n=lm(HOM~poly(NMAN,3,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit4n=lm(HOM~poly(NMAN,4,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit5n=lm(HOM~poly(NMAN,5,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit6n=lm(HOM~poly(NMAN,6,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit7n=lm(HOM~poly(NMAN,7,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit8n=lm(HOM~poly(NMAN,8,raw = T),data = Detroit_Data_Ben_Gonzalez)
anova(fit1n,fit2n,fit3n,fit4n,fit5n,fit6n,fit7n,fit8n)
plot(HOM,NMAN)


#Nonlinear relationships for Government Workers

fit1g=lm(HOM~poly(GOV,1,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit2g=lm(HOM~poly(GOV,2,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit3g=lm(HOM~poly(GOV,3,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit4g=lm(HOM~poly(GOV,4,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit5g=lm(HOM~poly(GOV,5,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit6g=lm(HOM~poly(GOV,6,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit7g=lm(HOM~poly(GOV,7,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit8g=lm(HOM~poly(GOV,8,raw = T),data = Detroit_Data_Ben_Gonzalez)
anova(fit1g,fit2g,fit3g,fit4g,fit5g,fit6g,fit7g,fit8g)
plot(HOM,GOV)

## Nonlinear Relationship for Hourly Earnings

fit1h=lm(HOM~poly(HE,1,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit2h=lm(HOM~poly(HE,2,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit3h=lm(HOM~poly(HE,3,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit4h=lm(HOM~poly(HE,4,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit5h=lm(HOM~poly(HE,5,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit6h=lm(HOM~poly(HE,6,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit7h=lm(HOM~poly(HE,7,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit8h=lm(HOM~poly(HE,8,raw = T),data = Detroit_Data_Ben_Gonzalez)
anova(fit1h,fit2h,fit3h,fit4h,fit5h,fit6h,fit7h,fit8h)
plot(HOM,HE)

## Non-Linear Relationships for Weekly Earnings 

fit1w=lm(HOM~poly(WE,1,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit2w=lm(HOM~poly(WE,2,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit3w=lm(HOM~poly(WE,3,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit4w=lm(HOM~poly(WE,4,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit5w=lm(HOM~poly(WE,5,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit6w=lm(HOM~poly(WE,6,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit7w=lm(HOM~poly(WE,7,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit8w=lm(HOM~poly(WE,8,raw = T),data = Detroit_Data_Ben_Gonzalez)
anova(fit1w,fit2w,fit3w,fit4w,fit5w,fit6w,fit7w,fit8w)
plot(HOM,WE)

## Non-Linear Relationships for Assaults 

fit1a=lm(HOM~poly(ASR,1,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit2a=lm(HOM~poly(ASR,2,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit3a=lm(HOM~poly(ASR,3,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit4a=lm(HOM~poly(ASR,4,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit5a=lm(HOM~poly(ASR,5,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit6a=lm(HOM~poly(ASR,6,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit7a=lm(HOM~poly(ASR,7,raw = T),data = Detroit_Data_Ben_Gonzalez)
fit8a=lm(HOM~poly(ASR,8,raw = T),data = Detroit_Data_Ben_Gonzalez)
anova(fit1a,fit2a,fit3a,fit4a,fit5a,fit6a,fit7a,fit8a)
plot(HOM,ASR)


## Detroit Dataset Tree-Based Methods ##################################

## Detroit Dataset Random Forest
library(ISLR)
library(tree)
names(Detroit_Data_Ben_Gonzalez)
library(randomForest)
attach(Detroit_Data_Ben_Gonzalez)

lstMSEs=numeric()
set.seed(1)
maxnumpreds=ncol(Detroit_Data_Ben_Gonzalez)-1
maxnumtrees=10

for(numpreds in 1:maxnumpreds){
  for(numtrees in 1:maxnumtrees){
    
    nrow(College)
    train=sample(1:nrow(Detroit_Data_Ben_Gonzalez),nrow(Detroit_Data_Ben_Gonzalez)/2)
    
    
    model.bagged=randomForest(HOM~.,data = Detroit_Data_Ben_Gonzalez,subset = train,mtry=numpreds,ntree=numtrees,importance=TRUE)
    
    
    
    pred.vals.bagged=predict(model.bagged,newdata = Detroit_Data_Ben_Gonzalez[-train])
    testvals=Detroit_Data_Ben_Gonzalez$HOM[-train]
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
tree.detroit1=tree(HOM~.,data = Detroit_Data_Ben_Gonzalez)
plot(model.bagged)
plot(tree.detroit1)
text(tree.detroit1,pretty = 0)
varImpPlot(model.bagged)
model.bagged
min(lstMSEs)

## Detroit Random Forest with K-Fold CV Approach


library(randomForest)
library(tree)
attach(Detroit_Data_Ben_Gonzalez)
lstMSEs <- numeric()
set.seed(1)
maxnumpreds <- ncol(Detroit_Data_Ben_Gonzalez) - 1
maxnumtrees <- 10

samplesize <- dim(Detroit_Data_Ben_Gonzalez)[1] 
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
    train <- sample(1:nrow(Detroit_Data_Ben_Gonzalez), nrow(Detroit_Data_Ben_Gonzalez)/2) 
    model.bagged.2 <- randomForest(HOM~.,data=Detroit_Data_Ben_Gonzalez,subset=train,mtry=numpreds,ntree=numtrees,importance=TRUE) 
    
    pred.vals.bagged <- predict(model.bagged.2, newdata=Detroit_Data_Ben_Gonzalez[-train,])
    testvals <- Detroit_Data_Ben_Gonzalez$HOM[-train]
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
tree.detroit2=tree(HOM~.,data = Detroit_Data_Ben_Gonzalez)
plot(model.bagged.2)
text(tree.detroit2,pretty = 0)
varImpPlot(model.bagged.2)
importance(model.bagged.2)
model.bagged.2
min(lstMSEs)


##Detroit Dataset Linear Model with K-Fold CV Approach

library(ISLR)
names(Detroit_Data_Ben_Gonzalez)
attach(Detroit_Data_Ben_Gonzalez)

lstMSEs=numeric()
set.seed(1)
maxnumpreds=ncol(Detroit_Data_Ben_Gonzalez)-1
maxnumtrees=10
samplesize <- dim(Detroit_Data_Ben_Gonzalez)[1] 
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
    train=sample(1:nrow(Detroit_Data_Ben_Gonzalez),nrow(Detroit_Data_Ben_Gonzalez)/2)
    
    
    model.linearKFoldCV=lm(HOM~.,data = Detroit_Data_Ben_Gonzalez,subset = train,mtry=numpreds,ntree=numtrees,importance=TRUE)
    
    
    pred.valskfoldcvlinear.bagged=predict(model.linearKFoldCV,newdata = Detroit_Data_Ben_Gonzalez[-train])
    testvals=Detroit_Data_Ben_Gonzalez$HOM[-train]
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

## Detroit Dataset Resampling Methods #################################################

#Cross-Validation Approach
set.seed(1)
dim(Detroit_Data_Ben_Gonzalez)
train=sample(13,4)
lmcv.fit1=lm(HOM~LIC,data = Detroit_Data_Ben_Gonzalez,subset = train)
mean((HOM-predict(lmcv.fit1,Detroit_Data_Ben_Gonzalez))[-train]^2)


## Detroit Dataset K-Fold Cross Validation #
cv.error=rep(0,5)
for (i in 1:5){
  glm.fit=glm(HOM~poly(LIC,i),data = Detroit_Data_Ben_Gonzalez)
  cv.error[i]=cv.glm(Detroit_Data_Ben_Gonzalez,glm.fit,K=13)$delta[1]
}
cv.error


## Leave-One-Out-Cross-Validation
glm.fit=glm(HOM~LIC,Detroit_Data_Ben_Gonzalez)
coef(glm.fit)
library(boot)
glm.fit=glm(HOM~LIC,data = Detroit_Data_Ben_Gonzalez)
cv.err=cv.glm(Detroit_Data_Ben_Gonzalez,glm.fit)
cv.err$delta




### End of Detroit Dataset Modeling########################################################



````
