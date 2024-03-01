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

## data cleaning process
```py
#import the file you requied
#import the pandas and named as pd
import pandas as pd
df=pd.read_csv("/SAMPLEIDS.csv")
df
```
![](/ouput1.png)


```py
df.head()        #display first 5 rows
```
![](/output2.png)


```py
df.tail()       #display last 5 rows
```
![](/output3.png)

```py
df.describe()
```
![](/output4.png)

```py
df.info()
```
![](/output5.png)


```py
df.shape
```
![](/output6.png)

```py
df.isnull().sum()
```
![](/output7.png)


```py
df.nunique()
```
![](/output8.png)

```py
df['GENDER'].value_counts()
```
![](/output9.png)

```py
mm=df.TOTAL.mean()
mm
```
![](/ouput9.png)

```py
df.TOTAL.fillna(mm,inplace=True)
df
```
![](/output10.png)


```py
x=df.M4.min()
x
```
![](/output11.png)

```py
df.M4.fillna(x,inplace=True)
df
```
![](/output12.png)

```py
df.duplicated()
```
![](/output13.png)

```py
df.drop_duplicates(inplace=True)
df
```
![](/output14.png)


```py
df['DOB']
```
![](/output15.png)

```py
y=pd.to_datetime(df['DOB'])
```
![](/output16.jpg)


```py
df['DOB']=pd.to_datetime(df['DOB'])
```
![](/output17.jpg)

```py
import seaborn as sns
sns.heatmap(df.isnull(),yticklabels=False,annot=True)
```
![](/output18.jpg)

```py
df.dropna(inplace=True)
sns.heatmap(df.isnull(),yticklabels=False,annot=True)
```
![](/output19.jpg)

```py
df.shape
```
![](/output20.jpg)


## outlayer detection and removal

```py
import pandas as pd
import seaborn as sns
import numpy as np
age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af
```
![](/output21.png)

```py
box_graph=sns.boxplot(data=age)
print(box_graph)
```
![](/output22.png)

```py
sns.scatterplot(age)
```
![](/output23.png)

```py
q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)
iqr=q3-q1
print(iqr)

```
![](/output24.png)

```py
Q1=np.percentile(af,25)
Q3=np.percentile(af,75)
IQR=Q3-Q1
print(IQR)
```
![](/outpyu25.png)

```py
lower_bond=Q1-1.5*IQR
upper_bond=Q3+1.5*IQR
outliers=[x for x in age if x< lower_bond or x>upper_bond]
print("Q1:",Q1)
print("Q3:",Q3)
print("IQR:",IQR)
print("lower bond :",lower_bond)
print("upper bond :",upper_bond)
print("outliers :",outliers)
```
![](/output26.png)

```py
af=af[((af>=lower_bond)&(af<=upper_bond))]
af
```
![](/output27.png)

```py
af.dropna()
```
![](/output28.png)

```py
sns.boxplot(data=af)
```
![](/output29.png)

```py
sns.scatterplot(af)
```
![](/output30.png)

```py
import scipy as stats
data={'Weight':[12,15,18,21,24,27,30,33,36,42,45,48,51,54,57,60,63,66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}
df=pd.DataFrame(data)
df
```
![](/output31.png)

```py
sns.boxplot(data=df)
```
![](/output32.png)

```py
   
z=np.abs(stats.zscore(df))
   
       # (or)

val=[12,15,18,21,24,27,30,33,36,42,45,48,51,54,57,60,63,66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]

def display(val):
  out=[]
  ts=3
  m=np.mean(val)
  sd=np.std(val)
  for i in val:
    z=(i-m)/sd
    if(np.abs(z)>ts):
      out.append(i)
    return out
op=display(val)
print(op)

```

![](/output33.jpg)


```py
print(df[z['Weight']>3])
```
![](/output34.jpg)
# Result
Hence the Data Cleaning process is performed successfully on the given data using python code




