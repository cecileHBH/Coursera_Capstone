# Predicting the severity of a car accident


## Introduction

The number of annual road traffic deaths has reached 1.35 million worldwide<sup>1</sup>. Road traffic injuries are the first cause of death of people aged 5-29 years. Every 24 seconds someone dies on the road. Those numbers are astonishingly high but there is another cost of these accidents : the medical costs for the survivors. Injured people often need medical care wheareas for short or long term injuries. The economic consequences of motor vehicle crashes have been estimated between 1% and 3% of the respective GNP of the world countries, reaching a total over $500 billion<sup>2</sup>

This project aims to determine if we can predict the severity of a car accident using features as date, time, location, weather conditions and road conditions.

### Interests

If such a prediction is possible, we may be able to find a correlation between the severity and a specific feature which could lead to improve the roads safety. Addressing this problem the right way, whereas it is prevention messages, adding traffic signage or redesigning roads would mean less road traffic injuries and less money spent on medical care. For a government or local authority taking care of the medical bill, it means they could spend this budget for other purposes.

## Data

### Data source

The dataset used is the US Accidents (3.5 million records)<sup>3</sup> dataset from Kaggle.

### Description

This dataset contains accident data covering 49 states of the USA. It has been collected from February 2016 and June 2020 using multiple Traffic APIs. It contains features as start and end time, location, weather conditions and road conditions

### Exploring the dataset

On the 49 existing columns, we will use only 23 of them : 
* 'Severity' : Shows the severity of the accident, a number between 1 and 4, where 1 indicates the least impact on traffic (i.e., short delay as a result of the accident) and 4 indicates a significant impact on traffic (i.e., long delay).
* 'Start_Time', Shows start time of the accident in local time zone.
* 'End_Time' : Shows end time of the accident in local time zone. End time here refers to when the impact of accident on traffic flow was dismissed.
* 'Start_Lat' : Shows latitude in GPS coordinate of the start point.
* 'Start_Lng' : Shows longitude in GPS coordinate of the start point.
* 'Temperature(F)' : Shows the temperature (in Fahrenheit)
* 'Humidity(%)' : Shows the humidity (in percentage).
* 'Pressure(in)' : Shows the air pressure (in inches).
* 'Visibility(mi)' : Shows visibility (in miles).
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

### Cleaning the dataset

After dropping the unused columns, we will look for the rows with missing values.
It looks like we have between 1.5% and 2.1% of rows with missing values for the weather related columns. 

<img src="https://user-images.githubusercontent.com/1349413/97034511-55c84300-1565-11eb-9e11-8a87a58ae487.png" alt="" width="400"/>

We can either fill the missing values or drop the impacted rows. As Those missing values are affecting all severity values so we will choose to drop the rows.

<img src="https://user-images.githubusercontent.com/1349413/97034516-582a9d00-1565-11eb-95ec-b9cd176f4768.png" alt="" width="700"/>

### Getting a balanced dataset

As we want to predict the severity, we check if the dataset is balanced for this feature

<img src="https://user-images.githubusercontent.com/1349413/97034632-80b29700-1565-11eb-92b4-5b7240ff3937.png" alt="" width="400"/>

It appears the dataset is unbalanced concerning the severity.

There is multiple ways to correct a dataset in order to have a balanced one<sup>4</sup>. Undersampling methods like [Random Undersampling](https://imbalanced-learn.readthedocs.io/en/stable/generated/imblearn.under_sampling.RandomUnderSampler.html#imblearn.under_sampling.RandomUnderSampler), [Edited Nearest Neighbours](https://imbalanced-learn.readthedocs.io/en/stable/generated/imblearn.under_sampling.EditedNearestNeighbours.html#imblearn.under_sampling.EditedNearestNeighbours) or [Tomek Links](https://imbalanced-learn.readthedocs.io/en/stable/generated/imblearn.under_sampling.TomekLinks.html#imblearn.under_sampling.TomekLinks), could be used, but it would lead to having only 29175 data for each severity and we would lost the advantage of a 3.5 million records.

We also have oversampling methods like [Random Over-Sampling](https://imbalanced-learn.readthedocs.io/en/stable/generated/imblearn.over_sampling.RandomOverSampler.html#imblearn.over_sampling.RandomOverSampler), [SMOTE](https://imbalanced-learn.readthedocs.io/en/stable/generated/imblearn.over_sampling.SMOTE.html#imblearn.over_sampling.SMOTE) or [ADASYN](https://imbalanced-learn.readthedocs.io/en/stable/generated/imblearn.over_sampling.ADASYN.html#imblearn.over_sampling.ADASYN) where we would generate additional data of the minority class and keep all the majority class. However, oversampling the minority class can lead to overfitting the model, since it will introduce duplicate instances of a set that is already small.

<img src="https://raw.githubusercontent.com/rafjaa/machine_learning_fecib/master/src/static/img/resampling.png" alt="" width="700"/>

[source](https://www.kaggle.com/rafjaa/resampling-strategies-for-imbalanced-datasets#t1)

Another alternative is a hybrid method combining both udersampling and oversampling like [SMOTEENN](https://imbalanced-learn.readthedocs.io/en/stable/generated/imblearn.combine.SMOTEENN.html#imblearn.combine.SMOTEENN) or [SMOTETomek](https://imbalanced-learn.readthedocs.io/en/stable/generated/imblearn.combine.SMOTETomek.html#imblearn.combine.SMOTETomek).

We will use an hybrid method to get a balanced dataset

<img src="https://user-images.githubusercontent.com/1349413/97109601-6f3bcd00-16d4-11eb-901b-3ea416dbb6fd.png" alt="" width="600"/>

After using SMOTEENN we can see the repartition of the Severity feature is better. We will run it one more time to even the repartition.

<img src="https://user-images.githubusercontent.com/1349413/97109651-b5912c00-16d4-11eb-8d8f-dc49d6cde17e.png" alt="" width="600"/>

We can see the dataset is well balanced know and we can begin to use it.

## Methodology

### Finding correlation

We will use the Pearson Correlation to find out if some specific variables have an interdependence with the Severity of an accident

The Pearson Correlation measures the linear dependence between two variables X and Y.
The resulting coefficient is a value between -1 and 1 inclusive, where:
* 1: Total positive linear correlation.
* 0: No linear correlation, the two variables most likely do not affect each other.
* -1: Total negative linear correlation.

<img src="https://user-images.githubusercontent.com/1349413/97780670-43ae5c00-1b86-11eb-8c0f-44cf1530c29b.png" alt="" width="600"/>

We can see that there is no variable that have a significant interdependence with the Severity feature. 

As 2 variables: Humidity and pressure have the best results, we will use the meteorological variables and see if we can have good results predicting the severity of a car accident with them.

### Model Development

We will try 2 different classification models :

* KNN
* Decision Tree

#### K-Nearest Neighbors
Let's start with KNN.

K-Nearest Neighbors is an algorithm for supervised learning. Where the data is 'trained' with data points corresponding to their classification. Once a point is to be predicted, it takes into account the 'K' nearest points to it to determine it's classification.

#### Decision Tree

The basic intuition behind a decision tree is to map out all possible decision paths in the form of a tree

Each internal node corresponds to a test
Each branch corresponds to a result of the test
Each leaf node assigns a classification
We will first create an instance of the DecisionTreeClassifier called severityTree. Inside of the classifier, specify criterion="entropy" so we can see the information gain of each node.

## Results

## Discussion

## Conclusion

###### References
<sup>1</sup>World Health Organization (WHO) - Global Status Report on Road Safety 2018 : https://www.who.int/violence_injury_prevention/road_safety_status/2018/en/external

<sup>2</sup>World Health Organization (WHO) - Global Plan for the Decade of Action for Road Safety 2011-2020 : https://www.who.int/roadsafety/decade_of_action/plan/plan_english.pdf?ua=1

<sup>3</sup>Moosavi, Sobhan, Mohammad Hossein Samavatian, Srinivasan Parthasarathy, and Rajiv Ramnath. “A Countrywide Traffic Accident Dataset.”, 2019.
Moosavi, Sobhan, Mohammad Hossein Samavatian, Srinivasan Parthasarathy, Radu Teodorescu, and Rajiv Ramnath. "Accident Risk Prediction based on Heterogeneous Sparse Data: New Dataset and Insights." In proceedings of the 27th ACM SIGSPATIAL International Conference on Advances in Geographic Information Systems, ACM, 2019.

<sup>4</sup>https://blog.soat.fr/2019/12/techniques-augmentation-dataset-smote/

