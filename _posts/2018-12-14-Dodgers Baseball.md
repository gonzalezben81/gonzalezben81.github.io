
The following analysis is of the dodgers baseball dataset received from Professor Keith
Hacke for Contemporary Analytics 5750. The dataset looks at the promotional use of items such
as fireworks, caps, shirts, and bobblehead’s as giveaways. The purpose of the following analysis
is to see if the use of giveaways has an impact on the attendance of individuals who attend
baseball games at Dodger’s stadium. The following table describes the variables that are in the
data set. The following predictors were used to determine if the use of bobblehead’s, caps,
fireworks, or shirts affected the attendance of individuals at dodger’s games. The overall results
from the analysis show that utilizing both fireworks and bobblehead’s as a giveaway on the same
day has the best effect on attendance. Certain variables such as the day of the week and the
temperature also impact attendance as well. The following tables list the variables and their
description for the Dodgers dataset.




  
### Dodgers Dataset Description 




| Variable   | Description          | Quantitative or Qualitative  |
| :------------- |:-------------| :-----|
|Month |Month of the year |Qualitative|
|Day |Day of Month| Quantitative|
|Attend |Attendance at game| Quantitative|
|Day of Week| Day of week| Qualitative|
|Opponent| Opponent played in game| Qualitative|
|Temp| Temperature at time of game |Quantitative|
|Skies| Condition of skies| Quantitative|
|Day Night| Time of game (day or night)|Qualitative|
|Cap| Cap given away (yes or no)| Qualitative|
|Shirt| Shirt given away (yes or no)|Qualitative|
|Fireworks| Fireworks used at game (yes or no)|Qualitative|
|Bobblehead| Bobblehead given away (yes or no)|Qualitative|
|Ordered day of week| Day of week (Mon, Tues. etc.…)|Qualitative|
|Ordered month| Month of year (Apr, Aug, etc.…)|Qualitative|
|Temp high low| Temperature ( Cold, Mild,Hot) |Qualitative|


Dodgers' Dataset Visualizations

![](/img/dodgers_temperature.png)

The temperature visualization shows that the temperature at the time of the game is a good
indicator of the attendance by individuals at the game.

![](/img/dodgers_attendance.png)

The attendance by day of week chart shows that the highest number of individuals attended
games on Tuesdays.

![](/img/dodgers_bobblehead_attendance.png)

The bobblehead by attendance chart shows that more individuals attended games when a
bobblehead was given away than if there was no bobblehead given away.

![](/img/dodgers_tshirt_giveaway.png)

The t-shirt by attendance chart shows that individuals were more likely to attend a game if a tshirt
was given away, versus if a t-shirt was not given away.

![](/img/dodgers_fireworks_attendance.png)

The fireworks by attendance chart shows that individuals were neither more nor less likely to
attend a game with fireworks present. This may be due to fireworks being used on holidays,
weekends, or after a win against certain teams.

![](/img/dodgers_cap_giveaway.png)

The cap by attendance chart shows that individuals were not more or less likely to attend a game
if a cap was being given away at the game.

### What days are promotions used?

| Promotion Used  | Mon|Tues|Wed|Thurs|Fri|Sat|Sun|Total Used|
| :---------------|:---|:---|:--|:----|:--|:--|:--|:---------|
| Bobblehead|0|6|0|2|0|2|1|11|
| Cap|0|1|0|0|0|0|1|2|
| Shirt|1|1|0|0|0|0|1|3|
| Fireworks|0|0|1|0|13|0|0|14|
| Total per Day|1|8|1|2|13|2|3|31|

The above table shows that the most used promotional item was fireworks on Fridays, but
these were no more likely to affect attendance according to the previous charts. The next most
giveaways were given away on Tuesday, and these were the bobblehead giveaways. This shows
that bobblehead giveaways may affect attendance more than any other promotional item.

### Dodgers Dataset: Conditional Variable Charts

![](/img/dodgers_fireworks_lattice.png)

The fireworks chart shows that more individuals were likely to attend a night game with clear
skies if fireworks were present than any other time of day or condition of the skies. 

![](/img/dodgers_cap_lattice.png)

The cap chart shows that more individuals attended a game with a cap give away when the
conditions were both day and the skies were clear. 

![](/img/dodgers_shirt_lattice.png)

The shirt chart shows that more individuals attended a night game that had clear skies if a shirt
was being given away. 

![](/img/dodgers_bobblehead_lattice.png)

The bobblehead chart shows that more individuals attended either a night game whether it was
clear or cloudy if a bobblehead was being given away. This chart also shows that bobblehead’s
have an impact on the number of individuals who attend games.

![](/img/dodgers_opponent_lattice.png)

![](/img/dodgers_opponent_shirt_lattice.png)

![](/img/dodgers_opponent_fireworks_lattice.png)

![](/img/dodgers_opponent_cap_lattice.png)

![](/img/dodgers_temp_lattice.png)
### Linear Models

Dodgers Linear Models: Single Giveaways

|Model|Multiple R-Squared|Adjusted R-Squared|P-Value|Estimated Effect on Attendance|
|:----|:-----------------|:-----------------|:------|:-----------------------------|
|Bobblehead Linear Model|0.54|0.46|2.083e-7|10715|
|Cap Linear Model|0.45|0.34|4.439-e05|-10983|
|Fireworkd Linear Model|0.45|0.34|4.593e-05|15658|
|Shirt Linear Model|0.42|0.31|0.0001687|4720|

Utilizing linear regression with one promotional item shows that utilizing bobblehead’s
as a giveaway has the best R-squared at 0.46 and has an estimated effect on attendance at 10,715.
One interesting linear model is that the use of fireworks will have an estimated effect on
attendance at 15,658. The fireworks may be due to the fact they are mainly used on Friday’s,
with the variable day of week being a significant predict itself. Utilizing bobblehead’s on
Friday’s in turn may yield even higher attendance at the dodger’s games. 

### Dodgers Linear Models: Multiple Giveaways

|Model|Multiple R-Squared|Adjusted R-Squared|P-Value|Estimated Effect on Attendance|
|:----|:-----------------|:-----------------|:------|:-----------------------------|
|Bobblehead & Shirt|0.56|0.47|1.599e-07|11134|
|Bobblehead & Cap|0.56|0.46|2.222e-07|9932|
|Bobblehead & Fireworks|0.59|0.50|2.848e-08|10995|
|Cap & Shirt|0.46|0.34|60196e-05|4415|
|Cap & Fireworks|0.48|0.37|1.648e-05|15063|
|Shirt & Fireworks|0.46|0.34|6.41e-05|15394|

For the dodgers dataset when using multiple giveaways at one time, the dual giveaways
of bobblehead’s and fireworks creates the best fitting model. The estimated effect on attendance
is 10995 with the highest adjusted r-squared value of .50. The only other model that has a greater
effect on attendance is the shirt and fireworks model. If the dodgers utilized fireworks and an
additional giveaway on Fridays with fireworks, this would provide the best fitting model to
increase attendance at the games.

### Random Forest: Decision Trees

|Model|Learning Technique|Variables Used|Mean of Squared Residuals|% Variance Explained|Optimal Confg.|Optimal Trees/Interaction F-Statistic|
|:----|:-----------------|:-------------|:------------------------|:-------------------|:-------------|:-------------------------------------|
|Model One|Random Forest Trees = 150|Outcome = Attend Predictors = All(day,  -opponent)|51876966|58858099|28.86|8 Predictors|3 Trees|
|Model Two|Random Forest Trees = 500|Outcome = Attend Predictors = All(day,  -opponent)|42221845|54675633|12.73|9 Predictors|36 Trees|
|Model Three|Random Forest Trees = 1000|Outcome = Attend Predictors = All(day,  -opponent)|42182704|54675633|23.41|9 Predictors|36 Trees|

The best model when utilizing a random forest design on the dodgers’ dataset is Model
One. The model has the largest variance explained at 28.86%. The MSE is only slightly higher
than the MSE for Model Three at 58858099. Model One also has the lowest number of
predictors at trees with 8 predictors and 3 trees being utilized to explain 28.86% of the variance
in the dodgers’ dataset. Thus Model One is the best fitting model when compared to the other
two models that have been utilized on the dodgers’ dataset. 

### Conclusion

Overall, the use of bobblehead’s is the best predictor for increasing attendance at Dodgers
baseball games. Utilizing additional giveaways in combination with bobblehead’s will also
increase attendance at baseball games as well. The additional best predictor’s of attendance at a
baseball game are the day of week and the temperature at the game. Utilizing all three of these
predictor’s will help to determine what combination of giveaways, day of week, and temperature
will help to increase attendance at the Dodgers baseball games. 


