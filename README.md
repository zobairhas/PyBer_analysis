# PyBer Analysis

## Project Overview
The client has asked to summarize various ride-sharing data by city type. The client also wants a multiple-line graph that shows the total weekly fares per city type.

## Methodology
- Tools/Programs/Languages used:
    - Python 
    - Jupyter Notebook
    - Pandas library
    - Matplotlib library

- I used the Pandas library to merge the data from the provided CSVs into a single dataset. After that, I was able to generate a summary of the DataFrame.

```
pyber_data_df = pd.merge(ride_data_df, city_data_df, how="left", on=["city", "city"])
```

- After that, I used the ```groupby()``` function to calculate/set up multiple variables to get "Total Rides", "Total Drivers", "Total Fares", "Average Fare per Ride", and "Average Fare per Driver."
- Then, I combined all of those variables into a new DataFrame.

```
pyber_summary_df = pd.DataFrame({"Total Rides": total_rides,
                           "Total Drivers": total_drivers,
                           "Total Fares": total_fares,
                           "Average Fare per Ride": avg_fare_per_ride,
                           "Average Fare per Driver": avg_fare_per_driver})
```

- The new DataFrame displayed the following summary: 
<br><br>
**Pyber Summary DataFrame Output:**
![PyBer_Summary](https://user-images.githubusercontent.com/44425379/151722378-42d0d42b-656d-4c90-8e45-225c0b7c84bf.png)

- To construct the multiple-line chart, I create a new DataFrame using the ```groupby()``` function and filtering by two columns. 
- Then, I had to create a pivot table using the "date" column as the index to get total fares for each city type by date. 
- Once I got the pivot working, I created another new DataFrame using the ```resample()``` function to get the sum of the fares for each week.

```
total_fare_per_date_df = pyber_data_df.groupby(["type", "date"]).sum()[["fare"]]

total_fare_pivot_df = total_fare_per_date_df.pivot(index="date", columns="type", values="fare")

total_fare_resample_df = total_fare_pivot_df.resample("W").sum()
```
- Finally, I was able to create the multiple line chart using the object-oriented interface method. I formatted the chart to make it easier to read and saved the figure as a png. 
![PyBer_Linechart](https://user-images.githubusercontent.com/44425379/151722361-6e92d08e-0b76-41a3-bbbf-32bbcce5e7cf.png)

## PyBer Analysis Results
- Urban areas have the highest number of total rides, drivers, and fares. Although the average fare per ride and average fare per driver is significantly lower than the other two city types; however, Urban areas make up for it with a higher quantity of rides.
- Urban areas have 13x the number of rides compared to Rural areas and 2.6x the number of rides compared to Suburban areas.

**Pyber Summary DataFrame Output:**
![PyBer_Summary](https://user-images.githubusercontent.com/44425379/151722378-42d0d42b-656d-4c90-8e45-225c0b7c84bf.png)

## PyBer Summary Recommendations
- Following the 80/20 rule, it would make sense to continue optimizing efforts for Urban areas as they generate the most revenue.
- That doesn't mean that there aren't opportunities to improve revenues in Suburban or Rural areas. 
- The average fares per driver and average fares per ride are significantly higher in Rural areas. Perhaps lowering these costs could generate more total drivers and fares in Rural areas. 
- Suburban areas make quite a bit of revenue for the number of rides and drivers that those areas have. It's interesting to note that there are more rides than drivers. It might make sense to charge more in Suburban areas as the demand is high for rides. 
