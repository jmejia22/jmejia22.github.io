# Blog Post 0: Visualization of Palmer Penguins

In this blog post, we will be taking a look at the Palmer Penguins data set from PIC 16A and provide a tutorial on how to create visualizations from the data. More specifically, we will be using the **Pandas** and **Seaborn** packages from Python to achieve our goal. To begin this process, we will start by importing the **Pandas** package and grabbing our data via a URL link using the **read_csv()** function from **Pandas** to read it into our notebook. We name the data set as **penguins** which will be a **Data Frame** for which we can use **Pandas** to perform operations on it. 


```python
import pandas as pd
url = "https://raw.githubusercontent.com/PhilChodrow/PIC16B/master/datasets/palmer_penguins.csv"
penguins = pd.read_csv(url)
```

We now have our data and are ready to begin working towards our goal. First we will display the first couple rows of the data set to get a sense of what columns we are working with as well as the values/types of these respective columns. To do so, we will use the **.head()** function from **Pandas**.


```python
penguins.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>studyName</th>
      <th>Sample Number</th>
      <th>Species</th>
      <th>Region</th>
      <th>Island</th>
      <th>Stage</th>
      <th>Individual ID</th>
      <th>Clutch Completion</th>
      <th>Date Egg</th>
      <th>Culmen Length (mm)</th>
      <th>Culmen Depth (mm)</th>
      <th>Flipper Length (mm)</th>
      <th>Body Mass (g)</th>
      <th>Sex</th>
      <th>Delta 15 N (o/oo)</th>
      <th>Delta 13 C (o/oo)</th>
      <th>Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>PAL0708</td>
      <td>1</td>
      <td>Adelie Penguin (Pygoscelis adeliae)</td>
      <td>Anvers</td>
      <td>Torgersen</td>
      <td>Adult, 1 Egg Stage</td>
      <td>N1A1</td>
      <td>Yes</td>
      <td>11/11/07</td>
      <td>39.1</td>
      <td>18.7</td>
      <td>181.0</td>
      <td>3750.0</td>
      <td>MALE</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Not enough blood for isotopes.</td>
    </tr>
    <tr>
      <th>1</th>
      <td>PAL0708</td>
      <td>2</td>
      <td>Adelie Penguin (Pygoscelis adeliae)</td>
      <td>Anvers</td>
      <td>Torgersen</td>
      <td>Adult, 1 Egg Stage</td>
      <td>N1A2</td>
      <td>Yes</td>
      <td>11/11/07</td>
      <td>39.5</td>
      <td>17.4</td>
      <td>186.0</td>
      <td>3800.0</td>
      <td>FEMALE</td>
      <td>8.94956</td>
      <td>-24.69454</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>PAL0708</td>
      <td>3</td>
      <td>Adelie Penguin (Pygoscelis adeliae)</td>
      <td>Anvers</td>
      <td>Torgersen</td>
      <td>Adult, 1 Egg Stage</td>
      <td>N2A1</td>
      <td>Yes</td>
      <td>11/16/07</td>
      <td>40.3</td>
      <td>18.0</td>
      <td>195.0</td>
      <td>3250.0</td>
      <td>FEMALE</td>
      <td>8.36821</td>
      <td>-25.33302</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>PAL0708</td>
      <td>4</td>
      <td>Adelie Penguin (Pygoscelis adeliae)</td>
      <td>Anvers</td>
      <td>Torgersen</td>
      <td>Adult, 1 Egg Stage</td>
      <td>N2A2</td>
      <td>Yes</td>
      <td>11/16/07</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Adult not sampled.</td>
    </tr>
    <tr>
      <th>4</th>
      <td>PAL0708</td>
      <td>5</td>
      <td>Adelie Penguin (Pygoscelis adeliae)</td>
      <td>Anvers</td>
      <td>Torgersen</td>
      <td>Adult, 1 Egg Stage</td>
      <td>N3A1</td>
      <td>Yes</td>
      <td>11/16/07</td>
      <td>36.7</td>
      <td>19.3</td>
      <td>193.0</td>
      <td>3450.0</td>
      <td>FEMALE</td>
      <td>8.76651</td>
      <td>-25.32426</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



Before proceeding to the visualization step, we notice that there are some columns in our data set **(headers in bold)** that do not provide very interesting information that is worth including in our visualization of the data. For instance the columns: **studyName, Sample Number, Individual ID, Date Egg, and Comments** would not be of much interest to visualize. For this reason we will drop these columns so that our data is cleaner and only contains variables we are interested in visualizing. We will do so using the **.drop()** function. 


```python
drop_columns = ["studyName","Sample Number", "Individual ID", "Date Egg", "Comments"]
penguins = penguins.drop(drop_columns,axis = 1)
```

We recall from PIC 16A that in row 336 of the data set, the **Sex** column is occupied by the string "." which does not make much sense. Thus we will choose to drop this row from the penguins data frame once again using the **.drop()** function. 


```python
penguins = penguins.drop(336)
```

For further data cleaning purposes and for the sake of keeping our visuals clean, we will replace the entire formal species name with the first word (for example in the first row, **Adelie Penguin (Pygoscelis adelie)** will become **Adelie**). We can achieve this task using **Pandas** and string operations by first splitting the string in the **Species** column and then getting the first entry of the list. Note that before each string operation we must include **str**. To get the first entry of the list we will call **.get(0)** (0 corresponds to first entry because of zero-based indexing).


```python
penguins["Species"] = penguins["Species"].str.split().str.get(0)
```

Our last cleaning objective will be to drop the rows that contain **N/A** values. This is because we want to work with numerical data so that our visualizations reflect accurately recorded penguins. We can simply drop all rows that contain **N/A** values using the **.dropna()** function. 


```python
print("Total number of rows before dropping: " + str(len(penguins)))

penguins = penguins.dropna()

print("Total number of rows after dropping: " +  str(len(penguins)))
```

    Total number of rows before dropping: 343
    Total number of rows after dropping: 324


We will now begin to create visualizations of the data using **Seaborn**. We will first import the **Seaborn** package.


```python
import seaborn as sns
```

# Summary Statistic Plots

For the visualization phase, we will start by providing summary statistic plots using our imported **Seaborn** package in order to get a sense of how some of the columns are distributed. 

For our first plot, we will create a boxplot with **Species** on the x-axis and **Culmen Depth** on the y-axis. To do so we will use the function **sns.boxplot()** and specify the x parameter (x-axis) as **Species** and the y parameter (y-axis) as **Culmen Depth**. Additionally, we will also look at the distribution of **Culmen Depth** for each **Species** by **Sex**. In order to do so, we simply set the hue parameter equal to the **Sex** column. 


```python
plot1 = sns.boxplot(x = penguins["Species"], y = penguins["Culmen Depth (mm)"], hue = penguins["Sex"]);
plot1.set(title = "Plot 1: Boxplot of Species vs Culmen Depth by Sex");
```


    
![png](output_18_0.png)
    


**Plot 1 Summary**: This boxplot shows us the distribution of the **Culmen Depth** for each **Species** by **Sex**. When looking at any particular box, the very bottom line represents the minimum, the botttom line of the box represents the 25th percentile, the middle line represents the median, the top line of the box represents the 75th percentile, and finally the very top line represents the maximum. We observe in this plot that the Gentoo penguins seem to have the smallest **Culmen Depth** on average compared to the Chinstrap and Adelie penguins. The Adelie and Chinstrap share pretty similar characteristics in terms of **Culmen Depth** and we also notice that in general males have a larger **Culmen Depth** than females.

For our second plot, we will create a line graph with **Species** on the x-axis and **Culmen Length** on the y-axis. To do so we will use the function **sns.lineplot()** and specify the x parameter as **Species** and the y parameter as **Culmen Length**. Additionally, we will also look at the distribution of **Culmen Length** for each **Species** by **Sex**. In order to do so, we simply set the hue parameter equal to the **Sex** column. If you look at the graph below you will notice shading around each respective line. This represents the mean and 95% confidence interval.


```python
plot2 = sns.lineplot(x = penguins["Species"], y = penguins["Culmen Length (mm)"], hue = penguins["Sex"]);
plot2.set(title = "Plot 2: Line Graph of Species vs Culmen Length by Sex");
```


    
![png](output_21_0.png)
    


**Plot 2 Summary**: From this graph we observe different characterisitcs compared to **Plot 1**. Despite the Gentoo having the smallest **Culmen Depth** on average, they appear to have the the second highest **Culmen Length** on average. Similarly the Adelie has swapped rankings from the previous plot going from the largest **Culmen Depth** to the smallest **Culmen Length**. The Chinstrap meanwhile has maintained its dominance in both categories. Lastly, the male penguins have a larger **Culmen Length** on average compared to their female counterparts. 

For our third plot, we will create a histogram with **Body Mass** on the x-axis and the penguin count for each **Body Mass** interval on the y-axis. To do so we will use the function **sns.histplot()** and specify the x parameter (x-axis) as **Body Mass**. Additionally, we will also look at the distribution of **Body Mass** for each **Species**. In order to do so, we simply set the hue parameter equal to the **Species** column. Also, in order to create a visually appealing figure, we will set the multiple parameter equal to "stack" which simply changes the style of the histogram.


```python
plot3 = sns.histplot(x = penguins["Body Mass (g)"], hue = penguins["Species"], multiple = "stack");
plot3.set(title = "Plot 3: Histogram of Body Mass by Species");
```


    
![png](output_24_0.png)
    


**Plot 3 Summary**: We are now looking at a histogram with **Body Mass** on the x-axis and the number of penguin **Species** within a particular interval of **Body Mass** on the y-axis. From the graph, we see that the Gentoo seem to be the heaviest of the 3 **Species** as their distribution is centered to the right on the x-axis. On the other hand the Chinstrap seems to be the lightest as their distribution is centered to the left on the x-axis, leaving the Adelie penguins as the **Species** with a median **Body Mass**. 

For our fourth plot, we will create another boxplot with **Species** on the x-axis and **Flipper Length** on the y-axis. To do so we will once again use the function **sns.boxplot()** and specify the x parameter (x-axis) as **Species** and the y parameter (y-axis) as **Flipper Length**. Additionally, we will also look at the distribution of **Flipper Length** for each **Species** by **Sex**. In order to do so, we simply set the hue parameter equal to the **Sex** column. 


```python
plot4 = sns.boxplot(x = penguins["Species"], y = penguins["Flipper Length (mm)"], hue = penguins["Sex"]);
plot4.set(title = "Plot 4: Boxplot of Species vs Flipper Length by Sex");
```


    
![png](output_27_0.png)
    


**Plot 4 Summary**: In this plot we will once again be looking at a boxplot this time analyzing the **Flipper Length** instead of the **Culmen Depth**. This graph seems like a flipped version of the first boxplot we looked at in **Plot 1**. The Gentoo noticeably have the largest **Flipper Length** whle the Chinstrap and Adelie are close with a slight advantage to the Chinstrap. In addition we notice that the **Flipper Length** for the males are larger than the females however by a much smaller amount compared to the other plots. 

# More Penguin Plots

Next, we will provide more penguin plots that look at relationships between different columns. We will continue using the **Seaborn** package to create scatterplots and histograms.

We will create a plot that analyzes the distribution of **Body Mass** by **Island**. To create this plot we will use the **sns.displot()** function with the x parameter (x-axis) as **Body Mass** and the y-axis (which we will not specify in the function) will be the number of penguin **Species** within a particular interval of **Body Mass**. We will also set the element parameter equal to step for stylistic purposes. To look at the distribution of **Body Mass** for each **Island**, we simply set the hue parameter equal to the **Island** column.


```python
plot5 = sns.displot(penguins, x = penguins["Body Mass (g)"], hue = penguins["Island"], element = "step")
plot5.set(title = " Plot 5: Distribution of Body Mass by Island");
```


    
![png](output_32_0.png)
    


**Plot 5 Summary**: In this plot we observe the distribution of penguin **Body Mass** by **Island**. Comparing this plot to **Plot 3**, we can get a sense of what **Species** of penguins live on what respective **Island**. For instance in **Plot 3** we found the Gentoo to be distributed towards the right of the x-axis, so looking at this plot we might infer that most of Biscoe Island is inhabited by Gentoo penguins. Following the same strategy we can say that Chinstraps are from Torgerson Island, and Adelies are from Dream Island. 

In this next plot we will take a look at the comparison between **Culmen Length** (x-axis) and **Culmen Depth** (y-axis) with a subplot for each **Species** by **Sex**. In order to create subplots using **Seaborn** we will use the **sns.FacetGrid()** function which is a multi-plot grid for plotting conditional relationships. In our first parameter we pass in the data set, in the second parameter we specify which column we want our conditional relationship to be based on (ie **Species**), in the third parameter we provide an additional condition that allows us to look at comparisons between **Sex**, and finally the height parameter is for adjusting the size of the figure. Next in order to tell Python what we want to plot on each of these subplots, we call the **.map()** function. We will be plotting scatterplots, so for our first parameter we call **sns.scatterplot** and then our second and third parameters represent the x and y axis variables respectively. In the last three lines of the following code block, we show how to add a legend/title and adjust the header title. 


```python
plot6 = sns.FacetGrid(penguins, col = "Species", hue = "Sex", height = 5);
plot6.map(sns.scatterplot, "Culmen Length (mm)", "Culmen Depth (mm)");
plot6.add_legend();
plot6.fig.subplots_adjust(top = 0.85) 
plot6.fig.suptitle("Plot 6: Culmen Length vs Culmen Depth For Each Species by Sex");
```


    
![png](output_35_0.png)
    


**Plot 6 Summary**: In general, we observe that the relationship between **Culmen Length** and **Culmen Depth** appears to be positively correlated (ie an increase in **Culmen Length** usually means an increase in **Culmen Depth**). This property is apparent for the Chinstrap and Gentoo peguins as well as for each respective **Sex** in these **Species**. For the Adelie penguins specifically we notice that this relationship is less apparent for both the males and females but is still somewhat noticeable. 

In our penultimate plot, we will take a look at two columns of the penguins data set we have not yet explored: **Delta 15 N** and **Delta 13 C**. We will use the **sns.scatterplot()** function to create a scatterplot with **Delta 15 N** on the x-axis and **Delta 13 C** on the y-axis. Similar to previous plots, we will also condition by **Species** which we can specify in the hue parameter of our scatterplot function. 


```python
plot7 = sns.scatterplot(x = penguins["Delta 15 N (o/oo)"], y = penguins["Delta 13 C (o/oo)"], hue = penguins["Species"]);
plot7.set_title("Plot 7: Delta 15 N vs Delta 13 C by Species");
```


    
![png](output_38_0.png)
    


**Plot 7 Summary**: Looking at each **Species** separately, we notice that the relationship between the **Delta 15 N** and **Delta 13 C** appears negatively correlated for the Gentoo and Chinstrap (an increase in **Delta 15 N** leads to a decrease in **Delta 13 C**). On the other hand, for the Adelie penguins the two delta variables do not appear to have a definitive relationship but appear to have a weak positive correlation (increase in **Delta 15 N** generally leads to an increase in **Delta 13 C**.

In our last plot, we will once again use the **sns.FacetGrid()** function to explore the relationship between **Flipper Length** (x-axis) and **Body Mass** (y-axis). We will proceed in the same way as **Plot 6** to create this visualization, just changing the second and third parameters in the **.map()** function to **Flipper Length** and **Body Mass** respectively.  


```python
plot6 = sns.FacetGrid(penguins, col = "Species", hue = "Sex", height = 5);
plot6.map(sns.scatterplot, "Flipper Length (mm)", "Body Mass (g)");
plot6.add_legend();
plot6.fig.subplots_adjust(top = 0.85) 
plot6.fig.suptitle("Plot 8: Flipper Length vs Body Mass for each Species by Sex");
```


    
![png](output_41_0.png)
    


**Plot 8 Summary**: For the Chinstrap and Gentoo penguins, there appears to be a positive correlation between the **Flipper Length** and **Body Mass** (an increase in **Flipper Length** leads to an increase in **Body Mass**). This applies for both males and females. For the Adelie penguins there also appears to be a positive correlation however the relationship is much weaker compared to the other **Species**. 

# Conclusion

Thank you for joining me on this tutorial about Palmer Penguins! I hope you were able to learn about the Adelie, Gentoo, and Chinstrap penguins and their characterisitcs through these visualizations. 


```python

```
