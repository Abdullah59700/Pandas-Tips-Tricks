**Created By:** **Abdullah Jamil.**\
**DATE:** **8/28/2024**\
**Email:** [Click Here:](abdullahdatascientist@gmail.com)
______

# **Pandas Tips and Tricks**

> This repository is dedicated to sharing practical **tips and tricks for using Pandas**, a powerful Python library for data manipulation and analysis. Whether you're a beginner looking  to  get started or an experienced user seeking to optimize your workflows, you'll find a **variety of helpful techniques here to enhance your data science projects.**

# **What's Inside?**
> - **Common Data Manipulations:** Learn how to efficiently filter, sort, and aggregate your data.
> - **Advanced Operations:** Explore advanced features like pivot tables, merging datasets, and working with time series.
> - **Performance Tips:** Discover ways to speed up your data processing with vectorized operations and memory optimization.
> - **Useful Shortcuts:** Save time with handy shortcuts and lesser-known Pandas functions.
 
# **How to Use This Repository**
> - **Explore the Notebooks:** Each Jupyter Notebook covers a specific topic, complete with code examples and explanations.
> - **Contribute:** Have a tip or trick to share? Feel free to open a pull request!
> - **Stay Updated:** Watch the repository to stay updated with the latest tips and additions.

*****

# There are the Following Pandas Tips & Tricks with some Important example:
____
## **01- How to find the version.**
```
import pandas as pd 
pd.__version__
```

```
pd.show_versions()
```
____
## 02- Make a DataFrame.
```
df = pd.DataFrame({'A col':[1,2,3], 'B col':[4,5,6]})
df
```

```
#numpy array use to create a dataframe
import numpy as np
arr = np.array([[1,2,3] ,[4,5,6] , [7,8,9]])
arr
pd.DataFrame(arr)
```

```
#numpy arry dataframe 
pd.DataFrame(np.random.rand(10,8) , columns=list('abcdefgh'))
```
_____

## 03- How to rename colums?
```
df = pd.DataFrame({'A col':[1,2,3], 'B col':[4,5,6]})
df
```

```
df.rename(columns={'A col': "A" , 'B col': "B"} , inplace=True)
df
```

```
# rename columns.
df.columns=['A_A' , "B_B"]  
df  
```

```
# to replace any characters or string. 
df.columns=df.columns.str.replace('_' , '*')
df
```

```
# Adding prefix to columns
df=df.add_prefix("col_")
df
```

```
# Adding Suffix in columns 
df=df.add_suffix("_col")
df
```

```
df.columns=["A" , "B"]
df
```
______

## 04- Using template data 
```import pandas  as pd 
import numpy as np 
import seaborn as sns 

df_1 = sns.load_dataset("tips")
df_1.head()
```

```
# summary 
df.describe()
```

```
# columns name 
df_1.columns
```
________

## 05- Save the Data 
### Read and write data

## 06- Reverse Row order. 
```
import pandas as pd 
import numpy as np 

kashti= sns.load_dataset("titanic")
kashti.head()

```

```
kashti.loc[::-1]
```

```
df.loc[::-1].reset_index(drop=True).head()
```
_____

## 07- Reverse Columns order
```
df.loc[: , ::-1].head()
```
_________

## 08- Select a colums  D type
```
df.dtypes
```

```
# only select those who has numeric type.
numeric_df = df.select_dtypes(include=[np.number])
numeric_df.head()
```

```
# another way
df.select_dtypes(include=['number']).head()
```

```
# only select those who has object type 
df.select_dtypes(include=['object']).head()
```

```
# select those who having multiple type 
df.select_dtypes(include=['number' , 'object' , 'category']).head()
```

```
df.select_dtypes(exclude=['number']).head()
```
____

## 09- Convert string to number
```
df = pd.DataFrame({"col_a": [1,2,3,4,5,6,7],
                    "col_b": [1,2,3,4,5,6,7]})
df
```

```
df.dtypes
```

```
df.astype({"col_a": "float64" , "col_b": "float64"}).dtypes
```

```
pd.to_numeric(df["col_a"], errors="coerce")
df.dtypes
```
________

## 10- Reduce Data frame size
```
import pandas as pd 
import numpy as np 
import seaborn as sns 

df = sns.load_dataset("titanic")
df.head()
df.shape
```

```
df.info(memory_usage="deep")
```

```
df.sample(frac=0.1).shape
```

```
df.info()
```
_____

## 11- Copy Data from clipboard
```
# Datasets download 
import pandas as pd 
import seaborn as sns 

kashti= sns.load_dataset("titanic")
kashti.to_excel("kashti.xlsx")
```

```
# Read data from clipboard 
# To copy data and run this command.
import pandas as pd
kashti=pd.read_clipboard()
kashti.head()
```
____

## 12- split dataframe into tow subsets 
```
import pandas as pd 
import seaborn as sns 
kashti= sns.load_dataset("titanic")
kashti.head()

```

```
len(kashti)
```

```
kashti.shape
```

```
from random import random

kashti_1 = kashti.sample(frac=0.50 , random_state=1)
kashti_1.shape
```

```
kashti_2 = kashti.drop(kashti_1.index)
kashti_2.shape
```

```
kashti_1.head()
```

```
kashti_2.head()
```

```
len(kashti_1) + len(kashti_2)
```
_____

## 13- join to data sets.
```
df1 = kashti_1.append(kashti_2)
df1
```

```
df1 =len(kashti_1) + len(kashti_2)
df1
```
______

## 14- Filtering the datasets.

```
df.head()
```

```
df.sex.unique()
```

```
df[df.sex=='male'].head()
```

```
df.embark_town.unique()
```

```
df[((df.embark_town=="Southampton") |
   (df.embark_town=='Queenstown'))  &  
    (df.sex=='female')]
```

```
df[df.embark_town.isin(['Queenstown' , 'southampton'])].head()
```

```
df[df.age>30]
```

```
df[df.age<30].shape
```
______

## 15- Filtering By large categories

```
df.age.value_counts().nlargest(3).index
```

```
counts=df.embark_town.value_counts().nlargest(3)
counts.nlargest(3).index
```

```
counts=df.who.value_counts().nlargest(3)
counts.nlargest(3).index
```

```
df[df.who.isin(counts.nlargest(2).index)].head()
```
_____

## 16- Spliting a string into multiple columns.

```
import pandas as pd 

df=pd.DataFrame({'name':["john Alex" ,"James Alex","Joseph Alex", "David Alex"],
                 'location':['Athens. USA' , 'Auburn. USA' , 'Bessemer. USA' , 'Birmingham USA']})
df
```

```
# slpit a columns into tow columns.
df.name.str.split(" " , expand=True)
```

```
# adding those split into those new columns 
df[["first name" , "last name"]]=df.name.str.split(" " , expand=True)
df
```

```
df.location.str.split(" " , expand=True)
```

```
df[["city name" , "country name"]]=df.location.str.split(" " , expand=True)
df
```

```
# refine data manuplucation
df = df[["first name" , "last name" , "city name" , "country name"]]
df
```
______

##  17- Aggregrate by multiple groups/function

```
# libraries 
import pandas as pd 
import seaborn as sns 
import numpy as np 

# import data sets
df = sns.load_dataset("titanic")
df.head()

```

```
df.groupby('sex').count()
```

```
df.groupby('who').count()
```

```
len(df.groupby("who"))
```

```
df.head()
```

```
df.groupby(["sex" , "who" , "pclass"]).count()
```
_________

## 18- slect specfics Row and Colums 
```
df.head()
```

```
# slect columns
df[["sex", "class"]].head()
```

```
df.describe()
```

```
df.describe().loc[['min' , '25%' ,'50%', '75%', 'max' ]]

# 0r 
df.describe().loc['mean' : 'max' ]
```

```
df.describe().loc['mean' : 'max' , :]
```

```
df.describe().loc['mean':'max' , 'survived':'age']
```
_____

## 19- reshape multiindex series

```
df.head()
```

```
df.survived.mean()
```

```
df.groupby(['sex', 'class']).survived.mean()
```

```
df.groupby(['sex', 'class']).survived.mean().unstack()
```
_______

## 20- continuons to catagorical data conversion 
```
df.head()

```

```
df.age.head()
```

```
# creating bins 
pd.cut(df.age , bins= [0 , 18 , 25 , 99] , labels=['child' , 'young_adult' , 'adult']).head()
df['new_age'] = pd.cut(df.age , bins= [0 , 18 , 25 , 99] , labels=['child' , 'young_adult' , 'adult']).head()
df.head()
```
_______

## 21-convet  one set of value into anotherone 

```
df.sex.head()
```

```
df.sex.map({'male': 0  , 'female' : 1})

```

```
df['sex_number'] = df.sex.map({'male': 0  , 'female' : 1})
df.head()
```

```
df.embarked.head()
```

```
df.embarked.unique()
```

```
df['embarked_number']=df.embarked.factorize()[0]
df.head()

```
_____

## 22- transpose a wide data frame 

```
# libraries 
import pandas as pd 
import seaborn as sns 
import numpy as np
# creating a new data frame 
df = pd.DataFrame(np.random.rand(200,25))
df.head(10)
```

```
df.head(10).T
```

```
df.describe()
```

```
df.describe().T
```
______

**Regards: 
Abdullah Jamil**

__**Thanks for view My Repo.**__
______
_____
____

