# Assignment3
PS947 Assignment3


#loading data file 
getwd()
install.packages("tidyverse")
data <- read.csv("recommendations.csv", header = (TRUE))
print(data)


#Loading all the required library   
library(ggplot2)
library(tidyverse)
library(tibble)
library(purrr)
set.seed(947)


#Question 3:

#Part 1- 
#There are two parameters that beta distribution takes which are alpha and beta. 
#alpha represents the number of positive outcome that we believe have occurred before observing any data.
#leads to a distribution skewed towards 1, indicates stronger belief in high possibilities. 

#beta represents the number of negative outcome that we believe have occurred before observing any data. 
#leads to a distribution skewed towards 0, indicates stronger belief in lower possibilities. 

#changes that we will have to make in our dependent variable will be to bound our DV within the range of 0 and 1 as beta distribution is defined on the interval (0 and 1).
#it can be done by checking the skewness and checking for 0 and 1.


#Part 2- Plotting a beta distribution.
#simulating prior predictions for a single sample, and making predictions for multiple samples along with creating a tibble for parameters and lastly, computing the likelihood for a given value of alpha and beta.

  
#Plotting Prior predictions
Alpha <- rnorm(1, 70, 5)
Beta <- rnorm(1, 27.5)

sim_distribution <- tibble(marks = rbeta(100, Alpha, Beta))
priors <- tibble(n = 1:50) %>%
  mutate(Alpha = rnorm(n, 70, 5),
         Beta = rnorm(n, 27.5, 5)) 

gen_prior_pred <- function(n, Alpha, Beta)
  x <- seq(0, 1, 0.01)    # Making an assumption marks range from 0 to 100, scale x to [0, 1]
  d <- tibble(n = n, Alpha = Alpha, Beta = Beta, x = x, y = dbeta(x, Alpha, Beta))
  return(d)
  
prior_llh <- pmap_df(priors, gen_prior_pred)

# Plotting geom_path to show variability in the data.
ggplot(prior_llh, aes(x, y, group = n, color = Beta)) +
  geom_path(alpha = 0.25) +
  scale_color_gradient(low = "pink", high = "blue") +
  labs(title = "Prior Predictions For PS947 Marks",
       x = "Marks", y = "Density", color = "Variability")


#Part 3- Creating a set of informative and a set of weakly-informative priors for the model.

#Part 4- Creating some prior predictions and creating a plot.



# Question 2:

#Fitting the model

model <- glm(RecommendationFollowed ~ Mode , data = data, family = binomial)
summary(model)

#Analysis choice- 
#For visual mode the coefficient is -0.48. 
#It indicates that people are less likely to follow visual recommendation as compared to auditory mode.
#Furthermore, the P value suggests that the mode of recommendation significantly affects the likelihood of the recommendation. 

#Plotting a graph- 
ggplot(new_data, aes(x = Mode, y = prob)) +
  geom_bar(stat = "identity", fill = "pink", width = 0.2) +
  labs(x = "Mode", y = "Recommendation Followed") +
  ggtitle("logistic regression plot of recommendation mode vs recommenation followed")



# Question 1: 
#Repository has been made on github in which changes has been commited. Collaborates has been added and the repository is public.  

