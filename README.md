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

6- From now on, once getting familiar with the DataFrame, my next step was to create graphs. The first graph is a pie chart which which was created with the help of matplotlib was th comparison of study hours per gender. I have used matplotlib in order to calculate the percentage:

 ```
graph = new_df.plot(kind='pie',title='Hours Of Study Vs Gender',subplots=True,figsize=(8,8),autopct='%1.1f%%')


for ax in graph:
    ax.set_ylabel('')  # Removes the y-label (optional)
    ax.set_xlabel('')  # Removes the x-label (optional)
    ax.set_axis_off()  # Hides the axis completely
  ```

 - The result came out as follows:

<img width="500" alt="Screenshot 2025-04-26 at 11 34 59" src="https://github.com/user-attachments/assets/fe2e48f2-87f5-40bf-9f29-2a5b6198ed08" />

7- The second graph which was created was the bar graph. In order for the bar graph to make sense, I had to group the ages of the genders together:

 ```
grouped_data = data.head(10).groupby('age')['social_media_hours'].sum()
ax = grouped_data.head(10).plot(title='Social Media Hours Per Day',kind='bar',x='age',y='social_media_hours')
ax.set_xlabel('Age')
ax.set_ylabel('Hours')
  ```
- The result showcases the first 10 results as .head(10) was used:
<img width="441" alt="Screenshot 2025-04-26 at 11 36 59" src="https://github.com/user-attachments/assets/37d73865-5fab-40cb-aaa7-419e62fcf1bf" />

8- The next step allowed me to caluclate the number one position of females that use netflix the most and analyse it myself. data.sort_values was used to only sort the values that mattered in this case, which was netflix_hours:

 ```
top_row = data.sort_values('netflix_hours', ascending=False).iloc[0]

top_row
  ```
- The results came out as follows:
  <img width="232" alt="Screenshot 2025-04-26 at 11 45 57" src="https://github.com/user-attachments/assets/a08fca67-d8a1-439a-a5c6-cdac733d65c9" />


9- The following pie chart has been create using groupby methods as well as not forgetting autopct='%1.1f%%' technique to calculate the percentage of students that study after their part time jobs.

 ```
grouped = data.groupby('part_time_job')['study_hours_per_day'].sum()


print(grouped)


ax = grouped.head(10).plot(title='Job to study ratio',kind='pie',autopct='%1.1f%%')
ax.set_ylabel('')
  ```
<img width="315" alt="Screenshot 2025-04-26 at 11 49 04" src="https://github.com/user-attachments/assets/93a5e242-9e8f-4a2b-a435-75898b516c44" />

10 - 
