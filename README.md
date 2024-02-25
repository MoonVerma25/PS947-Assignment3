# Assignment3
 PS947 Assignment3

#running logistic regression 
model <- glm(RecommendationFollowed ~ Mode , data = data, family = binomial)
summary(model)
