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













