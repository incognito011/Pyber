
# Pyber Ride Sharing




## Analysis

#### Observed Trend 1 
There is an inverse crrelation between the population size and the fare price. The less populated the area, the higher the fare price. 

#### Observed Trend 2
There is a direct correlation between city population size and the number of drivers. Urban areas have more drivers than suburban and rural areas.

#### Observed Trend 3
Ride sharing is most prevelant and cost-effective in urban areas, where the supply of drivers and riders is the highest.




```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
```


```python

# takes in all of the ride sharing data and reads it into pandas
city_data = "Resources/city_data.csv"
ride_data = "Resources/ride_data.csv"

# creates city data and ride data dataframes
city_data_df = pd.read_csv(city_data)
ride_data_df = pd.read_csv(ride_data)


ride_data_df.head(5)
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
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Lake Jonathanshire</td>
      <td>2018-01-14 10:14:22</td>
      <td>13.83</td>
      <td>5739410935873</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Michelleport</td>
      <td>2018-03-04 18:24:09</td>
      <td>30.24</td>
      <td>2343912425577</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Port Samanthamouth</td>
      <td>2018-02-24 04:29:00</td>
      <td>33.44</td>
      <td>2005065760003</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Rodneyfort</td>
      <td>2018-02-10 23:22:03</td>
      <td>23.44</td>
      <td>5149245426178</td>
    </tr>
    <tr>
      <th>4</th>
      <td>South Jack</td>
      <td>2018-03-06 04:28:35</td>
      <td>34.58</td>
      <td>3908451377344</td>
    </tr>
  </tbody>
</table>
</div>




```python
# merges the first two datasets on "city" so that no data is lost 

combined_data_df = pd.merge(ride_data_df, city_data_df, how='outer', on='city')
combined_data_df.head(5)
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
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Lake Jonathanshire</td>
      <td>2018-01-14 10:14:22</td>
      <td>13.83</td>
      <td>5739410935873</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Lake Jonathanshire</td>
      <td>2018-04-07 20:51:11</td>
      <td>31.25</td>
      <td>4441251834598</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Lake Jonathanshire</td>
      <td>2018-03-09 23:45:55</td>
      <td>19.89</td>
      <td>2389495660448</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Lake Jonathanshire</td>
      <td>2018-04-07 18:09:21</td>
      <td>24.28</td>
      <td>7796805191168</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Lake Jonathanshire</td>
      <td>2018-01-02 14:14:50</td>
      <td>13.89</td>
      <td>424254840012</td>
      <td>5</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>



# Bubble Plot of Ride Sharing Data


```python
# groups data by city
group_data = combined_data_df.groupby(['city'])
group_data.count().head(5)
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
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Amandaburgh</th>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
    </tr>
    <tr>
      <th>Barajasview</th>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Barronchester</th>
      <td>16</td>
      <td>16</td>
      <td>16</td>
      <td>16</td>
      <td>16</td>
    </tr>
    <tr>
      <th>Bethanyland</th>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
      <td>18</td>
    </tr>
    <tr>
      <th>Bradshawfurt</th>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>




```python

# finds average fare
average_fare = group_data.mean()['fare']

# finds total number of rides
ride_total = group_data['ride_id'].count()

# finds driver count
driver_count = group_data.mean()['driver_count']

# city type data
city_type = city_data_df.set_index('city')['type']

# creates new dataframe for scatter plot data
city_results = pd.DataFrame({
    "Average Fare": average_fare,
    "Total Number of Rides": ride_total,
    "Total Number of Drivers": driver_count,
    "City Type": city_type
})


city_results.head(5)
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
      <th>Average Fare</th>
      <th>City Type</th>
      <th>Total Number of Drivers</th>
      <th>Total Number of Rides</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Amandaburgh</th>
      <td>24.641667</td>
      <td>Urban</td>
      <td>12.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>Barajasview</th>
      <td>25.332273</td>
      <td>Urban</td>
      <td>26.0</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Barronchester</th>
      <td>36.422500</td>
      <td>Suburban</td>
      <td>11.0</td>
      <td>16</td>
    </tr>
    <tr>
      <th>Bethanyland</th>
      <td>32.956111</td>
      <td>Suburban</td>
      <td>22.0</td>
      <td>18</td>
    </tr>
    <tr>
      <th>Bradshawfurt</th>
      <td>40.064000</td>
      <td>Rural</td>
      <td>7.0</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>




```python
# splits up data into groups based on City Type

# urban
urban = city_results.loc[city_results["City Type"] == "Urban"]

# suburban
suburban = city_results.loc[city_results["City Type"] == "Suburban"]

# rural
rural = city_results.loc[city_results["City Type"] == "Rural"]


```


```python
# creates scatter plot for each city type

# urban
plt.scatter(urban["Total Number of Rides"], urban["Average Fare"], marker="o", facecolor = "lightcoral", edgecolors="black", s = urban["Total Number of Drivers"]*10, label = "Urban", alpha = 0.75, linewidth = 1)

# suburban
plt.scatter(suburban["Total Number of Rides"], suburban["Average Fare"], marker="o", facecolor = "lightskyblue", edgecolors ="black", s = suburban["Total Number of Drivers"]*10, label = "Suburban", alpha = 0.75, linewidth = 1)

# rural
plt.scatter(rural["Total Number of Rides"], rural["Average Fare"], marker="o", facecolor = "gold", edgecolors = "black", s = rural["Total Number of Drivers"]*10, label = "Rural", alpha = 0.75, linewidth = 1)


# adds title, x axis label and y axis label
plt.title("Pyber Ride Sharing Data (2018)")
plt.xlabel("Total Number of Rides (per City)")
plt.ylabel("Average Fare ($)")

# adds note
plt.text(45, 30,"Note: \nCircle size correlates with driver count per city")


# adds legend
plt.legend(loc=1,  markerscale = 0.5 , title='City Types')

# displays grid
plt.grid(True)

# Saves an image of the scatter chart and prints the final product to the screen
plt.savefig("Images/Pyber_Pie.png")

plt.show()
```


![pyber_pie](https://user-images.githubusercontent.com/37307811/41499675-f6d7b83a-7151-11e8-9aa2-abb5b29b5fbd.png)


# Total Fares by City Type


```python
# finds total fares by city type

pie_fare = combined_data_df.groupby(["type"])["fare"].sum()
pie_fare
```




    type
    Rural        4327.93
    Suburban    19356.33
    Urban       39854.38
    Name: fare, dtype: float64




```python
# sets labels, colors and explode for all pie charts
pies = ["Rural", "Suburban", "Urban"]
colors = ["gold","lightskyblue","lightcoral"]
explode = (0,0,0.1)
```


```python

# tells matplotlib to create a pie chart based upon the above data
plt.pie(pie_fare, explode=explode, labels=pies, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)

# Creates axes which are equal so the pie chart is a perfect circle
plt.axis("equal")

plt.title("% of Total Fares by City Type")

# Saves an image of the chart and prints the final product to the screen
plt.savefig("Images/Fares_Pie.png")

plt.show()
```


![fares_pie](https://user-images.githubusercontent.com/37307811/41499674-f6b66f0e-7151-11e8-89b1-e45f7f04bef3.png)


# Total Rides by City Type


```python
# finds riders by city type

pie_riders =  city_results.groupby(["City Type"])["Total Number of Rides"].sum()
pie_riders
```




    City Type
    Rural        125
    Suburban     625
    Urban       1625
    Name: Total Number of Rides, dtype: int64




```python
# tells matplotlib to create a pie chart based upon the above data
plt.pie(pie_riders, explode=explode, labels=pies, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)

# Creates axes which are equal so the pie chart is a perfect circle
plt.axis("equal")

plt.title("% of Total Rides by City Type")

# Saves an image of the chart and prints the final product to the screen
plt.savefig("Images/Rides_Pie.png")

plt.show()
```


![rides_pie](https://user-images.githubusercontent.com/37307811/41499676-f6e2239c-7151-11e8-80a7-f8b089bf0fd4.png)


# Total Drivers by City Type


```python
# finds total drivers by city type

pie_drivers = city_results.groupby(["City Type"])["Total Number of Drivers"].sum()
pie_drivers
```




    City Type
    Rural         78.0
    Suburban     490.0
    Urban       2405.0
    Name: Total Number of Drivers, dtype: float64




```python
# tell matplotlib to create a pie chart based upon the above data
plt.pie(pie_drivers, explode=explode, labels=pies, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=140)

# Creates axes which are equal so the pie chart is a perfect circle
plt.axis("equal")

plt.title("% of Total Drivers by City Type")

#Saves an image of our chart and prints the final product to the screen
plt.savefig("Images/Drivers_Pie.png")

plt.show()
```


![drivers_pie](https://user-images.githubusercontent.com/37307811/41499671-ee9474d8-7151-11e8-8afc-4a7f6bdd1ed4.png)

