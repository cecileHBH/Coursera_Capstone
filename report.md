# Predicting the severity of a car accident


## Introduction

The number of annual road traffic deaths has reached 1.35 million worldwide[^1]. Road traffic injuries are the first cause of death of people aged 5-29 years. Every 24 seconds someone dies on the road. Those numbers are astonishingly high but there is another cost of these accidents : the medical costs for the survivors. Injured people often need medical care wheareas for short or long term injuries. The economic consequences of motor vehicle crashes have been estimated between 1% and 3% of the respective GNP of the world countries, reaching a total over $500 billion [^2]

This project aims to determine if we can predict the severity of a car accident using features as date, time, location, weather conditions and road conditions.

### Interests

If such a prediction is possible, we may be able to find a correlation between the severity and a specific feature which could lead to improve the roads safety. Addressing this problem the right way, whereas it is prevention messages, adding traffic signage or redesigning roads would mean less road traffic injuries and less money spent on medical care. For a government or local authority taking care of the medical bill, it means they could spend this budget for other purposes.

## Data

### Data source

The dataset used is the US Accidents (3.5 million records)[^3] dataset from Kaggle.

### Description

This dataset contains accident data covering 49 states of the USA. It has been collected from February 2016 and June 2020 using multiple Traffic APIs. It contains features as start and end time, location, weather conditions and road conditions

### Exploring dataset

On the 49 existing columns, we will use only 28 of them : 
* 'Severity' : Shows the severity of the accident, a number between 1 and 4, where 1 indicates the least impact on traffic (i.e., short delay as a result of the accident) and 4 indicates a significant impact on traffic (i.e., long delay).
* 'Start_Time', Shows start time of the accident in local time zone.
* 'End_Time' : Shows end time of the accident in local time zone. End time here refers to when the impact of accident on traffic flow was dismissed.
* 'Start_Lat' : Shows latitude in GPS coordinate of the start point.
* 'Start_Lng' : Shows longitude in GPS coordinate of the start point.
* 'Description' : Shows natural language description of the accident.
* 'Temperature(F)' : Shows the temperature (in Fahrenheit)
* 'Wind_Chill(F)' : Shows the wind chill (in Fahrenheit).
* 'Humidity(%)' : Shows the humidity (in percentage).
* 'Pressure(in)' : Shows the air pressure (in inches).
* 'Visibility(mi)' : Shows visibility (in miles).
* 'Wind_Direction' : Shows wind direction.
* 'Wind_Speed(mph)' : Shows wind speed (in miles per hour).
* 'Precipitation(in)' : Shows precipitation amount in inches, if there is any.
* 'Weather_Condition' : Shows the weather condition (rain, snow, thunderstorm, fog, etc.)
* 'Amenity' : A [POI](https://wiki.openstreetmap.org/wiki/Points_of_interest) annotation which indicates presence of [amenity](https://wiki.openstreetmap.org/wiki/Key:amenity) in a nearby location.
* 'Bump' : A POI annotation which indicates presence of speed bump or hump in a nearby location.
* 'Crossing' : A POI annotation which indicates presence of [crossing](https://wiki.openstreetmap.org/wiki/Key:crossing) in a nearby location.
* 'Give_Way' : A POI annotation which indicates presence of [give_way](https://wiki.openstreetmap.org/wiki/Tag:highway%3Dgive_way) in a nearby location.
* 'Junction' : A POI annotation which indicates presence of [junction](https://wiki.openstreetmap.org/wiki/Key:junction) in a nearby location.
* 'No_Exit' : A POI annotation which indicates presence of [no_exit](https://wiki.openstreetmap.org/wiki/Key:noexit) in a nearby location.
* 'Railway' : A POI annotation which indicates presence of [railway](https://wiki.openstreetmap.org/wiki/Key:railway) in a nearby location.
* 'Roundabout' : A POI annotation which indicates presence of [roundabout](https://wiki.openstreetmap.org/wiki/Tag:junction%3Droundabout) in a nearby location. 
* 'Station' : A POI annotation which indicates presence of [station](https://wiki.openstreetmap.org/wiki/Key:station) in a nearby location.
* 'Stop' : A POI annotation which indicates presence of [stop](https://wiki.openstreetmap.org/wiki/Key:stop) in a nearby location.
* 'Traffic_Calming' : A POI annotation which indicates presence of [traffic_calming](https://wiki.openstreetmap.org/wiki/Key:traffic_calming) in a nearby location.
* 'Traffic_Signal' : A POI annotation which indicates presence of [traffic_signal](https://wiki.openstreetmap.org/wiki/Tag:highway%3Dtraffic_signals) in a nearby location.
* 'Turning_Loop' : A POI annotation which indicates presence of [turning_loop](https://wiki.openstreetmap.org/wiki/Tag:highway%3Dturning_loop) in a nearby location.

As we want to predict the severity, we check if the dataset is balanced for this feature
<img src="https://user-images.githubusercontent.com/1349413/97021232-ddf11d00-1552-11eb-891d-82a1e1d0d9cd.png" alt="" width="400"/>
It appears the dataset is unbalanced concerning the severity.

### smote ?

## Finding correlation
## Results
## Discussion
## Conclusion

###### References
[^1]World Health Organization (WHO) - Global Status Report on Road Safety 2018 : https://www.who.int/violence_injury_prevention/road_safety_status/2018/en/external

[^2]World Health Organization (WHO) - Global Plan for the Decade of Action for Road Safety 2011-2020 : https://www.who.int/roadsafety/decade_of_action/plan/plan_english.pdf?ua=1

[^3] Moosavi, Sobhan, Mohammad Hossein Samavatian, Srinivasan Parthasarathy, and Rajiv Ramnath. “A Countrywide Traffic Accident Dataset.”, 2019.
Moosavi, Sobhan, Mohammad Hossein Samavatian, Srinivasan Parthasarathy, Radu Teodorescu, and Rajiv Ramnath. "Accident Risk Prediction based on Heterogeneous Sparse Data: New Dataset and Insights." In proceedings of the 27th ACM SIGSPATIAL International Conference on Advances in Geographic Information Systems, ACM, 2019.
