# Multiple-Regression-in-R-programming-
#MULTIPLE REGRESSION  ###
### loading the library
pacman::p_load(pacman, rio, tidyverse)

### Loading the dataset 

data <- import("StateData.xlsx") %>% as_tibble() %>%
  select(instagram:modernDance) %>% print()
view(data)
attach(data)

data %>% select(volunteering, everything()) %>% print() #volunteering comes first 

### There are three ways to specify multiple regression 
model<- lm(data) # the simplest form at line 12
model
summary(model)
### Another way 
# This helps in identitfying the outcome 

model <- lm(volunteering ~., data = data)
model
summary(model)


### Another method is by identifying all the variables 
model <- lm(volunteering ~ instagram + facebook + retweet + entrepreneur + gdpr + 
              privacy + university + mortgage + museum + scrapbook +
              modernDance, data = data)
model
summary(model)

### Confidence interval for the coefficients 
confint(model)

### Prediction values for the coefficients 
predict(model)

### Prediction intervals  for the coefficients 
predict(model, interval = "prediction")

### Regression diagnostics 
lm.influence(model)
influence.measures(model)
