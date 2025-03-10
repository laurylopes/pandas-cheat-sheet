
# Pandas Cheat Sheet
<img width="200" alt="image" src="https://github.com/user-attachments/assets/a6f18a27-6575-462c-b9c1-6eaf0b495565">

Hello, and welcome to my Pandas cheat sheet!

### Columns manipulation
``` python
# drop columns
df.drop(['col1', 'col2'])

# rename columns
df.rename(columns={'Old_Name' : 'New_Name'})

# keep only selected columns
df = df[['col1', 'col2']]
```
``` python
# open all columns in df
pd.set_option('max_columns', None)
```

### Concatenation
``` python
# concat several df 
pd.concat([df1, df2, df3], ignore_index=True)

# concat excel sheets in file
df = pd.concat(pd.read_excel('file.xlsx', sheet_name=None), ignore_index=True)

# concat all files in a folder
import os
import pandas as pd

# 1. list data in a folder called data
os.listdir('Data') 

# 2. create a list of files
files_list = os.listdir('Data')

# 3. create a df for each file in list 
df_files = [pd.read_csv(os.path.join('Data', file), on_bad_lines ='skip', skiprows = 3, sep = '\t', parse_dates=False) for file in files_list]

# 4. concat all df_files into df
df = pd.concat(df_files, ignore_index =False)
```

### String manipulation 
``` python
# contains 
df['col'].str.contains('containString')

# replace
df['col'].str.replace('old', 'new')

# start with
df['col'].str.startswith('A')
```

### Date Time Format
``` python
# transform data into dateTime value type
pd.to_datetime(df['col'])

# extract year, month and day and create new column with data
df['year'] = df['col'].dt.year
df['month'] = df['col'].dt.month
df['day'] = df['col'].dt.day

# deal with erros
pd.to_datetime(df['col'], errors='coerce')
```

### Duplicates
``` python
# drop duplicates
df.drop_duplicates(subset = 'column')

# count duplicates
df['col1'].duplicated().sum()

# count unique values
df['col1'].nunique()
```

### Group By
``` python
# group by on more than one column

# 1. create disctionnary with 'column' : 'function'
dico_agg = {'col1': ['agg1'], 'col2': ['agg2'], 'col3' : ['agg3']}

# 2. run group by and aggregate
df.groupby('col').agg(dico_agg)
```

### Order By
``` python
# sort values by column
sort_values(by=['col'], ascending=False)
```

### Selection
``` python
# iloc
df.iloc[rows_index, col_index]
df.iloc[:,:8] # select all rows column zero to 8

# loc 
df.loc['rows_values', 'col_name'] # select all rows 
df.loc['string', 'col_name'].str.contains('a') # select all rows in col where value contains 'a'

# loc and iloc are uselful not only to select but also to filter the dataframe with a certain condition like the example above

```

### Anti-join
``` python
# inner join
merge = pd.merge(df1, df2, on ='key', how='inner')

# keep values of interest to filter => equivalent to SELECT DISTINCT in SQL
array = merge['pKey_column'].unique() 

# select all the values in df that are different from the values in array
df[~df['pKey_column'].isin(array)]
```

### Print values
``` python
# f print python
print(f' My name is : {name} and I am {age} years old')
```
