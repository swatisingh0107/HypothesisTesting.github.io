50 customers were randomly assigned to each group as follows:

|Group|Discount Type|	Color
|---|---|---
|1|	10% off	|Green|
|2	|10% off	|Black|
|3|	10% off|	Red|
|4	|-10% |	Green|
|5	|-10% |	Black|
|6|	-10%	|Red|

According to null hypothesis, the mean of the dependent variable i.e. Total Amount Spent is the same for all groups mentioned above. 
Therefore, the interaction of different text of promotion and color of presentation does not have any effect on the spending behavior 
of the customers.

**Following hypotheis is proposed:**

**Hypothesis 1:** When we collapse across color, the main effect of text of the promotion i.e. ‘-10%’ vs ‘10% off’ is significant on groups. 
The amount spent will be more when the text states “store wide price promotions of 10% off on what you purchase today”.

**Hypothesis 2:** When we collapse across text, the main effect of the color of the presentation is significant on each group. 
Red will have highest influence on the dependent variable.

**Hypothesis 3:** The interaction of color and promotional text have influence on the group means of dependent variable. 
We presume that customers are more likely to buy more when presented with “10% off” discount in RED color.

**Reasoning for the proposed hypothesis:**

•	Customers are in general, **“cognitive misers”**. A discount of -10% leads the customers to focus on the calculation of what is -10% 
value rather than the discount itself.

•	-10% also projects an image that sales are not great, or the product was originally overvalued, and the price is now being corrected 
rather than present a picture that customers are getting a better deal on a high value item.

•	Psychologically, the color, RED increases heart rate and promotes urgency. This makes it a good color of choice for clearance or 
discounts sales which encourages consumers to hurry and take advantage of the opportunity. BLACK signifies power and authority and 
therefore is more suitable for luxury items. GREEN signifies peace and calmness and is generally associated with positive features and 
therefore is contradictory to the concept of discount.

•	RED is the color with highest wavelength in the visible spectrum of light and therefore the easiest to process by the human brain. 
Therefore, RED tends to stand out amidst a mix of colors and draw immediate attention which meets the objective of the banner on the 
screen.

•	In general, we assume that bulk of the text and background in websites is BLACK/WHITE and choosing RED will help the banner stand 
out in contrast to the background.

We can run both ANOVA and LINEAR regression, but ANOVA is more suited for this specific use case as the predictor variable is continuous and the independent variables are 
categorical in nature

```yaml
---
title: Hypothesis Testing
  Author: Swati Singh
rmarkdown::github_document
        ---
```
```{r}
library(dae)
## Loading required package: ggplot2
library(psych)
dataA <- read.csv("data.csv",encoding = 'UTF-8')

#model the effect of interaction of color and discount on Purchase Amount
model1<- lm(Amount.spent~color*discount,dataA) 

#study the effect of each color used in promotion on Purchase Amount
model2 <-lm (Amount.spent~factor(color),dataA)
```

```{r}
anova(model1)
```

```{r}
with(dataA, interaction.plot(discount,color,Amount.spent, ylab="Amount.Spent",
                             xlab="Discount",trace.label = "Color"))

```
### Inference from ANOVA:
•	The main effect of color is significant on the outcome variable i.e. amount spent.\
•	The main effect of discount is not significant on the outcome variable.\
•	There is interaction (cross-over) between the type of discount and color of discount for BLACK and RED colors and has significant effect on the outcome variable.\
•	RED and “10% off” discount type offers the best value for amount spent. \
•	When using -10% discount type, BLACK color results in higher spending than RED color.\
•	GREEN color results in lesser amount spent compared to RED/BLACK irrespective of the type of discount.\


```{r}
#Linear regression output for model1
summary(model1)
```
Inference:
•	Linear model has similar inference about the main effects and interaction of color and discount.\
•	The interaction of colorGreen:DiscountOff showed higher magnitude of influence on the total amount spent vs colorBlack:DiscountOff which is different for the ANOVA model.\
•	The null hypothesis is rejected by both models.\

```{r}
library("ggpubr")
ggboxplot(dataA, x = "discount", y = "Amount.spent", color = "color",
          palette = c("black","green","red"))
```
### Based on the analysis of the boxplot and anova summary

•	The null hypothesis is rejected. The mean of all the groups is not the same.\
•	The main effect of color is statistically significant with low P value ( 2e-16< 0.05) and high F value (~89). \
•	The main effect of discount type is statistically insignificant with high P value (0.574>0.05) and low F value (~0.3). \
•	Hence, the interaction of color and discount type is statistically significant with low P value ( 5.74e-14<0.05) and high F value ( ~33) \
### Inference
•	Based on the experiment, the mean of the amount spent for group with “10% Off” was higher than the rest of the groups. Therefore we can infer that the customers will spend more when the promotion is “store wide price promotions of 10% off on what you purchase today”.\
•	When, -10% off is used, customers spent more the discounted was presented in BLACK color than when presented in RED color\
•	GREEN color resulted in lower sales compared to BLACK & RED irrespective of type of discount\

Color of presentation plays a major role in the amount spent by the customer. The significant main effect for color means that the null hypothesis is rejected and there is significant difference between the means of the groups for different colors.\
•	The interaction of the RED and BLACK lines when plotted over the discount type indicate that the outcome by using either color is increased when paired with an appropriate discount type (BLACK with -10% and RED with 10% off). The interaction suggests that the color group behaves differently for different discount types.\

```{r}
TukeyHSD(aov(model1))
```

Based on Tukey analysis, we identified groups that perform marginally better than other groups. Group 3 and group 5 perform marginally better than other groups.\
•	For red and black, promotion text has slightly significant influence.\
•	Advertise 10% off in RED color to achieve the best sales.\
•	The website text and background colors need to be chosen in contrast with RED color so that the banner stands out distinctly and catches the customer’s attention\
•	Run campaign 1 (10% Off) and campaign2 (-10%) based on different promotion contexts. Campaign 1 is suitable for situations during clearance sales, limited period offers. Campaign 2, however can be used in contrast with campaign 1, for luxury items. \
•	The promotions should be run infrequently so that customers perceive the difference. Leaving the banner present always results in cognitive oversight as well as the impression that base prices may have been hiked to offset the discount resulting in the customer not receiving any value-add with the discount. \



