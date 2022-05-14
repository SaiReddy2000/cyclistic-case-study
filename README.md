---

# **Google Data Analytics:Capstone Project**

---

## **Cyclistic Bike-Share Analysis**

---
---

### **Project Overview**  

---  


**Cyclistic**, a bike-sharing firm, believes that increasing the number of annual members over casual riders is the key to future success. The marketing analyst tems needs to know the following in order to develop a new marketing plan focused at converting casual riders into annual members:

* What are the differences in how annual members and casual riders utilize Cyclistic bikes?

* Why would an casual rider purchase a Cyclistic annual membership?

* How can Cyclistic utilize digital media to encourage casual members to become annual members?

I will be answering the first question using the 6 steps of data analysis taught in the Google Data Analytics course; **ask**, **prepare**, **process**, **analyze**, **share**, and **act**.

The primary tools for my project are **R** for **Data Analysis**, and **Tableau** for **Data Visualization**.

---

### **Phase 1:Ask**  

---  


The **Cyclistic** executive team is focused on optimizing the company's future growth. The head of marketing, is focused with securing this growth by developing a marketing plan to turn casual Cyclistic riders into annual members. My marketing analytics team is focused on leveraging our data to answer the three questions above and then using the answers to steer the marketing campaign.

The current job is to evaluate the data and discover major behavioral distinctions between casual riders and annual members so that the firm may be advised on next moves.

---

### **Phase 2:Prepare - (Data Transformation)**

---  

The project's data is stored on Amazon Web Services (AWS) (Amazon Web services). I'm utilizing travel data from the previous 12 months, starting in 2021-05 and ending in 2022-04. Motivate International Inc. has made the data accessible under this license after collecting it directly from Cyclistic. There is no personally identifying information in the data because it has been anonymised. While this will prevent analyses that look into the personal characteristics of individual riders, such as their history or where they reside, but there is still enough data to uncover certain patterns.

The dataset is publicly available on [kaggle](https://www.kaggle.com/datasets/saireddy2000/cyclistic-bike-share-data-may-2021-to-apr-2022).

---

### **Phase 3:Process - (Data Cleaning)**

---  

The total changes made to the data are summarized below:  

* Excluded geographical coordinates
* Removed rows with null values
* Removed duplicate rows
* Removed whitespaces
* Ensured consistency in datatypes across variables
* Created columns to report the year,month,day and hour of each ride
* Created a column to report duration of each ride
* Excluded trips lasting less than or equal to 0 seconds  

---  

### **Phase 4: Analyze - (Data Analysis)**

---  

A detailed report on the complete **Data Analysis Process** along with the **Code** can be found [here](https://github.com/SaiReddy2000/cyclistic-case-study/blob/main/Data%20Analysis.md).

I explored several variables for differences in behaviour between annual members and casual riders:

* Number of users
* Use of bicyle types
* Prefered days of week
* Prefered hours of the day
* Duration of the rides
* Most visited stations

I also explored general trends in order to determine the usage of Cyclistic's services regardless of the user type:

* Prefered months of the year  

---

### **Phase 5: Share - (Data Visualization)**

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








