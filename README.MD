# Analyzing Police data in South and North Wales between 2019-2021

The report is part of a course work in principles of computing module in Python from a grad programme.

Making it available publicly as a reference learning materia for anyone learning data analysis with python and the use of pandas, seaborn, plotly, matplotlib.plyplot, and folium for heat map generation.

- First we read the data into a [dataframe](https://www.tutorialspoint.com/python_pandas/python_pandas_dataframe.htm) in pandas (A Data frame is a two-dimensional data structure, i.e., data is aligned in a tabular fashion in rows and columns).

  Since we're reading in multiple csv files, we have to append each file path into an array and load into panda.

```py
filepaths = [f for f in os.listdir("datasets") if f.endswith('.csv')]
path_ = []
count = 0
for file in filepaths:
  df = pd.read_csv('./datasets//'+file, index_col=None ,header=0, na_values='NaN', keep_default_na=False)
  count = count+(len(df))
  path_.append(df)

crimeData = pd.concat(path_,axis=0)
```

- We can see information about the data with

```py
  crimeData.info()
```

The data has over 600 thousand rows of data, 12 columns.

- Cleaning the data
Inspecting the dataset with .info(), we can see some columns have null values in them, some in wrong data type like objects when they should either dates, numbers etc.

```py
# Clean Data, remove nulls, duplicates and NaNs
crimeData.isna().sum()
crimeData.duplicated(subset=None, keep='first').count()
crimeData.drop_duplicates()
crimeData = crimeData.iloc[:,[0,1,2,3,4,5,6,7,8,9,10,11]]

crimeData.dropna(inplace=True)

crimeData['Latitude'] = pd.to_numeric(crimeData['Latitude'], downcast='float')
crimeData['Longitude'] = pd.to_numeric(crimeData['Longitude'], downcast='float')

crimeData.info()
```

- Performing analysis and plotting Charts
After cleaning up our dataset, we can begin plotting graphs, charts, carry out statistical analysis, read meaningful information out of the data.

In getting meaningful information out of your data, you can plot basic graphs for visualization and better understanding before we begin answering business questions.

In this case, we are interested in seeing the difference between crimes rate, types in south and north wales, what factors could influence our findings and so on.

full jupyter notebook can can be found here [analysis.ipynb](./analysis.ipynb).

I hope you find something helpful with this.
