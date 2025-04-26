# Creating an Analysis project using Pandas & Numpy


## In this github repository I will showcase the step by step guide I took to create a project in a jupyter file:

1- First step is to import the libraries such as pandas and numpy in this case as well as read the csv file. 
  - Along the way, I have managed to find the total amount of males and females that are included in this DataFrame. 

  ```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt


data = pd.read_csv('students/student_habits_performance.csv')

data.head(10)
data.groupby('gender').count()

  ```
<img width="136" alt="Screenshot 2025-04-26 at 09 47 30" src="https://github.com/user-attachments/assets/7690b5f6-98e1-48a8-8db0-55af72b58dfb" />

2- Secondly, data cleaning actions took place in order for the document to be more presentable and easier to work with:

  ```
data.rename(columns={'student_id':'ID','study_hours_per_day':'study_hours','social_media_hours':'sm_hours'})
  ```
- I firstly focused on renaming the column names and later checking for any empty values and duplicates like below. The result came out positive so this allowed me to move on to the next step:

  ```
  data.duplicated().head(10)
  ```

3 - The following step was to move on to some analysis, starting out with finding out how many hours each gender spends in front of the social media apps. The groupby method has been used to recieve this information: 

 ```
grouped_sm = data.groupby('gender')['social_media_hours'].sum()

grouped_sm
  ```

4- In order for me to practice .loc, I have selected columns such as gender = 'Male' and part_time_job = 'Yes', for practice purposes:

 ```
data_age_male = data.loc[(data['part_time_job']=='Yes') & (data['gender']== 'Male')].head(10)

data_age_male
  ```

5- Once finding out how many social media hours each gender spends, my next step was to use groupby method and concat to combine two datasets together, to find out the total amount of daily hours spend studying per gender:


 ```
datam = data_age_male.head(100).groupby('gender')['study_hours_per_day'].sum() 

dataf = data_age_female.head(100).groupby('gender')['study_hours_per_day'].sum()

datam = pd.DataFrame(datam)
dataf = pd.DataFrame(dataf)

datam 
dataf

new_df = pd.concat([datam,dataf]) # it allows us to combine two dataframes together.

new_df
  ```
- The result came out to the following:

<img width="189" alt="Screenshot 2025-04-26 at 10 01 48" src="https://github.com/user-attachments/assets/758210af-4256-4990-8d39-a49a46c48ff9" />
