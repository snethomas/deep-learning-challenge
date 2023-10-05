# Module 21 - deep-learning-challenge

## Overview 
Alphabet Soup is a non profit organization that funds ventures across use cases like preservation, healthcare and product development. Their goal is to identify those ventures that are 'succesful' or used the funds effectively.

## Results

1. Data Preprocessing

* IS_SUCCESSFUL - boolean variable that shows if funds were used succesfully, is the target variable in this exercise. 
* The features of the model are the rest of the columns that play a role in venture 'success', as listed below:
APPLICATION_TYPE
AFFILIATION	
CLASSIFICATION	
USE_CASE	
ORGANIZATION	
STATUS	
INCOME_AMT	
SPECIAL_CONSIDERATIONS	
ASK_AMT
* 'EIN' and 'NAME' are identification columns and neither a feature nor target variable and was dropped
* The categorical variables with too many unique values can reduce the efficiency of a model - hence two columns were considered and grouped/binned, such that their values with the lowest count form an 'Other' bucket:
image.png
    * APPLICATION_TYPE - with 17 unique values reduce to 8 unique values
    image.png
    * CLASSIFICATION - with 71 unique values to 7 unique values
    image.png

2. Compiling, Training, and Evaluating the Model

* The neural network in my first itreation used :
    * 'relu' activation in both the hidden layers since we have positive non-linear input variables
    * 2 hidden layers - as a start
    * 16 neurons in both the hidden layers - there are 26 input variables and 1 output variable so used a number in between as a start
    * 'sigmoid' activation was used for the final layer because its ideal for classification 1/0 output
* To optimize the first model further:I used keras tuner to run multiple iterations with the following range of parameters:
    * 'relu' and 'tanh' activatiions for the hidden layers - since tanh is also an option for regression        
    * 1 to 3 hidden layers - increased by 1 from first model
    * 40 to 100 neurons - to increase accuracy I started with a value greater than that used for the first model
    * Reduced the #epochs to 30
* I also reduced the number of unique values (bins) in APPLICATION_TYPE and CLASSIFICATION columns by changing the cut off values but this did not yield a significant change in results

### Note - The tuner search for best model was terminated after 247 trials due to long run time and the best value of accuracy so far was considered

## Summary

* First iteration yield 72.68% accuracy and 55.26% loss on the test data
    image.png
* The model optimized by keras tuner yielded the following best model parameters:
    * {'activation': 'relu', 'first_units': 32, 'num_layers': 1, 'units_0': 32, 'units_1': 24, 'tuner/epochs': 12, 'tuner/initial_epoch': 0, 'tuner/bracket': 2, 'tuner/round': 0}
    * The model accuracy increased marginally to 72.80% with 55.56% loss
    image.png
