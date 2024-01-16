
# Stage3: Database Implementation and Indexing
------------------------------------------

### A. Proof of GCP Setup:
<p align="center">
  <img src="https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/blob/main/doc/Stage3_Database_Implementatio_and_Indexing/Image/Proof%20of%20GCP%20Setup.png" alt="ER-diagram"/>
</p>

### B. DDL Commands And Row Counts:
#### Company
``` sql
CREATE TABLE Company
(
IATA_Designator VARCHAR(2) NOT NULL, 
AirlaneName VARCHAR(100),

PRIMARY KEY ( IATA_Designator)
);
```
<p align="center">
  <img src="https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/blob/main/doc/Stage3_Database_Implementatio_and_Indexing/Image/Company_count.png" alt="ER-diagram"/>
</p>

#### Airport
``` sql
CREATE TABLE Airport
(
IATA_Code VARCHAR(100) NOT NULL, 
Airport VARCHAR(500),
City VARCHAR(500) NOT NULL,
State VARCHAR(100) NOT NULL,
Latitude DOUBLE,
Longtitude DOUBLE,

PRIMARY KEY (IATA_Code)
);
```
<p align="center">
  <img src="https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/blob/main/doc/Stage3_Database_Implementatio_and_Indexing/Image/Airport_count.png" alt="ER-diagram"/>
</p>

#### Airplane_Record
``` sql
CREATE TABLE Airplane_Record
(
FlightNumber INT NOT NULL,
IATA_Designator VARCHAR(2) NOT NULL, 
Month VARCHAR(512)  NOT NULL, 
Day VARCHAR(512)  NOT NULL, 
DayOfWeek VARCHAR(512)  NOT NULL, 
TailNumber VARCHAR(100)  NOT NULL,
Departure_Time INT, 
Departure_Delay INT, 
Taxi_Out INT, 
Elapsed_Time INT,
Air_Time INT, 
Taxi_In INT,
Arrival_Time INT, 
Arrival_Delay INT, 

PRIMARY KEY (TailNumber, FlightNumber)
);
```
<p align="center">
  <img src="https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/blob/main/doc/Stage3_Database_Implementatio_and_Indexing/Image/Airplane_Records_count.png" alt="ER-diagram"/>
</p>


#### Flight
``` sql
CREATE TABLE Flight
(
IATA_Designator VARCHAR(3) NOT NULL, 
FlightNumber INT NOT NULL,
Origin_Airport VARCHAR(5) NOT NULL,
Destination_Airport VARCHAR(5) NOT NULL,
Schedule_Departure INT, 
Scheduled_Time INT, 
Scheduled_Arrival INT, 
Distance INT,

PRIMARY KEY (IATA_Code, FlightNumber),
FOREIGN KEY (Origin_Airport) REFERENCES Airport (IATA_Code),
FOREIGN KEY (Destination_Airport) REFERENCES Airport (IATA_Code)
);
```

<p align="center">
  <img src="https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/blob/main/doc/Stage3_Database_Implementatio_and_Indexing/Image/Flight_count.png" alt="ER-diagram"/>
</p>

#### Airline_Reviews
``` sql
CREATE TABLE Airline_Reviews
(
Review_ID INT NOT NULL,
Airline_Name VARCHAR(100) NOT NULL,
Overall INT,
Author VARCHAR(100),
Review_date VARCHAR(100),
Aircraft VARCHAR(100),
Traveller_type VARCHAR(100),
Cabin VARCHAR(100),
Route VARCHAR(100),
Date_flown VARCHAR(100),
Seat_comfort VARCHAR(100),
Cabin_service VARCHAR(100),  
Food_bev VARCHAR(100),
Entertainment VARCHAR(100),
Ground_service VARCHAR(100),
Value_for_money VARCHAR(100),
Recommended VARCHAR(100),

PRIMARY KEY (Review_ID)
);
```
<p align="center">
  <img src="https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/blob/main/doc/Stage3_Database_Implementatio_and_Indexing/Image/Airplane_Reviews_count.png" alt="ER-diagram"/>
</p>

### C. Advanced Queries:
#### Advanced Query #1:

``` sql
SELECT FlightNumber, City FROM Flight JOIN Airport ON Flight.Original_Airport = Airport.IATA_Code WHERE FlightNumber IN (SELECT FlightNumber FROM Airplane_Record WHERE 1 <= Month and Month <=3);
``` 

We are selecting the flight number and city for the flights that were scheduled from the first 3 months of 2015 in this query.   
**(JOIN and SUBQUERY)**
![image](https://user-images.githubusercontent.com/97086822/224241311-036ba55d-6e70-4c32-9ed6-afae0e25c48f.png)

#### Advanced Query #2:
``` sql
SELECT IATA_Designator, AVG(Departure_Delay + Arrival_Delay) FROM Airplane_Record WHERE DayOfWeek IN (SELECT DayofWeek FROM Airplane_Record WHERE DayOfWeek = 4) GROUP BY IATA_Designator;
``` 
We are computing and selecting the average delay time for flights that were scheduled on Wednesdays in 2015. **(GROUP BY and SUBQUERY)**
This only has 14 data values because we are using a limited number of rows for our dataset since uploading a larger file doesn’t work on GCP.
![image](https://user-images.githubusercontent.com/97086822/224241547-8dfecf81-82e5-46f8-bd63-72027ade28fd.png)


### D. Indexing:
#### Query 1:
The nested loop inner joins costs are **25089.14** and **12518.05**, respectively. These are **not** very optimal.
![image](https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/blob/main/doc/Stage3_Database_Implementatio_and_Indexing/Image/Query1-1.png)
We added an index using the **FlightNumber** column because FlightNumbers are unique values for our tables. Adding this index increases the performance of query 1, as seen below:
The nested inner loops now only cost **205.07** and **161.59**, respectively, which is a pretty drastic improvement from the original query without indexing.
![image](https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/blob/main/doc/Stage3_Database_Implementatio_and_Indexing/Image/Query1-2.png)

We tried indexing on city for this query, but that index did not provide any changes to its performance. This could be because a large number of rows could share the same city attribute, so indexing would still not help improve the efficiency of the query.
![image](https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/blob/main/doc/Stage3_Database_Implementatio_and_Indexing/Image/Query1-3.png)

We also tried indexing on distance for this query, and, as seen in the image above, the cost increased greatly to **330508.79** as well (the same cost as indexing on city) and is much greater than the cost when we indexed on flight number. A large number of rows may also share similar distance as flights usually take the same paths during each trip. 
![image](https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/blob/main/doc/Stage3_Database_Implementatio_and_Indexing/Image/Query1-4.png)

#### Query 2:

In this query, the nest loop inner join cost is **10405**, which is a pretty high number.
We decided to index on the day of the week for this query because we used **DayOfWeek** in the WHERE clause of the query so indexing by that could possibly help increase the performance of the query.
![image](https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/blob/main/doc/Stage3_Database_Implementatio_and_Indexing/Image/Query2-1.png)


2nd version upload:

As seen in the EXPLAIN ANALYZE above, indexing by the day of the week did in fact improve the performance of this query. The nest loop inner join cost only 137.46 this time, which is yet another good improvement from the original query.


Next, we tried indexing on the Month. This worked surprisingly well, as the cost was only 61.35 for the inner loop as compared to the 137.46 from the previous indexing cost. This can be seen in the EXPLAIN ANALYZE image below:
![image](https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/blob/main/doc/Stage3_Database_Implementatio_and_Indexing/Image/Query2-2.png)


Finally, we decided to also try indexing on the TailNumber. We decided to do this because it’s a primary key for the Airplane_Record table, so we wanted to see whether it would help. Indexing on TailNumber yielded a cost of 61.35 for next loop inner join, which is the same as the cost when indexed by Month. Thus, we concluded that a good option for our project would be to index by either the TailNumber or Month, based on the context of our functions.

![image](https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/blob/main/doc/Stage3_Database_Implementatio_and_Indexing/Image/Query2-3.png)


### E. Changes Made to the Stage 2:
[Stage2 revisited:](https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/tree/main/doc/Stage2_Conceptual_and_Logical_Database_Design)
*	Since we did not have four main entities in our first submission for Stage 2, we found another dataset to join with our current files. It includes the **airline reviews** for the most popular airlines in 2018 and can be found using this link: https://www.kaggle.com/datasets/efehandanisman/skytrax-airline-reviews?resource=download. Using this, we created our fourth main entity “Reviews” with primary key “airlines” that connects to our company entity. We know that this this data is reliable as it was used for MEF University Big Data Analytics programme for 2018-2019, and it is relevant to our project as it allows us to analyze and connect the raw data behind delays and cancellations and real customer feedback. 
*	We have also **merged and update some of our smaller entities** together to better organize our data, and we have remarked the weak entities in our diagram. 
*	**Revisited the relationship** and check if this relationship exists or not.
*	**Release version updated**.
*	**Delete weak entity**(we discuss and think in the table, the weak enetity did not exist.
*	Updated **entity descriptions**.




