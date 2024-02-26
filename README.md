# Assignment3
 PS947 Assignment3

#loading data file 
getwd()
install.packages("tidyverse")
data <- read.csv("recommendations.csv", header = (TRUE))
print(data)

#running logistic regression 
model <- glm(RecommendationFollowed ~ Mode , data = data, family = binomial)
summary(model)

#To analyse how the recommendtation mode affects whether a recommendation is followed, we are fitfing a logostic regression model with recommendation mode as the predictor value and recommendation followed as the reponse variable. We are using logistic resgression as the response variable is binary, whether was recommendation was followed or not (0 or 1) 

#creating a plot 
library(ggplot2)

#scatter plot of data points
ggplot(data, aes(x = Mode, y = RecommendationFollowed)) +
geom_point() + 
stats_smooth(method = "glm", color = "pink", method.args = list(family = "binomial"), se = FALSE) + 

#labels for x and y axes 
labs(x = "Mode", y = "RecommendationFollowed") +

#title for the plot
ggtitle("logistic regression plot of recommendation mode vs recommendation followed") 



  