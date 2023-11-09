# 1) #Creating_data

- There are two core objects in pandas: the #DataFrame and the #Series .
### [DataFrame](https://www.kaggle.com/code/residentmario/creating-reading-and-writing#DataFrame)
- A DataFrame is a table. It contains an array of individual _entries_, each of which has a certain _value_. Each entry corresponds to a row (or _record_) and a _column_.
```Python
pd.DataFrame({'Yes': [50, 21], 'No': [131, 2]})
```


### [Series](https://www.kaggle.com/code/residentmario/creating-reading-and-writing#Series)
- A Series, by contrast, is a sequence of data values. If a #DataFrame is a table, a #Series is a list. And in fact you can create one with nothing more than a list:
```Python
pd.Series([30, 35, 40], index=['2015 Sales', '2016 Sales', '2017 Sales'], name='Product A')
```


### #Reading_data_files
