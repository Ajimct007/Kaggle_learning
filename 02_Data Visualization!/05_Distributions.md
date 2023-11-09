
# #Histograms

- Say we would like to create a **histogram** to see how petal length varies in iris flowers. We can do this with the `sns.histplot` command.
```python
# Histogram 
sns.histplot(iris_data['Petal Length (cm)'])
```

![[Pasted image 20230928174829.png]]
# #Density_plots

- The next type of plot is a **kernel density estimate (KDE)** plot. In case you're not familiar with KDE plots, you can think of it as a smoothed histogram.
- To make a KDE plot, we use the `sns.kdeplot` command. Setting `shade=True` colors the area below the curve (_and `data=` chooses the column we would like to plot_).
```python
# KDE plot 
sns.kdeplot(data=iris_data['Petal Length (cm)'], shade=True)
```

![[Pasted image 20230928174849.png]]

# #2D_KDE_plots

- We're not restricted to a single column when creating a KDE plot. We can create a **two-dimensional (2D) KDE plot** with the `sns.jointplot` command.
- In the plot below, the color-coding shows us how likely we are to see different combinations of sepal width and petal length, where darker parts of the figure are more likely.
```python
# 2D KDE plot
sns.jointplot(x=iris_data['Petal Length (cm)'], y=iris_data['Sepal Width (cm)'], kind="kde")
```

![[Pasted image 20230928174959.png]]

- Note that in addition to the 2D KDE plot in the center,
	- the curve at the top of the figure is a KDE plot for the data on the x-axis (in this case, `iris_data['Petal Length (cm)']`), and
	- the curve on the right of the figure is a KDE plot for the data on the y-axis (in this case, `iris_data['Sepal Width (cm)']`).


# #Color-coded-plots

- For the next part of the tutorial, we'll create plots to understand differences between the species.
- We can create three different histograms (one for each species) of petal length by using the `sns.histplot` command (_as above_).
	- - `data=` provides the name of the variable that we used to read in the data
	- `x=` sets the name of column with the data we want to plot
	- `hue=` sets the column we'll use to split the data into different histograms
```python
# Histograms for each species
sns.histplot(data=iris_data, x='Petal Length (cm)', hue='Species')

# Add title
plt.title("Histogram of Petal Lengths, by Species")
```

![[Pasted image 20230928175304.png]]


- We can also create a KDE plot for each species by using `sns.kdeplot` (_as above_). The functionality for `data`, `x`, and `hue` are identical to when we used `sns.histplot` above. Additionally, we set `shade=True` to color the area below each curve.
```python
# KDE plots for each species
sns.kdeplot(data=iris_data, x='Petal Length (cm)', hue='Species', shade=True)

# Add title
plt.title("Distribution of Petal Lengths, by Species")
```

![[Pasted image 20230928175344.png]]

