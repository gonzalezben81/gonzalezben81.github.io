---
layout: page
title: "Predicting crime in Detroit"
author: "Ben Gonzalez"
date: "December 14 , 2018"

---


<center>Final Data Analysis-Detroit Dataset</center>


<center>Ben Gonzalez</center>


<center>AA530-Advanced Analytics</center>


<center>Summer,2015</center>


<center>Dr. Mudigonda</center>



**<center>Introduction: Detroit Dataset</center>**

The Detroit dataset is from a book called “Subset selection in Regression”. The original data was collected by J.C. Fisher and used in his paper “Homicide in Detroit: The Role of Firearms”, Criminology, vol.14, 387-400 (1976). The data collected represents homicide data in Detroit from 1961-1973. The data was obtained from ![]http://lib.stat.cmu.edu/datasets/detroit. The following table lists each variable and their descriptions.

----
<center>Detroit Dataset table</center>

----



| Variable   | Scale           | Predictor/Output  | Measurement |
| ------------- |:-------------:| -----:|---|
| FTP(Full-Time Police)    | Predict future homicides | Predictor |  Quantitative |
|  UEMP(Unemployment)    | 3.2-11     |  Predictor/Output |  Quantitative  |
| LIC(Hangun Licences) | 156.4-1134.2 |    Predictor | Quantitative  |
|GR(Handgun Registrations) | 180.5-1029.8| Predictor/Output|Quantitative |
|CLEAR(Homicides cleared) |58.90-94.40 | Predictor/Output|Quantitative |
|WM(White Males) | 359647-558724| Predictor/Output|Quantitative |
| NMAN(Non-manufacturing workers)|539.1-819.8 | Predictor/Output|Quantitative |
|GOV(# of government workers) |133.9-230.9 | Predictor/Output|Quantitative |
|HE(Average Hourly Earnings) | 2.91-5.76| Predictor/Output|Quantitative |
| WE(Average Weekly Earnings) | 117.2-258.1| Predictor/Output|Quantitative |
|HOM(# of homicides)|8.52-52.33| Predictor/Output|Quantitative |
|ACC(Death rate in accidents)|39.17| Predictor/Output|Quantitative |
|ASR(# of assaults)|218-473| Predictor/Output|Quantitative |

----
**Methods of Analysis**

----

**Overview:** For the Detroit dataset I have used several modeling techniques (Correlation, Simple Linear Regression, Multiple Linear Regression, Subset Selection, and Generalized Additive Models). The utilization of the plot function helped to determine what variables in the dataset would be significant and those which would not be significant. The correlation function was also used to determine which variables had a high correlation with the outcome variable of homicide. The models were chosen due to the continuous quantitative features of the Detroit dataset. Simple linear regression was utilized and helped to determine the number of predictors in the dataset that would be needed to predict homicide(s) in Detroit . GLM, LDA, QDA, and K-Nearest-Neighbors(KNN) were ignored due to the dataset having continuous variables which would not model well as low or high classification. Lastly the outcome variable is continuous and the above methods are utilized on qualitative outcome variables.
