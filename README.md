# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
from google.colab import drive
drive.mount('/content/drive')

ls drive/MyDrive/DS2024/Data_set.csv

# **Data Cleaning**

import pandas as pd
df=pd.read_csv('drive/MyDrive/DS2024/Data_set.csv')
df
![Screenshot 2024-12-13 152317](https://github.com/user-attachments/assets/1cb7ce84-167b-4b22-af25-98c2afa859b9)

# CHECK OUT NULL VALUES IN DATA SET USING FUNCTION
df_null=df.isnull()
df_null
![Screenshot 2024-12-13 152317](https://github.com/user-attachments/assets/fbfe4cf5-395b-4d96-a591-8c07c8d72ec2)

# DISPLAY THE SUM ON NULL VALUES IN EACH ROWS
df_null_sum=df.isnull().sum()
df_null_sum
![Screenshot 2024-12-13 152306](https://github.com/user-attachments/assets/ab125b7e-c8ad-4ee9-8778-bf794a0221ff)

# DROP NULL VALUES
df_dropna=df.isnull().dropna()
df_dropna
![Screenshot 2024-12-13 152258](https://github.com/user-attachments/assets/2b9178ca-c966-4a35-a551-42882a4d71a0)

# FILL NULL VALUES WITH CONSTANT VALUE "O"
df_nafill_0=df.fillna(0)
df_nafill_0
![Screenshot 2024-12-13 152252](https://github.com/user-attachments/assets/de741975-1ac8-4d24-9da4-eda22268b0dc)

# FILL NULL VALUES WITH ffill METHOD
df_ffill=df.ffill()
df_ffill
![Screenshot 2024-12-13 152241](https://github.com/user-attachments/assets/246bf1f4-3730-4ab1-ae0a-ed554fbf7f49)

# FILL NULL VALUES WITH bfill METHOD
df_bfill=df.bfill()
df_bfill
![Screenshot 2024-12-13 152230](https://github.com/user-attachments/assets/b6d3e1e1-719c-4e0e-a2c4-f55555c23c83)

# CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES
df_mean1=df['num_episodes'].fillna(df['num_episodes'].mean())
df_mean1
![Screenshot 2024-12-13 152203](https://github.com/user-attachments/assets/c31c3236-f59c-46e4-a135-ff66cefc0bd0)

df_mean2=df['rating'].fillna(df['rating'].mean())
df_mean2
![Screenshot 2024-12-13 152158](https://github.com/user-attachments/assets/836c5dbe-bdef-4ffa-bd32-6a8b348e62aa)

df_mean3=df['current_overall_rank'].fillna(df['current_overall_rank'].mean())
df_mean3
![Screenshot 2024-12-13 152153](https://github.com/user-attachments/assets/6c97e751-904b-41e3-bca4-70cab42eff65)
df_mean4=df['lifetime_popularity_rank'].fillna(df['lifetime_popularity_rank'].mean())
df_mean4
![Screenshot 2024-12-13 152148](https://github.com/user-attachments/assets/120bc058-be7b-43b0-80b7-6bcbb6b2228f)

df_mean5=df['watchers'].fillna(df['watchers'].mean())
df_mean5
![Screenshot 2024-12-13 152140](https://github.com/user-attachments/assets/267e6358-9cc0-49ee-b074-614f156dfeee)

# DROP NULL VALUES
df_dropna=df.dropna()
df_dropna
![Screenshot 2024-12-13 152130](https://github.com/user-attachments/assets/bafb10e0-88e2-4843-9b2a-e970122927fc)

# **Outlier Detection and Removal - IQR**

import pandas as pd
import seaborn as sns

age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af
![Screenshot 2024-12-13 152117](https://github.com/user-attachments/assets/d0b00c3b-a556-4800-9371-3d2359c1c5ea)

# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
sns.boxplot(af)
![Screenshot 2024-12-13 152111](https://github.com/user-attachments/assets/c669577b-e09b-45f6-9f5f-b4ecd8d3c9ef)

sns.scatterplot(af)
![Screenshot 2024-12-13 152104](https://github.com/user-attachments/assets/fd40460c-d584-49c7-93db-260936e435d3)

q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)


iqr=q3-q1
iqr
![Screenshot 2024-12-13 152055](https://github.com/user-attachments/assets/dc8db04d-613c-4078-b1dd-79606ae3eb8a)

import numpy as np

Q1=np.percentile(af,25)
Q2=np.percentile(af,50)
Q3=np.percentile(af,75)

IQR=Q3-Q1

lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR

outliers = [x for x in age if x < lower_bound or x > upper_bound]


print('Q1:',Q1)
print('Q3:',Q3)
print('IQR:',IQR)
print('Lower bound:',lower_bound)
print('Upper bound:',upper_bound)
print('Outliers:',outliers)
![Screenshot 2024-12-13 152049](https://github.com/user-attachments/assets/0f0db811-1391-4109-ab78-cf9443962d48)

af=af[((af>=lower_bound)&(af<=upper_bound))]
af
![Screenshot 2024-12-13 152044](https://github.com/user-attachments/assets/6bf2ae4a-354e-479b-b829-4ce3334a2fcf)
af.dropna()
![Screenshot 2024-12-13 152038](https://github.com/user-attachments/assets/b4b34cef-e98a-43bd-883c-12a18ee7fa92)

sns.boxplot(af)
![Screenshot 2024-12-13 152031](https://github.com/user-attachments/assets/8432af59-1790-4f8a-ae47-7113e886ce4c)

sns.scatterplot(af)
![Screenshot 2024-12-13 152023](https://github.com/user-attachments/assets/41d1cdc5-11df-4ad8-a47c-fadd5e89201a)

# **Z Score**

from scipy import stats #STATS METHOD IS USED TO IMPLEMENT Z SCORE METHOD
import numpy as np
import pandas as pd
import seaborn as sns

data=[1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90,93]
df=pd.DataFrame(data)

# USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
sns.boxplot(df)
![Screenshot 2024-12-13 152014](https://github.com/user-attachments/assets/e955c960-71d7-487b-811b-e4b25fbce5dd)

mean=np.mean(data)
mean
![Screenshot 2024-12-13 152008](https://github.com/user-attachments/assets/2f43e6b7-51b9-4fdb-8b90-320a7443c40d)

std=np.std(data)
std
![Screenshot 2024-12-13 152003](https://github.com/user-attachments/assets/f19df514-f6c9-4c95-b256-eccedb9bad01)

# PERFORM Z SCORE METHOD AND DETECT OUTLIER VALUES
z=np.abs(stats.zscore(df))
z
![Screenshot 2024-12-13 151958](https://github.com/user-attachments/assets/686e220c-9426-40ba-958a-2ea1ef381b2e)

threshold=3
outliers = df[abs(df) > 3]
print("Outliers:")
print(outliers)
![Screenshot 2024-12-13 151927](https://github.com/user-attachments/assets/2e4a6653-1457-48d8-ad2b-d9261b4b6d1b)

# Remove outliers
df_cleaned = df[(z <= threshold)]
df_cleaned
![Screenshot 2024-12-13 151916](https://github.com/user-attachments/assets/257d8c8c-a2d6-485c-bdb7-113b12e57df7)

# USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED
sns.boxplot(df_cleaned)
![Screenshot 2024-12-13 151849](https://github.com/user-attachments/assets/b929bc5d-19b0-4854-a286-df40786aeb22)

sns.scatterplot(df_cleaned)
![Screenshot 2024-12-13 151842](https://github.com/user-attachments/assets/0deafbe2-7fa1-4b1e-9e44-fcd67132cc57)

# Result

         The process of data cleaning code is executed successfully.
