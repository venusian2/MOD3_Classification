# Mod 3 Classification Project

DSC NYC Flatiron Module 2 Project
By: **Jason Drummond and Muriel Kosaka**

## Goal

Create a classification model that will correctly predict whether a person will make over median income based on different attributes.

## Use Case

As a policy maker you would like to know where to allocate resources or create programs for people who fall below the median income range.

## DataSet

Our original data set came from the UCI Machine Learning Repository website, (https://archive.ics.uci.edu/ml/datasets/Adult). This Datset was deemed to be too 
outdated as it was over 205 years old. We extracted the same data along with new variables from the following website, (https://cps.ipums.org/cps/) 

There were over 180,000 rows in our Dataset depicting the salaries for people participating in the Census Bureaus CPS Survey for the year 2018. It is our goal to 
see what factors contribute most to a persons Income.



## Data Cleaning

There were many things that need to be cleaned up in our Dataset. First we had to recode columns, using a Data Dictionary, to get a better understanding of what each one represented. We

There were many things that needed to be cleaned up in our Dataset. First we dropped Fiscal Year 2014 from our dataset as it had very little data to use. We then created a new column to explore any relationhip between number of years worked for city and Salary. Upon investigating the Data for Teachers I found bi problem that needed to be fixed. Whenever a Teacher does extracurricular work they get paid per session and this shows up in an entirely different row from their yearly salary. I took all the money they made from this row and addded it in as OT in their respective yearly salary row. This one step got rid of a big chink of Data as teachers are one of the most common jobs in NYC. From here I fixed all of the Agency Names to reflect the overarching Agency that they belong to, as some were broken down into smaller components, mainly Community Board, Department of Eduaction, and District Attorney. The last step was getting rid of anyone that was not a full time workker as we only wanted to focus on this group.

## Statistical Tests

After conducting a chi square test on Sex and Income, we found a significant difference between men and women. Men are significantly more likely to earn over the 
median income as compared to women



After performing an independent samples t-test on Age and Income, we found a significant difference. Those who earn more than the median are significantly older 
than those who are not.



We performed an independent samples t-test on Hours Worked Per Week vs. Income and found a significant difference. Those who earn more than the median amount 
worked significantly more hours per week than those who make less than the median.



We performed a chi square test on Education vs Income and found a significant difference. Post-hoc tests revealed that those who have a Doctorate, Master’s, or a 
Professional School Degree earn more than the median.



## Feature Engineering

This was the biggest limitation to this DataSet. We could not create too many features as a majority of the Data was categorical or binary. We did look at percentages of people making over the median income in the following areas, age, race, 


We were able to create a feature pertaining to how many years the person worked for the City. Other than that we mainly had to work with Dummy variables, we created them for all of the different agencies. Upon looking at all the different jobs in the Title Description column we had to limit dummy variables as it the amount would overload the OLS model and not output a model. To make a good model based on this data we created dummy variables for all of the Title Descriptions and then looped through all of them and found the Jobs that gave us the highest R_squared value when compared to Salary and added them in to our model. This greatly boosted the R_squared of our model.

## Classification Models

We created four different classification models, a logistic, a KNN, a Decision Tree, and a Random Forest. We found that the KNN Model, after GridSearch. gave us our best accuracy score of .7859 but failed to do well on the F-1 score giving us a meager score of .6045. The Logistic model, after GridSearch however gave us the best F-1 score of .6641 and a fairly decent accuracy score of .7612. After testing on each of our models we noticed some were giving us good F-1 scores while others were giving us better accuracy scores, this led us to our decision to try and implement a Voting Classifier. Upon creating this ensemble model we produced our best accuracy and F-1 scores of .7850 and .6680 respectively. This also produced the highest ROC_AUC score of .8532 just barely beating out the Logistic regression model with Grid Search's score of .8493. This led us to choosing the Voting Classifier model bundling all other grid Searched models as our final model that we would use on an unseen dataset.

## Conclusion
 
(Distribtion_Plot.png)

(Probability_Plot.png)

We were able to create a model using a Voting Classifier bundling the KNN, Logsitic, Decision Tree, and Random Forest models that produced a model with an F-1 score of .6680 and an accuracy score of .7850. The baseline accuracy, if we were just to choose the majority class for all datapoints, was .7005 for our dataset, utilizing the Voting Classifier model we are able to increase that accuracy by 12 percent.

## Use Case Insights

* There has been a rise in Average Salary every year in the dataset 
* If you wanted to Retire Early the best Agencies to go into are as follows
  * Police Department
  * Department of Education
  * Fire Department
* If you want to be in the Top earning Agencies focus on jobs in the folloowing Agencies
  * Office Of Colletive Bargaining
  * Financial Info Svcs Agency
  * Office of the Actuary
