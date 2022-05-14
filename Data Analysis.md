---

# **Google Data Analytics:Capstone Project**

---

## **Cyclistic Bike-Share Analysis**

---
---

### **Introduction**  

---  


This is my capstone case study that I completed as part of the **Google Data Analytics Professional Certificate**.

I will be following the corresponding steps of the **Data Analysis Process** as my guidelines for the completion of the project:  


* **Ask**
* **Prepare**
* **Process**
* **Analyze**
* **Share**
* **Act**

The primary tools for my project are **R** for **Data Analysis**, and **Tableau** for **Data Visualization**.

---

### **About the company**  

---  


**Cyclistic** developed a successful bike-share program in 2016. Since then, the initiative has evolved to include a fleet of 5,824 bicycles that are geotracked and locked into 692 stations across Chicago. The bikes may be unlocked and returned to any other station in the system at any time.  

**Cyclistic** also distinguishes itself by providing reclining bikes, hand tricycles, and cargo bikes, making bike-share more accessible to persons with impairments and others who are unable to ride a regular two-wheeled bike.  

**Cyclistic** offers a variety of price options, including single-ride passes, full-day permits, and annual memberships. Casual riders are customers who purchase single-ride or full-day passes. Member riders are customers who pay yearly memberships.

---

### **Phase 1:Ask**

---  


#### **Scenario**  


You work as a junior data analyst in the marketing analyst team of **Cyclistic**, a Chicago-based bike-share firm. The director of marketing feels that increasing the number of yearly subscriptions is critical to the company's future success. As a result, your team is interested in learning how casual riders and member riders utilize Cyclistic bikes. Your team will devise a new marketing campaign based on these findings in order to convert casual riders into member riders. However, Cyclistic executives must first accept your ideas, therefore they must be supported with compelling data insights and good data visualizations.  

The question you'll have to answer comes from the director of marketing: **How do member riders and casual riders use Cyclistic bikes differently?**  


#### **Business Task**  


**Analyze the data to find major behavioral differences between casual and member riders so that a targeted marketing campaign can be presented to convert casual riders to members.**

---

### **Phase 2:Prepare**

--- 

#### **Data Transformation**


The data from the bike-sharing firm will be used in the project. The data used in the project is kept on AWS (Amazon Web Services). It was obtained directly from Cyclistic and made accessible under the license by Motivate International Inc. There is no personally identifying information in the data because it has been anonymised.  

For my case study, I'll concentrate on the years 2021-2022 because it's the more relevant to the business task.

The following information is accessible after downloading the data:  


* Unique id for each ride  
* Type of bikes (classic, electric, docked)
* When the ride started (date and time)
* When the ride ended (date and time)
* Where the ride started (start station name and the corresponding lattitude and longitude)
* Where the ride ended  (end station name and the corresponding lattitude and longitude)
* Whether it's a member or a casual rider  


#### **Code**

Installing packages thar are required to perform the analysis:

```{r}
install.packages("tidyverse", repos = "http://cran.us.r-project.org")
install.packages("lubridate", repos = "http://cran.us.r-project.org")
install.packages("here", repos = "http://cran.us.r-project.org")
install.packages("skimr", repos = "http://cran.us.r-project.org")

```

Loading the installed packages:

```{r}
library("tidyverse")
library("lubridate")
library("here")
library("skimr")

```

To check what the current working directory is:

```{r}
getwd()

```

To set the current working directory in order to extract the data:

```{r}
setwd("C:/Users/user/Desktop/Data Analytics - Capstone Project")

```

Reading the 12 csv files for the trip data of months from may-2021 to apr-2022:

```{r}
T_2021_05 <- read_csv("2021_05_Divvy_Tripdata.csv")
T_2021_06 <- read_csv("2021_06_Divvy_Tripdata.csv")
T_2021_07 <- read_csv("2021_07_Divvy_Tripdata.csv")
T_2021_08 <- read_csv("2021_08_Divvy_Tripdata.csv")
T_2021_09 <- read_csv("2021_09_Divvy_Tripdata.csv")
T_2021_10 <- read_csv("2021_10_Divvy_Tripdata.csv")
T_2021_11 <- read_csv("2021_11_Divvy_Tripdata.csv")
T_2021_12 <- read_csv("2021_12_Divvy_Tripdata.csv")
T_2022_01 <- read_csv("2022_01_Divvy_Tripdata.csv")
T_2022_02 <- read_csv("2022_02_Divvy_Tripdata.csv")
T_2022_03 <- read_csv("2022_03_Divvy_Tripdata.csv")
T_2022_04 <- read_csv("2022_04_Divvy_Tripdata.csv")

```

To check the data types and coloumn names of each of the datasets before merging them into a single dataset:

```{r}
str(T_2021_05)
str(T_2021_06)
str(T_2021_07)
str(T_2021_08)
str(T_2021_09)
str(T_2021_10)
str(T_2021_11)
str(T_2021_12)
str(T_2022_01)
str(T_2022_02)
str(T_2022_03)
str(T_2022_04)

```

Merging the 12 datasets into a single dataset in order to perform efficient analysis:

```{r}
T_All <- bind_rows(T_2021_05,T_2021_06,T_2021_07,T_2021_08,T_2021_09,T_2021_10,T_2021_11,T_2021_12,T_2022_01,T_2022_02,T_2022_03,T_2022_04)

```

---

### **Phase 3:Process**

---  


#### **Data Cleaning**  


The total changes made to the data are listed below:  


* Excluded geographical coordinates
* Removed rows with null values
* Removed duplicate rows
* Removed whitespaces
* Ensured consistency in datatypes across variables
* Created columns to report the year,month,day and hour of each ride
* Created a column to report duration of each ride
* Excluded trips lasting less than or equal to 0 seconds  


#### **Code**  


Removing coloums `start_lat`,`start_lng`,`end_lat` and `end_lng` which show the corresponding starting and ending latitude and longitude of ride trip as its not required in order to perform the analysis:

```{r}
T_All <- T_All %>%  
  select(-c(start_lat, start_lng, end_lat, end_lng))

```

Checking the coloumn names, the total number of rows and the generating insights into the data, its data types and high level view on its summary statistics:

```{r}
colnames(T_All)
nrow(T_All)
glimpse(T_All)
skim_without_charts(T_All)
head(T_All)

```

Removing rows with missing data:

```{r}
T_All <- T_All %>%
  drop_na()

```

Removing rows with duplicate data:

```{r}
T_All <- T_All %>%
  distinct()

```

Removing whitespace in the coloumns with character data type:

```{r}
T_All <- T_All %>%
  mutate_if(is.character, str_trim)

```

Creating new coloums by extracting the day, month, year and hour of the ride trip from the coloumn `stared_at`:

```{r}
T_All$day <- format(as.Date(T_All$started_at), "%A")
T_All$month <- format(as.Date(T_All$started_at), "%B")
T_All$year <- format(as.Date(T_All$started_at), "%Y")
T_All$hour <- format(as.POSIXct(T_All$started_at), "%H")
glimpse(T_All)

```
Creating a new coloumn to calculate the total ride time by finding the difference within `ended_at` and `started_at` and converting the `total_ride_time` coloumn into numeric data type:

```{r}
T_All$total_ride_time <- difftime(T_All$ended_at,T_All$started_at)
T_All$total_ride_time <- as.numeric(T_All$total_ride_time)
is.numeric(T_All$total_ride_time)
glimpse(T_All)

```
Removing rows which contain the `total_ride_time` as negative or zero value:

```{r}
T_All %>%
  filter(total_ride_time <= 0) %>%
  nrow()
T_All <- T_All[!(T_All$total_ride_time <= 0),]

```

---

### **Phase 4: Analyze**

---  

#### **Data Analysis**


I explored several variables for differences in behaviour between annual members and casual riders:

* Number of users
* Use of bicyle types
* Prefered days of week
* Prefered hours of the day
* Duration of the rides
* Most visited stations

I also explored general trends in order to determine the usage of Cyclistic's services regardless of the user type:

* Prefered months of the year  


#### **Code**  


Calculating the maximum, minimum and average time spent by a casual user:

```{r}
T_All %>%
  filter(member_casual == "casual") %>%
  summarize(max_casual = max(total_ride_time),min_casual = min(total_ride_time),avg_casual = mean(total_ride_time))

```

Calculating the maximum, minimum and average time spent by a member user:

```{r}
T_All %>%
  filter(member_casual == "member") %>%
  summarize(max_member = max(total_ride_time),min_member = min(total_ride_time),avg_member = mean(total_ride_time))

```

Calculating the ridership distribution based on the user type (Casual vs Member):

```{r}
T_All %>%
  group_by(member_casual) %>%
  summarize(number_of_rides = n())

```

Calculating the total ride time based on the user type (Casual vs Member):

```{r}
T_All %>%
  group_by(member_casual) %>%
  summarize(total_ride_time = sum(total_ride_time))

```

Calculating the usage of each of the bike types based on the user type (Casual vs Member):

```{r}
T_All %>%
  filter(member_casual == "casual") %>%
  group_by(rideable_type) %>%
  summarize(number_of_rides = n())

T_All %>%
  filter(member_casual == "member") %>%
  group_by(rideable_type) %>%
  summarize(number_of_rides = n())

```

Calculating the most visited start and end stations for both casual and member riders: 

```{r}
T_All %>%
  filter(member_casual == "casual") %>%
  group_by(start_station_name) %>%
  summarize(number_of_rides = n()) %>%
  arrange(-number_of_rides) %>%
  head(10)

T_All %>%
  filter(member_casual == "casual") %>%
  group_by(end_station_name) %>%
  summarize(number_of_rides = n()) %>%
  arrange(-number_of_rides) %>%
  head(10)

T_All %>%
  filter(member_casual == "member") %>%
  group_by(start_station_name) %>%
  summarize(number_of_rides = n()) %>%
  arrange(-number_of_rides) %>%
  head(10)

T_All %>%
  filter(member_casual == "member") %>%
  group_by(end_station_name) %>%
  summarize(number_of_rides = n()) %>%
  arrange(-number_of_rides) %>%
  head(10)

```

Calculating the number of riders based on months of the year:

```{r}
T_All %>%
  group_by(month) %>%
  summarize(number_of_rides = n())

```

Calculating the number of both casual and member riders based on the day of the week:

```{r}
T_All %>%
  filter(member_casual == "casual") %>%
  group_by(day) %>%
  summarize(number_of_rides = n())

T_All %>%
  filter(member_casual == "member") %>%
  group_by(day) %>%
  summarize(number_of_rides = n())

```

Calculating the number of both casual and member riders based on the hour of the day:

```{r}
T_All %>%
  filter(member_casual == "casual") %>%
  group_by(hour) %>%
  summarize(number_of_rides = n()) %>%
  arrange(hour)

T_All %>%
  filter(member_casual == "member") %>%
  group_by(hour) %>%
  summarize(number_of_rides = n()) %>%
  arrange(hour)

```

---

### **Phase 5: Share**

---  

#### **Data Visualization - Tableau**

---  

![ ](https://github.com/SaiReddy2000/cyclistic-case-study/blob/main/Images/Ridership_Distribution_(%20Casual%20vs%20Member%20).png?raw=true)

---

##### **Analysis:**  


It can be observed that member riders make up a larger part of the dataset (56.33 %), indicating that there are more member riders than casual riders (43.67 %).

---

![ ](https://github.com/SaiReddy2000/cyclistic-case-study/blob/main/Images/Total_Ridership_Time_(%20Casual%20vs%20Member%20).png?raw=true)

---

##### **Analysis:**  


* It can be observed that even though there are more member riders, the casual riders travel for more time yearly than the member riders, indicating a more leisure-oriented usage vs. a more "public transportation" or pragmatic use of the bikes by the member riders.

* On the assumption that yearly members have more completely integrated bike riding into their daily life, the use of the bicycle for shorter periods of time makes sense. A casual rider may view biking as a fun activity and hence choose to ride more leisurely and for longer periods of time. Furthermore, a casual rider may feel compelled to ride the bike for longer to maximize their money's worth because they must pay an unlocking fee at the start of their ride, which is waived for members.

---

![ ](https://github.com/SaiReddy2000/cyclistic-case-study/blob/main/Images/Bike_Type_Usage_(%20Casual%20vs%20Member%20).png?raw=true)

---

##### **Analysis:**  


We can observe that member riders only use two sorts of bikes for their rides: classic and electric, while the casual riders utilize all three types of bikes available: classic, electric, and docked. Both casual and member riders have a clear preference for classic bikes, which is followed by the electric bikes. The docked bike is clearly the least used/preferred bike by both casual and member riders.

---

![ ](https://github.com/SaiReddy2000/cyclistic-case-study/blob/main/Images/Ridership_Distribution_based_on_Months.png?raw=true)

---

##### **Analysis:**  


* A year of Cycliystic bike usage appears to follow a general rising trend from May 2021 to July 2021, when it reaches its peak. From this month on, usage drops gradually until January 2022, when it reaches its lowest overall usage of the year.

* The weather might a reason for the drastic fluctuations in usage across the months.

* A normal year of weather in Chicago, according to Weather Spark, includes a hot season from early June to late September and a cold season from early December to early March. The wind is highest from October to May, while the months of June, July, and August are the calmest. Rain falls throughout the year, however the most of it falls in the 31 days before June. Finally, throughout the months of December to March, there is a snowy season.

* These particular weather conditions appear to be linked to the use of bicycles.

* Temperature appears to have a significant impact on the number of rides per month, as evidenced by the fact that bike usage peaks in the months leading up to July, which corresponds to the summer months in Chicago, and reaches its lows in the months leading up to January, which corresponds to the winter season in Chicago.

---

![ ](https://github.com/SaiReddy2000/cyclistic-case-study/blob/main/Images/Ridership_Distribution_based_on_the%20_Day_(%20Casual%20vs%20Member%20).png?raw=true)

---

##### **Analysis:**  


* Saturday is the most popular day for casual riders. The second most popular day is Sunday, followed by Friday. The next four weekdays are about evenly divided, with lower utilization than the weekends.

* The usage of bikes by member riders is significantly more evenly distributed. The day with the most usage being Wednesday, while the day with the least usage is Sunday, followed by Saturday.

* It's hardly surprise that weekend rides are the most popular among casual riders.

* Based on this data, it's safe to say that the majority of casual riders do not include riding into their daily routine. While a casual member may be more likely to use a bike on occasion for transportation or entertainment, an annual member is more likely to utilize the bike on a daily basis, whether for commuting to work, exercising, or running errands.

---

![ ](https://github.com/SaiReddy2000/cyclistic-case-study/blob/main/Images/Ridership_Distribution_based_on_Time_of_the_Day_(%20Casual%20vs%20Member%20).png?raw=true)

---

##### **Analysis:**  



* The two peak hours for member riders are 7 a.m. to 9 a.m. and 4 p.m. to 6 p.m. The peak period for casual riders is from 12 p.m. to 6 p.m.

* This suggests that member riders are people who ride their bikes to work (data points between 7 and 9 a.m.) and return from work(data points between 4 p.m to 6 p.m).

* It also suggests that casual riders are most likely utilizing the bike for recreational purposes because their maxima occur in the afternoon to evening period, which are typically working hours.

---

![ ](https://github.com/SaiReddy2000/cyclistic-case-study/blob/main/Images/Top_10_visited_stations%20-%20Casual.png?raw=true)

---

---

![ ](https://github.com/SaiReddy2000/cyclistic-case-study/blob/main/Images/Top_10_visited_stations%20-%20Member.png?raw=true)

---

##### **Analysis:**  


* The popularity of certain stations is more significant in terms of casual riders.The station with the most visitors, Streeter Dr & Grand Ave, had 32,567 more visitors than the station with the second most visitors, DuSabel Lake Shore Dr & Monroe St. The gap between member rider's most visited stations, Kingsbury St & Kinzie St and Clark St & Elm St, is only 763 visitors.

* This may be seen throughout the list. The difference in casual rides between the most and least visited stations is 53,253 trips within the list. The gap between the most and least visited stations for member riders is only 7,193 rides within the list.

* The top four locations of casual riders is suggestive of their purpose. All four are located in locale that provides entertainment and potentially more leisure activites, such as the pier, the park and even the theatre. The top four locations of member rides are nearby or inside business districts, indicative of places of employement or errands.

---

### **Phase 6: Act**

---

I would like to suggest the following in order to convert casual users into annual customers:  


* It might be beneficial to emphasize the advertisements on the leisure side of the bike-share service and perhaps give some sort of weekend promotions which are exclusive to annual members, and as the most usage of service by the casual users happens during the weekends, this could promote conversions to being a annual member.

* Increasing the benefits for using the bike-share services during the winter months by having coupons and discounts distributed because service usage reaches its lows in the winter months therefore these benefits could promote more usage of the services.

* Advertising and promoting based on the most popular months, In the months leading up to the summer, **Cyclistic** could offer cheap annual subscriptions and also consider varied pricing options, such as seasonal passes, to boost conversion rates.

* Aiming to promote initiatives/ad campaigns primarily focused on the top 10 most visited stations by both the casual and member users.

---
