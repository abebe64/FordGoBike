# Project: Data Analysis of Ford GoBike Dataset
### By: Abebe Tarekegne
### Published: on May 5, 2019


## Exploration of Dataset

> I am interested to add on my learning experiance of using some spatial data analysis which I thought Ford GoBike's trip Dataset will be the best fit. I used the link which was provided from Udacity and also available for public use [here](https://www.fordgobike.com/system-data). I downloaded programatically all mix of those data sorces in *.csv and *.zip formats. 


### What is the structure of the dataset?
>The dataset gathered are from July 2017 to March 2019. It consists of 3015214 trip record with 16 features.

>`The features included in the source dataset:`

| `Feature Name`          | `Data Type` | `Unique Count` | `NaN Count` |
|-------------------------|-----------|--------------|-----------|
| duration_sec            | int64     | 22152        | 0         |
| start_time              | object    | 3015020      | 0         |
| end_time                | object    | 3015038      | 0         |
| start_station_id        | float64   | 360          | 12437     |
| start_station_name      | object    | 381          | 12437     |
| start_station_latitude  | float64   | 407          | 0         |
| start_station_longitude | float64   | 408          | 0         |
| end_station_id          | float64   | 360          | 12437     |
| end_station_name        | object    | 381          | 12437     |
| end_station_latitude    | float64   | 408          | 0         |
| end_station_longitude   | float64   | 410          | 0         |
| bike_id                 | int64     | 6802         | 0         |
| user_type               | object    | 2            | 0         |
| member_birth_year       | float64   | 92           | 206967    |
| member_gender           | object    | 3            | 206534    |
| bike_share_for_all_trip | object    | 2            | 519700    |

### What are the main feature(s) of interest in the dataset?
>I am most interested in the `duration_sec` but as the start and end oordinates are provided it will be more interesting to find the distance or the average speed of each trip so new features are added. It is also interesting to investigate the trip duration relationship with User Type (Subscriber or Customer – “Subscriber” = Member or “Customer” = Casual), Member Year of Birth and Member Gender.

### What type of new features are introduced?

>Since trip start and end locations are provided I am interested to find the minimum possible distance traveled by riders. We use geopy module for spatial data manuplation, it can calculate geodesic distance between two points. With time and distance then we calculated the average speed, so new feature called `minimum_distance_miles` and `average_speed_mph`.

>Based on latitue and longitude filtering we create new feature called `city` and group as `San Francisco`,`Oakland`,`San Jose` and `Others`.

>We created new feature called `member_age_group` which shows grouping based on the member age range. From `member_birth_year` we use 2019 as reference to find the `member_age`, and then we use bining to divide in groups of meaningful size for visualization.

#### What the statistics tells us from features we investigated?

>Average trip ride duration is 12.35 minutes and ride distance is 1 mile.
75% of the rides took less than 15 minutes and travel less than 1.4 miles.
99% of the rides took less than 102 minutes and travel less than 3.1 miles.

>Subscriber or member riders are 84.7 % while casual custemer are 15.3 %.
Male riders are 69.3 % while Female riders are 22.6 %.
Bike Share for all trips are only 7.3% while the rest are 75.6%
>San Francisco, Oakland, San Jose riders are 74.4%, 20.7%, and 4.8% respectively

>The largest number of riders 67.2% are in the age range of 20 to 40 years old.
San Francisco members age from 30 to 40 are the largest number of riders of all age group. Thursday is the busiest day of all weekdays, Tuesday is the second busiest.

>We observed that there are period where number of bikes in use decrease from 3.3K peak in March 2018 down to 2.8k, End of year 2018. And then increased at the high rate towards end of March 2019 with 6.8K unique bikes.

## Explanatory Data Visualization

#### What is the `average speed` of trip by specific area and user type?

>Oakland riders seems have a little bit faster than San Francisco riders. Interestingly San Jose riders are the slowest of all. For Other riders, areas away from city, they are faster than those in city as expected. Subscribers tend to show higher average speed compare to customers.
![Bivariate_AvgSpeed_User_Type_by_city.png] (./plots/Bivariate_AvgSpeed_User_Type_by_city.png)

#### What is the most commen age group of riders?

>- Age Group 30-40 riders are 36.4 %
>- Age Group 20-30 riders are 30.8 %
>- Age Group 40-50 riders are 14.7 %
>- Age Group 50-60 riders are 7.8 %

>The largest number of riders 67.2% are in the age range of 20 to 40 years old.

#### What are the busiest hours of the stations?

>We see 8th and 17th hours are the busiest hours for each work week as expected, typical work hour start and end times. 2nd busiest are 9th and 18th hours, followed by 7th and 16th hours all around the work start and end periods.

![Bivariate_HourOftheDay_Weekday_Rides.png](attachment:Bivariate_HourOftheDay_Weekday_Rides.png)

>Tuesday seems the most used rides comparing from other days.

![Bike_Ride_Hourly_Trend_by_city.png](attachment:Bike_Ride_Hourly_Trend_by_city.png)

>As previously observed the steep rise and fall around peak hours 8th and 17th hours occures especially for San Francisco. Oakland follows the same pattern as San Francisco for 8th hour but with lower rate of change. For 17th hour its rate of decrease is slower until 18th hour.San Jose, we can assume more consistancy in the number of rides betwen 8th hours until 15th hours, then slowly rise at 17th hour. 

![Bivariate_HourOftheDay_Month_Rides.png](attachment:Bivariate_HourOftheDay_Month_Rides.png)

>March is the busiest and April is the slowest month of the year. For both San Francisco and Oakland area we show decrease of riders in the month of April while it is peak in the month of October. San Jose shows relatively consistent number of rides across all months of the year.

#### What are the subscriber average speed comparing to customers?

>It seems that the subscriber average speed is consistently higher than customers in all city. Worth nothing that San Jose is the slowest for Customer but a bit higher for Subscriber. Need to investigate why this difference assuming the traffic congesion will be the same for all riders.

### Historical Growth of the Number of Bike Riders by City

>From previous analysis we show busy hours are aligned with the commute hours and from the lineplot what we show is the big drops on the number of rides are around Thanksgiving, X-Max, and New Year. The rate of increase after new year in 2019 is considerably very high comparing with the increase after January 1 of 2018. This is mainly due to the high number of bikes brought in service, about 2000 just in the first two months of 2019.

![HistoricalMonthlyTrend_Riders_City.png](attachment:HistoricalMonthlyTrend_Riders_City.png)

>Note that San Francisco riders rate of increase is higher than other cities as shown from the lineplot. 

![HistoricalMonthlyTrend_Riders_User.png](attachment:HistoricalMonthlyTrend_Riders_User.png)

>Subsciber riders are increasingly at a higher rate than customer riders.   

### Stations Highlights

>The number of stations increased dramatically from low 50s to 250 before November of 2017. Then constantly adding for the remaining 2018 and 2019. The latest number of stations shows 361. With 6801 maximum number of bikes in service.

#### What are the top two busy hour stations? 

>The first Top station, start_station_id of 30, San Francisco Caltrain (Townsend St at 4th St) has served 71 riders at a peak `Busy Hour` which occur on March 26 of 2019 at 8A.M. Second Top station, start_station_id of 67, San Francisco Caltrain Station 2  (Townsend St at 4th St) , served 70 at a peak `Busy Hour` which occur on July 09 of 2018 at 8A.M.

#### What is the top two busy day stations?

>First Top station, start_station_id of 67, San Francisco Caltrain Station 2  (Townsend St at 4th St) , served 305 rides at a peak `Busy Day` which occur on March 18 of 2019. Second Top station, start_station_id of 58, Market St at 10th St , served 247 rides at a peak `Busy Day` which occur on March 13 of 2019.

#### What are the number of days station is in service

>First Top station, start_station_id of 15 at San Francisco Ferry Building (Harry Bridges Plaza), were in service for 642 days and it has an average of 97.8 rides. Second Top station, start_station_id of 67 is at  San Francisco Caltrain Station 2  (Townsend St at 4th St), were in service for 641 days and it has an average of 96.2 rides.

>We show in Google Map the Top 10 (red outer circle), top 25 (orange outer circle) and blue dot for Ford GoBike stations.

![Riders_map.png](attachment:Riders_map.png)

## Key Insights

> The analysis of the dataset helps to tell story Ford GoBike services how their services are effective and efficient. Understanding the historical growth of the number of bike rides of Ford GoBike network will help policy makers in order to facilitate for future growth of the infrastructure. And also helps to further study the benefit of environmental friendly nature of the service around the bay area in general.

> We show big gender gap as almost 68% of riders are men, this possibly indicate that there is a need for Ford GoBike to research possible cause of such gap. Is business dressess, high hill shoes etc. discourage women to use bike rides, or any other reason?

> Increase of Subscribers riders at higher rate than customer is a good indication that more awareness through adverizment or environment friendly group joining the club. Bike Share for All are available to Bay Area residents ages 18 and older who qualify as Low Income member, another reason for increase of subscribers.

> Identify the top busiest stations by number of riders hourly or daily. Such as we show staion_id of 30, San Francisco Caltrain (Townsend St at 4th St) has served 71 riders at a maximum Busy Hour which occur on March 26 of 2019 at 8A.M.
And knowing the peak number of riders and maximum duration of bike rides per station used to determine if expanding for another nearby location is needed. It also helps to understand the most effcient use of resource allocation based on area, as San Francisco is the most utilized compared to other cities it is worth focusing for more growth opportunities.

> Knowing the slowest periods as we show around Thanksgiving, X-Max, and New Year can be used to service bikes of high milages in addition to malfanction bikes. And Ford GoBike can prepare by introducing new bikes, new stations, etc. for the high demand periods immediately after new year as we show in 2019 was considerably very high comparing with the previous year especially in San Francisco area. Or re-focus on the potential growth opportunies in the city that has more demands.
