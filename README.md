# Analysis of Employee Turnover at the White House using Department of Labor Data

For this simulated analysis, I investigated employee turnover at the White House using employee survey data from the Department of Labor.  My investigation included statistical analysis to analyze, predict and visualize future decisions to stay or leave the White House using smachine learning and neural network modeling.

## Preprocessing of Data

To begin, I read in a raw .xlsx file from the Department of Labor. I created a DataFrame to make sense of the over 7,500 employees surveys.  After observing a mixture of numerical and categorical data as well as missing responses, I realized I would need to clean and transform the raw data before proceeding with my machine learning and neural network modeling.

### Data Cleaning

To start, I selected from the data the survey questions that I believed would provide the best results for my analysis.  Of the 122 survey questions, I ultimately selected 32.  These questions included responses about the Employee, the Employee's Supervisor, the Employee's Leadership, the Employee's Organization, the Organizations's Diversity Equity and Inclusion efforts and the Employee's Employment Status.  Each question was ranked using values 1 through 5, ranging between Strongly Disagreeing to Strongly Agreeing.

![image](https://github.com/veenahvina/White_House_Analysis_MarvinaLarry/assets/131216752/3b05c276-bd45-47ee-ba05-85284e6dad98)

### Drop Rows with Missing Data
For any employee who did not respond to the "DLEAVING" question, "Are you considering leaving your organization within the next year?", I dropped their row of surveyed responses.  I decided to remove these rows because the goal of this analysis was to predict future employment status.  I would not be able to do this if the question was not answered.

### Missing Values Handling
Next, I knew I needed to address the other employee surveys with missing responses to other questions not "DLEAVING".  To accomplish this, I created a missing values threshold of 20% and calculated what percent of the 32 questions were not answered.  For any survey question with more than 20% of the survey questions missing values, I would evaluate the impact of removing them from my dataset.  There was only one question with more than 20% missing values, Question "DRNO":  "Please select the racial category/categories you most closely identify".  Since I considered this a very significant demographical question, I decided to address the missing values using a different approach.  See the next section.

### Impute and Aggregate Survey Responses
Instead of completely removing the "DRNO" column as previously discussed, I decided to recode the null values with response "D" for "Other Groups Collapsed for Privacy."
Additionally, I recoded survey questions with "X" or "Do not know", as the response to response "3" for "Neither Disagree nor Agree".  
Finally, I used the process of imputing to missing values with the Mode of the column for that missing value.  Meaning, calculated the Mode value of all the other responses in that columns and then used that value to repolace the Null value.
By aggregating and imputing null values to other response values, I maintained sufficient data in my dataset to proceed with my analysis.  Removing too much data could negatively impact the outcome of my analysis.

### Dealing with Question 84: "My Organization Meets My Accessibility Needs"
Question 84 presented many of the challenges mentioned above in addition to one unique challenge, there were two Categorical Responses given:  "X" and "Y" with 
"X" being "No Basis to Judge" and "Y" being "I don't have accessibility needs".  I considered both responses outliers indicating an employees inability to answer the question.  Therefore, I decided to recode both "X" and "Y" to response "3", "Neither Disagree or Agree".
I created bar graphs before and after the recoding of the "X" and "Y" survey responses.  Each of the graphs are presented below.  Notice how the recoding created an imbalancing of the value counts of the remaining survey responses.

![image](https://github.com/veenahvina/White_House_Analysis_MarvinaLarry/assets/131216752/3ba69ca2-3e11-4246-b110-b21f219ad2b5)

![image](https://github.com/veenahvina/White_House_Analysis_MarvinaLarry/assets/131216752/8db3d243-8383-45e0-95b5-4d48894a9e20)

### Assigning Dummies for Demographic Variables
Neither machine trained nor neural networked models can function using Categorical values, I created dummy variables for the Demographic variances in the dataset.  These dummies created new columns and assigned either a "0" or a "1" to each survey response.  Like computers, models like "0"s and "1"s.

### Creating Binary Variables for "DLEAVING"
For the "DLEAVING" question, I set response "A" to value "1" and responses, "B", "C" and "D" to value "0".  Again, by assigning either a "0" or a "1" to each survey question I standardized the data, which would make it possible to model later.  Also, since questions "B", "C" and "D" were all very similar in nature, I recoded them the differently than question "A".

This concludes the Data Preprocessing section.

## Variable Relationship Correlations
I used a correlation matrix to help me identify any relationships between the variables in my data, essentially attempting to identify any positive relationship between variables.  While there were a few questions which generated very strong positive relationships, greater than 0.8, the majority of the questions did not.  Further research into the causes of high positivity between variables would require further analysis.  Additionally, had I decided to recode any coefficients greater than 0.8 together, I might have observed less noise in my matrix.

![image](https://github.com/veenahvina/White_House_Analysis_MarvinaLarry/assets/131216752/77244de3-806e-41bc-8ff4-fc7dac48a682)

## Logistic Regression Analysis
As a refresher, the purpose of this simulated analysis is to predict the liklihood of employee retention at the White House.  One method of doing this is by using logistic regression to calculate the probability an employee will leave or continue working at the White House using a series of survey responses.
After establishing the "DLEAVING" question as my target or Independent variable, I trained, tested an fitted my model to predict the probability an employee will stay.  I conducted two model simulations using different model inputs.  In the first model, using a Penalty of "None", the results indicated high accuracy that the survey responses could determine if an employee was leaving or staying.  However, it didn't do so well predicting positive outcomes when compared to actual occurences.  

![image](https://github.com/veenahvina/White_House_Analysis_MarvinaLarry/assets/131216752/0a9cbe97-99bd-4737-8f9f-8da2bc5c766e)

![image](https://github.com/veenahvina/White_House_Analysis_MarvinaLarry/assets/131216752/3de7df75-1a4b-4752-8259-89e82f44d14a)

In my second model, I decided to address the imbalancing in my dataset caused by the removal of missing values and aggegating other values together by using balanced weighted class model.  The goal was to re-balance the distribution of classes in the dataset and to remove any biasness that may have existed.  Use of this balancing approach had a slightly positive impact on my F1 score.

![image](https://github.com/veenahvina/White_House_Analysis_MarvinaLarry/assets/131216752/94bb8484-5098-4532-b394-79ed3cbaed5b)

![image](https://github.com/veenahvina/White_House_Analysis_MarvinaLarry/assets/131216752/f8ba4505-8908-45da-81c9-22a8386d47c6)

This concludes the Logistic Regression section.

## Decision Plotting Using Shap Analysis

I used the Decision Plot by Shap Analysis to provide a visual representation of the most significant survey questions when predicting whether an employee would leave or continue working at the White House.  In the Decision Plot below, the most significant features appear to contribute equally to the prediction of the Outcome:  Will the employee stay or go.

![image](https://github.com/veenahvina/White_House_Analysis_MarvinaLarry/assets/131216752/145e0352-2419-498b-abe4-58beac60632e)

This concludes the Shap Analysis section and this README.











