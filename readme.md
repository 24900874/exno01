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
 ### READING THE GIVEN DATA
 ```
import pandas as pd
import numpy as np
df = pd.read_csv('SAMPLEIDS.csv')
df
```
![{241616D3-3311-47AB-8567-5F17A68B1223}](https://github.com/user-attachments/assets/9c92b4ec-7e2f-4a70-aca4-f1e5e1e64f1f)


### GETTING INFORMATION OF THE DATA 

```
df.describe()
```
![{17E3831D-5F54-42B5-A225-FFA3FC7D8768}](https://github.com/user-attachments/assets/1a488327-d465-4a80-804e-ff54023a8bbb)

```
df.info()
```

![{4B1ECAF8-06DF-46CA-9E13-580CDB133EA2}](https://github.com/user-attachments/assets/6c403bbc-5ea9-4ad8-bd1f-43c0ca7a10fd)

```
df.head(4)
```
![image](https://github.com/user-attachments/assets/3d0d360c-2fb9-4261-ae86-93e8b25e0c6f)

```
df.tail(3)
```
![Screenshot 2024-10-18 173458](https://github.com/user-attachments/assets/953790cb-f258-48d3-85c8-997685943f05)

```
df.shape
```
```
(12, 10)
```
### REMOVING NULL VALUES FORM THE DATA 
```
df.isnull()
```
![Screenshot 2024-10-18 173710](https://github.com/user-attachments/assets/8737a9de-0a1f-447b-86bc-7ecccae15ccd)


```
df.isnull().sum()
```
![{DC2E476B-B052-49E3-AA75-962D45B38661}](https://github.com/user-attachments/assets/95caec76-cf9b-40e0-9873-75c3d7062df1)


```
df.isnull().any()
```
![Screenshot 2024-10-18 173937](https://github.com/user-attachments/assets/cba6485a-2fe0-4883-b567-c498dfeae320)

```
df.dropna(axis=0)
```
![Screenshot 2024-10-18 174119](https://github.com/user-attachments/assets/ac668580-a4cc-4d9f-b934-e1c68d7d92f7)

### SAVING THE CLEAN DATA 
```
df = df.dropna(axis=1)
df
```
![Screenshot 2024-10-18 174200](https://github.com/user-attachments/assets/36574d5e-f070-4fb3-a3a7-f769c957e544)

### REMOVING OUTLIERS USING IQR 
```
import seaborn as sns
pf=pd.read_csv('heights.csv')
pf
```
![Screenshot 2024-10-18 174256](https://github.com/user-attachments/assets/0fbfc577-ffc3-4d73-a7f6-cb8ce5785dbe)

```
sns.boxplot(data=pf)
```
![Screenshot 2024-10-18 174452](https://github.com/user-attachments/assets/d05b4b2f-db61-4b8d-ae55-be9829369e72)

```
sns.scatterplot(data=pf)

```
![Screenshot 2024-10-18 174606](https://github.com/user-attachments/assets/c5a4e95e-f9ea-4a6a-8cf3-f0d082e56415)

```

Q1 = pf['height'].quantile(0.25)
Q3 = pf['height'].quantile(0.75)
IQR = Q3 - Q1
LB = Q1 - 1.5 * IQR
UB = Q3 + 1.5 * IQR

outliers = pf[(pf['height'] < LB) | (pf['height'] > UB)]

print("Lower Bound:", LB)
print("Upper Bound:", UB)
print("Outliers:\n", outliers)
```
![image](https://github.com/user-attachments/assets/29036b0e-3e88-4a52-9e7c-f3d4d5f38da3)

```
no_outliers = pf[~((pf['height'] < LB) | (pf['height'] > UB))]
print(no_outliers)
```
![image](https://github.com/user-attachments/assets/1a0ca7ed-d78d-4410-95c2-2413e60c6e30)

```
sns.boxplot(data=no_outliers)
```

![image](https://github.com/user-attachments/assets/5dbe39ef-f3b5-42f1-abbf-760b83669699)

```
sns.scatterplot(data=no_outliers)
```
![image](https://github.com/user-attachments/assets/048c781b-ba2e-4dd9-ae5a-02984be4fe8e)

### REMOVING OUTLIERS OF THE SAME DATA USING Z SCORE
```
import matplotlib.pyplot as plt
import scipy.stats as stats
pf
```
![Screenshot (165)](https://github.com/user-attachments/assets/465cf710-a8bb-4f75-913d-9cfbd685250e)

```
q1=pf['height'].quantile(0.25)
q2=pf['height'].quantile(0.5)
q3=pf['height'].quantile(0.75)

iqr=q3-q1
low= q1-1.5*iqr
high=q3+1.5*iqr

pf1=pf[((pf['height'] >= low) & (pf['height'] <= high))]
pf1
```
![image](https://github.com/user-attachments/assets/e14dc240-c6f4-4030-a3e1-be684893aa81)

```
z=np.abs(stats.zscore(pf['height']))
z
```
![image](https://github.com/user-attachments/assets/81c1e955-6334-4de1-a909-4dc056277dff)

```
pf1 = pf[z<3]
pf1
```
![image](https://github.com/user-attachments/assets/e14dc240-c6f4-4030-a3e1-be684893aa81)


# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method
         
