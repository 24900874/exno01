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

![info](https://github.com/user-attachments/assets/da2a5f9f-0988-487f-81ce-93eef92e81b0)
```
df.heaad()
```
![head](https://github.com/user-attachments/assets/de102b53-0ca9-493f-b811-91bc7e8f97b4)
```
df.tail()
```
![tail](https://github.com/user-attachments/assets/858ba30e-756d-4ed4-a398-34c35abf79f9)

```
df.shape
```
```
(21, 12)
```
### REMOVING NULL VALUES FORM THE DATA 
```
df.isnull()
```
![is null](https://github.com/user-attachments/assets/74553a9d-0c97-4a14-9de3-ecaac3960caf)

```
df.isnull().sum()
```
![is null sum](https://github.com/user-attachments/assets/50e322b2-1d19-4f6a-8083-2a4940b271a2)

```
df.isnull().any()
```
![is null any](https://github.com/user-attachments/assets/fd184f80-613a-4c51-9528-e6d9e9c4c3d7)

```
df.dropna(axis=0)
```
![dropna](https://github.com/user-attachments/assets/afbad0f5-244d-4033-be98-e2f14faa6d5b)

### SAVING THE CLEAN DATA 
```
df = df.dropna(axis=0)
df
```
![dropna](https://github.com/user-attachments/assets/23b194fe-fc59-4156-884e-3f59757d8445)

### REMOVING OUTLIERS USING IQR 
```
import seaborn as sns
pf=pd.read_csv('heights.csv')
pf
```
![Screenshot (165)](https://github.com/user-attachments/assets/465cf710-a8bb-4f75-913d-9cfbd685250e)

```
sns.boxplot(data=pf)
```
![image](https://github.com/user-attachments/assets/ae069561-4b2e-4cee-9769-83b6f2174c89)
```
sns.scatterplot(data=pf)

```
![image](https://github.com/user-attachments/assets/1170d545-0a22-4bfc-ba03-d8c12d0b043f)
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
         
