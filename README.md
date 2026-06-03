


**Apple Fitness Data Analysis**

#### Overview
This project involves an exploratory data analysis (EDA) of Apple Fitness data to understand activity patterns, including step count, distance covered, energy burned, walking speed, and walking efficiency over time. The analysis aims to visualize trends, identify correlations, and gain insights into daily fitness activities.

#### Data Source
The dataset used is `Apple-Fitness-Data.csv`, containing various fitness metrics recorded over a period.

#### Libraries Used
*   `pandas` for data manipulation and analysis.
*   `plotly.express` and `plotly.graph_objects` for interactive visualizations.

#### Key Analysis Steps and Insights

##### 1. Data Loading and Initial Inspection

The data was loaded into a pandas DataFrame, and an initial check for null values confirmed the dataset is clean.

```python
# Code for data loading and null check
import pandas as pd

data = pd.read_csv("/content/Apple-Fitness-Data.csv")
print("First 5 rows of the dataset:")
display(data.head())

print("\nNull values in each column:")
display(data.isnull().sum())
```

##### 2. Analyzing Trends Over Time

Visualizations were created to show trends for Step Count, Distance Covered, Energy Burned, and Walking Speed over time. These plots help in understanding daily activity fluctuations.

```python
# Code for visualizing Step Count Over Time
import plotly.express as px

fig1 = px.line(data, x="Time",
               y="Step Count",
               title="Step Count Over Time")
fig1.show()
```

```python
# Code for visualizing Distance Covered Over Time
fig2 = px.line(data, x="Time",
               y="Distance",
               title="Distance Covered Over Time")
fig2.show()
```

##### 3. Average Step Count Per Day

The average step count per day was calculated and visualized using a bar chart to identify daily activity levels.

```python
# Code for calculating and visualizing Average Step Count per Day
average_step_count_per_day = data.groupby("Date")["Step Count"].mean().reset_index()
fig5 = px.bar(average_step_count_per_day, x="Date",
              y="Step Count",
              title="Average Step Count per Day")
fig5.update_xaxes(type='category')
fig5.show()
```

##### 4. Walking Efficiency Analysis

A new metric, "Walking Efficiency" (Distance / Step Count), was calculated to understand how efficiently movement is converted into distance. This was also plotted over time.

```python
# Code for calculating and visualizing Walking Efficiency
data["Walking Efficiency"] = data["Distance"] / data["Step Count"]
fig6 = px.line(data, x="Time",
               y="Walking Efficiency",
               title="Walking Efficiency Over Time")
fig6.show()
```

##### 5. Analysis by Time Intervals

To understand variations in activity throughout the day, the 'Time' column was categorized into 'Morning', 'Afternoon', and 'Evening'. A scatter plot then visualized the relationship between 'Step Count' and 'Walking Speed' across these time intervals, with a trendline to show general correlation.

```python
# Code for creating time intervals and analyzing variations
time_intervals = pd.cut(pd.to_datetime(data["Time"]).dt.hour,
                        bins=[0, 12, 18, 24],
                        labels=["Morning", "Afternoon", "Evening"],
                        right=False)
data["Time Interval"] = time_intervals

fig7 = px.scatter(data, x="Step Count",
                  y="Walking Speed",
                  color="Time Interval",
                  title="Step Count and Walking Speed Variations by Time Interval",
                  trendline='ols')
fig7.show()
```

#### Conclusion

This analysis provides a comprehensive look into the user's fitness data, highlighting daily trends, average activity levels, and how efficiency and activity vary throughout different parts of the day. These insights can be valuable for understanding personal fitness habits and making informed decisions about activity scheduling.

