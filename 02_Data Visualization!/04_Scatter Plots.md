
# #Scatter_plots


```python
sns.scatterplot(x=insurance_data['bmi'], y=insurance_data['charges'])
```

- To double-check the strength of this relationship, you might like to add a **regression line**, or the line that best fits the data. We do this by changing the command to `sns.regplot`.

```python
sns.regplot(x=insurance_data['bmi'], y=insurance_data['charges'])
```

# #Color-coded-scatter-plots

- We can use scatter plots to display the relationships between (_not two, but..._) three variables! One way of doing this is by color-coding the points.

- For instance, to understand how smoking affects the relationship between BMI and insurance costs, we can color-code the points by `'smoker'`, and plot the other two columns (`'bmi'`, `'charges'`) on the axes.

```python
sns.scatterplot(x=insurance_data['bmi'], y=insurance_data['charges'], hue=insurance_data['smoker'])
```

- This scatter plot shows that while nonsmokers to tend to pay slightly more with increasing BMI, smokers pay MUCH more.
- To further emphasize this fact, we can use the `sns.lmplot` command to add two regression lines, corresponding to smokers and nonsmokers. (_You'll notice that the regression line for smokers has a much steeper slope, relative to the line for nonsmokers!_)

```python
sns.lmplot(x="bmi", y="charges", hue="smoker", data=insurance_data)
```

![[Pasted image 20230928172906.png]]

- The `sns.lmplot` command above works slightly differently than the commands you have learned about so far:
	- Instead of setting `x=insurance_data['bmi']` to select the `'bmi'` column in `insurance_data`, we set `x="bmi"` to specify the name of the column only.
	- Similarly, `y="charges"` and `hue="smoker"` also contain the names of columns.
- We specify the dataset with `data=insurance_data`.

```python
sns.swarmplot(x=insurance_data['smoker'],
              y=insurance_data['charges'])
```

![[Pasted image 20230928173008.png]]

- Among other things, this plot shows us that:
	- on average, non-smokers are charged less than smokers, and
	- the customers who pay the most are smokers; whereas the customers who pay the least are non-smokers.