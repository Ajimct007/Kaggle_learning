
## #Summary_functions

- Pandas provides many simple "summary functions" (not an official name) which restructure the data in some useful way. For example, consider the `describe()` method
```python
reviews.points.describe()
```

- for particular column
```python
reviews.taster_name.describe()
```

```python
reviews.points.mean()
```

```python
reviews.taster_name.unique()
```

```python
reviews.taster_name.value_counts()
```

## #Maps

- A **map** is a term, borrowed from mathematics, for a function that takes one set of values and "maps" them to another set of values. 
- In data science we often have a need for creating new representations from existing data, or for transforming data from the format it is in now to the format that we want it to be in later. 
- Maps are what handle this work, making them extremely important for getting your work done!
- There are two mapping methods that you will use often.
- [`map()`](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.map.html) is the first, and slightly simpler one. For example, suppose that we wanted to remean the scores the wines received to 0. We can do this as follows:

```python
review_points_mean = reviews.points.mean()
reviews.points.map(lambda p: p - review_points_mean)
```

- The function you pass to `map()` should expect a single value from the Series (a point value, in the above example), and return a transformed version of that value. `map()` returns a new Series where all the values have been transformed by your function.
- [`apply()`](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.apply.html) is the equivalent method if we want to transform a whole #DataFrame by calling a custom method on each row.

```python
def remean_points(row):
    row.points = row.points - review_points_mean
    return row

reviews.apply(remean_points, axis='columns')
```

