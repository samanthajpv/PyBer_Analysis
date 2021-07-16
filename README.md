# PyBer Analysis

## Project Overview

PyBer is a ride-sharing app seeking to enhance its services. The company is focusing on improving their access to users and be able to determine a cost-effective stategy for underserved areas. The rideshare data analyzed was from January to May of 2019. Using Python, together with Pandas and Matplotlib libraries, the goal of the project was to create a summary dataframe and a visualization that would help the company in driving business decisions.

### Purpose

The purpose of the project was to perform an exploratory analysis on the rideshare data. This includes creation of a Pandas summary DataFrame by type of city, and a multiple-line chart displaying the sum of weekly fares for each city type through utilizing Matplotlib. The findings were then evaluated to see how it can be beneficial to PyBer.

### Resources
- Data:
    - [City Data](https://github.com/samanthajpv/PyBer_Analysis/blob/26b8b75ec200e8587997d9e5d858d175cddd03aa/Resources/city_data.csv) - contains city, driver count, and type of city
    - [Ride Data](https://github.com/samanthajpv/PyBer_Analysis/blob/26b8b75ec200e8587997d9e5d858d175cddd03aa/Resources/ride_data.csv) - contains city, date, fare, and ride ID
- Software: Jupyter Notebook 6.3.0
- Language: Python 3.8.8
    - Libraries: Pandas 1.2.4, Matplotlib 3.3.4
- Refer to [PyBer_Challenge.ipynb](https://github.com/samanthajpv/PyBer_Analysis/blob/26b8b75ec200e8587997d9e5d858d175cddd03aa/PyBer_Challenge.ipynb) for the code

## Results

### Summary DataFrame by City Type

<p align="center">
    <img src="https://github.com/samanthajpv/PyBer_Analysis/blob/48e38d6ba89ed7469477b1ce6e3e924b7f016b60/Analysis/PyBer_summary_df.png" width="700" height="140">
</p>

The summary was created by using the ```groupby()``` function on the type of city, followed by an aggregate function on the selected column (```count()``` for the number of rides and ```sum()``` for the number of drivers and total fares). The analysis showed three city types, namely rural, suburban, and urban. Below are the findings:

- **Total Rides**
    -  The number of rides in urban areas is 68.4% of the total rides. That is 2.6 times the number of rides in suburban areas and 13 times the number of rides in rural areas. 
    - In addition, suburban rides are 5 times greater than the rides in rural areas.
- **Total Drivers**
    - There are 4.9 times more drivers in the urban areas compared to the suburban areas. This equates to 30.8 times more than the number of drivers in rural areas and 80.9% of the total number of drivers.
    - On the other hand, rural area drivers are 6.3 times less than the suburban area drivers.
- **Total Fares**
    - The sum of the fares in urban areas are 2.1 times more than the total fares in suburban areas and 9.2 times more than in the rural areas. The fares from urban areas constitutes 62.7% of the total fares.
    - Moreover, the sum of fares from suburban areas are 4.5 times greater than the total fares in rural areas.
- **Average Fare per Ride**
    - The average fare per ride in urban areas is $10.09 less than in rural areas and $6.44 less in suburban areas. There is a 26-41% increase in fare per ride from the average urban ride rate.
    - There is a $3.65 increase in average fare per ride from suburban to rural areas, or a 12% difference.
- **Average Fare per Driver**
    - The average fare per driver in rural areas is 3.3 times that of the average fare per driver in urban areas, and 1.4 times greater than in the suburban areas.
    - The average fare per driver in suburban areas is 2.4 times more than in urban areas.

### Total Fare by City Type

From the DataFrame, the sum of fares were grouped by the city type and date. The index was reset for the creation of the pivot table as shown in the code below:

```
# Reset index
fares_per_date = fares_per_date.reset_index()

# Pivot table with 'date' as the index, city 'type' for columns, and 'fare' for the values, to get the total fares for each type of city by date
fares_per_date_pivot = fares_per_date.pivot(index="date", columns="type", values="fare")
```
For the multiple-line chart, only the data from January 1 to April 29 was selected using the ```loc()``` method. The index was then converted to a datetime datatype in order to apply the ```resample()``` function as seen below to group the fares by week:

```
# Create a new DataFrame from the pivot table DataFrame using loc on the given dates, '2019-01-01':'2019-04-29'.
fares_date_type = fares_per_date_pivot.loc['2019-01-01':'2019-04-29']

# Create a new DataFrame using the "resample()" function by week 'W' and get the sum of the fares for each week.
fares_date_type_per_month = fares_date_type.resample("W").sum()
```
<p align="center">
    <img src="https://github.com/samanthajpv/PyBer_Analysis/blob/48e38d6ba89ed7469477b1ce6e3e924b7f016b60/Analysis/PyBer_fare_summary.png" width="730" height="250">
</p>

Total weekly fare for rides in urban areas range from greater than $1500 - $2500, greater than $500 - $1500 for rides in suburban areas, and below $500 for rides in rural areas. The graph appears to be moving in a straight line for all city types. Given that urban cities are densely populated, the urban line graph sits at the top of the chart, followed by suburban, and rural at the bottom. Although there are peaks towards the end of March and a dip in the first week of April for suburban, the graph does not display any erratic movement. The graph for each city type shows that they are moving within their own ranges and not coinciding with one another. 

## Summary
The analysis showed that from rural to suburban and suburban to urban, total rides, drivers, and fares increase while the average fare per ride and driver decrease. Below are business recommendations that PyBer might want to look into in order to address the disparities among the city types:

- **Conduct a market study** - It is important for a company to define who their target market is, how the service is currently received by potential users, and how they can improve their services based on the customers' priorities. It will be beneficial to know what influences users to use a ride-sharing app, what are the types of effective advertising, and knowing how to attract and retain customers. *(More on [market research](https://www.investopedia.com/terms/m/market-research.asp))*
- **Compare profitability routes** - The analysis above did not mention how the fares were calculated. The company might want to consider researching and comparing the profitability between mileage of trips and number of rides. With this, the company may or may not consider focusing on enhancing their services in just one or in all city types depending on the demand. They will also be able to evaluate if they have enough, an abundance, or a shortage of drivers.
- **Research on industry players** - It is essential to know who your competitors are, how they are performing, and being aware of what they are doing to keep up with the everchanging market demands. Benchmarking is an example of how the company can gauge their success against their competitors and use it as a way to continuously improve their performance. *(More on [benchmarking](https://www.thebalancecareers.com/overview-and-examples-of-benchmarking-in-business-2275114))*

## Reference

(1) Trilogy Education Services. (2021, July). *Module 5 Challenge*. https://courses.bootcampspot.com/courses/626/assignments/13386?module_item_id=212505

#### Other Useful Articles

###### (1) *Place Legend Outside the Plot in Matplotlib*. (2020, Dec. 13). DelftStack. Retrieved on July 14, 2021 from https://www.delftstack.com/howto/matplotlib/how-to-place-legend-outside-of-the-plot-in-matplotlib/
###### (2) Twin, A. (2020, Sept. 28). *Market Research. Investopedia*. https://www.investopedia.com/terms/m/market-research.asp
###### (3) Reh, J.F. (2019, July 26). *The Importance of Benchmarking in Improving Business Operations*. TheBalanceCareers. https://www.thebalancecareers.com/overview-and-examples-of-benchmarking-in-business-2275114
