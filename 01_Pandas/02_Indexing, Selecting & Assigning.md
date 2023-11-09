### #Native_accessors

- Native Python objects provide good ways of indexing data. Pandas carries all of these over, which helps make it easy to start with.
```Python
reviews.country
```

```Python
reviews['country'][0]
```
### #Indexing_in_pandas

- #Index-based-selection
	- To select the first row of data in a DataFrame, we may use the following:
```Python
reviews.iloc[0]
```

- Both `loc` and `iloc` are row-first, column-second. This is the opposite of what we do in native Python, which is column-first, row-second.
- This means that it's marginally easier to retrieve rows, and marginally harder to get retrieve columns. To get a column with `iloc`, we can do the following:
```Python
reviews.iloc[:, 0]
```

```Python
reviews.iloc[:3, 0]
```

```Python
reviews.iloc[1:3, 0]
```

- row as list
```Python
reviews.iloc[[0, 1, 2], 0]
```


- #Label-based-selection
- The second paradigm for attribute selection is the one followed by the `loc` operator: **label-based selection**. In this paradigm, it's the data index value, not its position, which matters.
```Python
reviews.loc[0, 'country']
```

- `iloc` is conceptually simpler than `loc` because it ignores the dataset's indices. When we use `iloc` we treat the dataset like a big matrix (a list of lists), one that we have to index into by position. `loc`, by contrast, uses the information in the indices to do its work. Since your dataset usually has meaningful indices, it's usually easier to do things using `loc` instead. For example, here's one operation that's much easier using `loc`
```Python
reviews.loc[:, ['taster_name', 'taster_twitter_handle', 'points']]
```

### Choosing between `loc` and `iloc`

- When choosing or transitioning between `loc` and `iloc`, there is one "gotcha" worth keeping in mind, which is that the two methods use slightly different indexing schemes.
- `iloc` uses the Python stdlib indexing scheme, where the first element of the range is included and the last one excluded. So `0:10` will select entries `0,...,9`. `loc`, meanwhile, indexes inclusively. So `0:10` will select entries `0,...,10`.
- Why the change? Remember that loc can index any stdlib type: strings, for example. If we have a #DataFrame with index values `Apples, ..., Potatoes, ...`, and we want to select "all the alphabetical fruit choices between Apples and Potatoes", then it's a lot more convenient to index `df.loc['Apples':'Potatoes']` than it is to index something like `df.loc['Apples', 'Potatoet']` (`t` coming after `s` in the alphabet).
- This is particularly confusing when the DataFrame index is a simple numerical list, e.g. `0,...,1000`. In this case `df.iloc[0:1000]` will return 1000 entries, while `df.loc[0:1000]` return 1001 of them! To get 1000 elements using `loc`, you will need to go one lower and ask for `df.loc[0:999]`.
- Otherwise, the semantics of using `loc` are the same as those for `iloc`.

## #Manipulating_the_index

- Label-based selection derives its power from the labels in the index. Critically, the index we use is not immutable. We can manipulate the index in any way we see fit.
- The `set_index()` method can be used to do the job. Here is what happens when we `set_index` to the `title` field:
```python
reviews.set_index("title")
```

## #Conditional_selection

- suppose that we're interested specifically in better-than-average wines produced in Italy.
- We can start by checking if each wine is Italian or not:
```python
reviews.country == 'Italy'
```

```python
reviews.loc[reviews.country == 'Italy']
```

```python
reviews.loc[(reviews.country == 'Italy') & (reviews.points >= 90)]
```

```python
reviews.loc[(reviews.country == 'Italy') | (reviews.points >= 90)]
```

```python
reviews.loc[reviews.country.isin(['Italy', 'France'])]
```

- The second is `isnull` (and its companion `notnull`). These methods let you highlight values which are (or are not) empty (`NaN`). For example, to filter out wines lacking a price tag in the dataset, here's what we would do:
```python
reviews.loc[reviews.price.notnull()]
```


## #Assigning_data

- Going the other way, assigning data to a DataFrame is easy. You can assign either a constant value
```python
reviews['critic'] = 'everyone'
reviews['critic']
```

- Or with an iterable of values:
```python
reviews['index_backwards'] = range(len(reviews), 0, -1)
reviews['index_backwards']
```

