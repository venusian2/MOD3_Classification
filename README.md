# Mod 3 Classification Project

DSC NYC Flatiron Module 3 Project
By: **Jason Drummond and Muriel Kosaka**

## Presentation Link (https://docs.google.com/presentation/d/1RYuTh9dFPOzJo0IkjLOwL0ptJ_eTNzYKQgWviHJQvaQ/edit#slide=id.g8b57e1b895_0_188)

## Goal

Create a classification model that will correctly predict whether a person will make over the median income based on different attributes.

## Use Case

As a policy maker you would like to know where to allocate resources or create programs for people who fall below the median income range.

## DataSet

Our original data set came from the UCI Machine Learning Repository website, (https://archive.ics.uci.edu/ml/datasets/Adult). This Datset was deemed to be too 
outdated as it was from over 25 years ago. We extracted the same data along with new variables from the following website, (https://cps.ipums.org/cps/) 

There were over 180,000 rows in our Dataset depicting the salaries for people participating in the Census Bureau's CPS Survey for the year 2018. It is our goal 
to see what factors contribute most to a persons income.


## Data Cleaning

There were many things that need to be cleaned up in our Dataset. First we had to recode columns, using a Data Dictionary, to get a better understanding of what 
was being represented. We noticed that there were about 40,000 rows that were missing our target variable of income so we had to delete all of those from the 
dataset. We noticed that there were another 40,000 or so rows that had a lot of missing data in various columns, we feel this is a result of people not taking 
the questionaire seriously and only filling out information that they felt comfortable releasing, we wound up deleting these rows from our data frame as well. 
The last column that we had to deal with was the amount of hours people worked, we wanted to limit our search to only people that were currently employed thus 
deleting anyone that worked 0 hours. This Data cleanning process left us with about 100,000 datapoints which is still good enough to make a model with.


## Statistical Tests

After conducting a chi square test on Sex and Income, we found a significant difference between men and women. Men are significantly more likely to earn over the 
median income as compared to women

![](/images/Sex_v_Income.png)

After performing an independent samples t-test on Age and Income, we found a significant difference. Those who earn more than the median are significantly older 
than those who are not.

![](/images/Age_v_Income.png)

We performed an independent samples t-test on Hours Worked Per Week vs. Income and found a significant difference. Those who earn more than the median amount 
worked significantly more hours per week than those who make less than the median.

![](/images/Hrs_v_Income.png)

We performed a chi square test on Education vs Income and found a significant difference. Post-hoc tests revealed that those who have a Doctorate, Master’s, or a 
Professional School Degree earn more than the median.

![](/images/Educ_v_Income.png)

## Feature Engineering

This was the biggest limitation to this DataSet. We could not create too many features as a majority of the Data was categorical or binary. We did look at 
percentages of people making over the median income in the following areas, Age, Race, Marital Status, ASECwt, and Education as to try and figure out the best 
way to bin each variable. Other than that we mainly had to work with dummy variables, we created dummy variables for Education level, Work class, Race,
Occupation, Industry, Birthplace, and Family Relation. After looking at the sheer amount of different dummy variables that would have been created for occupation 
and industry we decided to group these using the general heading for each different occupation and industry type in the data dictionary so we did not overload 
our system.

## Classification Models

We created four different classification models, a logistic, a KNN, a Decision Tree, and a Random Forest. We found that the KNN Model, after GridSearch. gave us our best accuracy score of .7859 but failed to do well on the F-1 score giving us a meager score of .6045. The Logistic model, after GridSearch however gave us the best F-1 score of .6641 and a fairly decent accuracy score of .7612. After testing on each of our models we noticed some were giving us good F-1 scores while others were giving us better accuracy scores, this led us to our decision to try and implement a Voting Classifier. Upon creating this ensemble model we produced our best accuracy and F-1 scores of .7850 and .6680 respectively. This also produced the highest ROC_AUC score of .8532 just barely beating out the Logistic regression model with Grid Search's score of .8493. This led us to choosing the Voting Classifier model bundling all other grid Searched models as our final model that we would use on an unseen dataset.

## Conclusion
 
![](/images/ROC_Final.png)

![](/images/confusion_matrix.png)

We were able to create a model using a Voting Classifier bundling the KNN, Logsitic, Decision Tree, and Random Forest models that produced a model with an F-1 score of .6680 and an accuracy score of .7850. The baseline accuracy, if we were just to choose the majority class for all datapoints, was .7005 for our dataset, utilizing the Voting Classifier model we are able to increase that accuracy by 12 percent.

## Use Case Insights

* Education level, Age, Gender, Hours worked per week, as well as occupations in the Management, Business, Science & Art Fields have the highest influence on predicting 
if a person will make over the median income.
* As a policy maker you can focus on variables such as Gender and Education Level to produce the largest increase in these groups making over the median income 
by providing resources for these types of individuals
 * For people with lower Education Levels, you can provide low or no interest loans to make it easier for people to enter into higher education or provide reduced costs for these individuals
 * For Gender, policy makers can create grants for women to enter into idustries where there is a large gender bias.
