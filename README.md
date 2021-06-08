# Data Analysis - Generic Dataset: Project Overview

In this project we analyzed a generic dataset with no clear definitions with the objective of generate insights and tell a history on it.

To do that we followed three main steps: 
1. Data Understanding: where we draw some basic initial assumptions about the dataset;
2. Data Preparation: where we adjust our data set by cleaning, completing and adding features: https://github.com/giovannisampaio/booking_data_analysis/blob/main/clean_data.ipynb
3. Exploratory Data Analysis (EDA): where we deepen our understanding about the dataset by relying on Pivote tables and Data Visualization techniques: https://github.com/giovannisampaio/booking_data_analysis/blob/main/eda.ipynb

## Code and Resources 
**Python Version:** 3.9.5  
**Packages:** pandas, numpy, matplotlib, seaborn

## Data Understading

### **What are the features available in the dataset?** ###

```python
['Unnamed: 0' 'channel' 'cnt' 'date_time' 'hotel_cluster'
 'hotel_continent' 'hotel_country' 'hotel_market' 'is_booking' 'is_mobile'
 'is_package' 'month' 'orig_destination_distance' 'posa_continent'
 'site_name' 'srch_adults_cnt' 'srch_children_cnt' 'srch_ci' 'srch_co'
 'srch_destination_id' 'srch_destination_type_id' 'srch_rm_cnt' 'user_id'
 'user_location_city' 'user_location_country' 'user_location_region'
 'year']
```

## Data Preparation

Cleaning

*	Removed the first and unamed column due to lack of usage
*	Removed column 'cnt' due to almost uniform value and no clear meaning
*	Removed columns 'month' and 'year' due to redundancy ('date_time' already includes the information)
*	Removed 'is_booking' due to its uniform value (all records are equals 1)

Adding features

* Added columns for duration of stay in days ('days_stay') and for how many days in advance the booking was done ('days_in_adv')

Missing values

* Replaced NA values on column 'orig_destination_distance' by values in a sample from existing values in order to not impact the exponential distribution observed for the feature

## EDA

First we confirm some assumptions about the location data:
*	'hotel cluster' is not contrained by location, as the same cluster can include several cotinents and countries
*	Except for only one case, each 'hotel_market' is limited to only one 'hotel_country'

Next, going through some pivot tables we observe that many features have an exponential distribution:
*	One 'hotel_country' has more than 50% of all bookings
*	![imagem](https://user-images.githubusercontent.com/18421068/120936620-aa898a00-c700-11eb-8b89-166da2205764.png)
*	One 'site_name' accounts for around 64% of bookings
*	![imagem](https://user-images.githubusercontent.com/18421068/120936695-0bb15d80-c701-11eb-8fd6-1c16ce73a3fd.png)
*	One 'destination_type_id' has more than 50% of the bookings
*	![imagem](https://user-images.githubusercontent.com/18421068/120936972-bc6c2c80-c702-11eb-8a6b-d8e04e7cffb6.png)
*	The distribution by 'user_location_country' shows that most of 50% bookings are done by users from one single country:
*	![imagem](https://user-images.githubusercontent.com/18421068/120936751-6480f600-c701-11eb-91a5-aed58e845bbc.png)

The pivot tables reveal a distinct user's pattern:
*	Most users are booking only once during the period in the dataset, but there are users with more than 10 bookings, which might indicate the pattern of travel agencies using the platform. This can be observed by using a [box plot](https://en.wikipedia.org/wiki/Box_plot) over a pivot table containing the number of records by each user_id.
*	![imagem](https://user-images.githubusercontent.com/18421068/120936836-f4bf3b00-c701-11eb-81b4-35d002bb74e7.png)

Then, we identify that a smaller part of users are buying travel packages or using mobile devices for bookings:

* Around 9.2% of bookings are done on mobile devices
* ![imagem](https://user-images.githubusercontent.com/18421068/120937407-284f9480-c705-11eb-9b65-a27291cba065.png)

* 13% of bookins appears to be part of travel packages
* ![imagem](https://user-images.githubusercontent.com/18421068/120937113-82e7f100-c703-11eb-838a-65f26a0a0c93.png)

One of the most useful data visualization for numerical data is the correlation matrix. It quickly allows us to visualize the correlation strength between different features:

![imagem](https://user-images.githubusercontent.com/18421068/120937535-e8d57800-c705-11eb-97b4-992d445f4d28.png)

* From the visualization above we can gather that, apart from the more obvious relationship between number of adults and number of rooms, there is a significant positive correlation between package bookings and number of days of stay.
* There is also some positive correaltion between number of days in advance of the booking the distance of origin, the number of people (adults and children) and the number of days of stay.

We can also visualize the number of check-ins booked over time. Most checkins are from september 2013 to January 2014:

![imagem](https://user-images.githubusercontent.com/18421068/120939936-68694400-c712-11eb-843a-07a3cbe71157.png)

The date with the highest number of reservations being 27-12-2013:

![imagem](https://user-images.githubusercontent.com/18421068/120940006-d4e44300-c712-11eb-844c-710dfabdca09.png)




