# Assignment3
PS947 Assignment3


#loading data file 
getwd()
install.packages("tidyverse")
data <- read.csv("recommendations.csv", header = (TRUE))
print(data)


#creating a plot 
library(ggplot2)
library(dplyr)

#running logistic regression 
model <- glm(RecommendationFollowed ~ Mode , data = data, family = binomial)
summary(model)


#To analyse how the recommendtation mode affects whether a recommendation is followed, we are fitfing a logostic regression model with recommendation mode as the predictor value and recommendation followed as the reponse variable. We are using logistic resgression as the response variable is binary, whether was recommendation was followed or not (0 or 1) 

#creating a new data frame to use for plotting 
new_data <- data.frame(Mode = c("Auditory", "Visual"))

#Predicting the probabilty of following the recommendation for each mode
new_data$prob <- predict(model, new_data, type = "response")


#scatter plot of data points
ggplot(new_data, aes(x = Mode, y = prob)) +
  geom_bar(stat = "identity", fill = "pink", width = 0.2) +
  labs(x = "Mode", y = "Recommendation Followed") +
  ggtitle("logistic regression plot of recommendation mode vs recommendation followed") 

  




  