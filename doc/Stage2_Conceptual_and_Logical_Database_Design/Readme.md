# Stage2: Flight Status Visualizing Map
------------------------------------------
## URL version Diagram:

<p align="center">
  <img src="https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/blob/main/doc/Stage2_Conceptual_and_Logical_Database_Design/Stage2_image/Stage2_ER_diagram-v05.png" alt="ER-diagram"/>
</p>

* **Airport &#8592;&#8594; Flight:**  
  •	We think each airport can allow multiple airplanes to arrive.  
  •	We think each airport can allow multiple airplanes to arrive.

* **Airport &#8592;&#8594; Flight:**  
  •	We think each airport can allow multiple airplanes to depart. 
  •	We think each airplane departs from one airport.

* **Company &#8592;&#8594; Flight:**  
  •	We think each company has multiple flights schedule.  
  •	But there each flight schedule belongs to only one company.
  
* **Airplane_Record &#8592;&#8594; Flight:**  
  •	Each flight has several flighting information.  
  •	Each flighting information belongs to only one flight.

* **Flight &#8592;&#8594; Distance:**  
  • Each flight can only have a route information. 
  •	A route can be picked up by different flight.
  
* **Company &#8592;&#8594; Airplane_Reviews:**  
  • Each air company can receive multiple airplane review. 
  •	Each airplane reviews points to only one company.

## DDL SQL Command:

  * Company(**<ins>IATA_Designator</ins>**, AirlaneName);  
  * Airport(**<ins>IATA_Code</ins>**, Airport, Latitude, Longtitude, City, State);  
  * Flight(**<ins>IATA_Designator</ins>**, **<ins>FlightNumber<ins>**, Origin_Airport, Destination_Airport, Schedule_Departure, Scheduled_Time, Scheduled_Arrival, Distance);  
  * Airplane_Record(**<ins>TailNumber</ins>**, **<ins>FlightNumber</ins>**, IATA_Designator, Month, Day, DayOfWeek, Departure_Time, Departure_Delay, Taxi_Out, Elapsed_Time, Air_Time, Taxi_In, Arrival_Time, Arrival_Delay);  
  * Airline_Reviews(**<ins>Review_ID</ins>**, Airline_Name, Overall, Author, Review_date, Aircraft, Traveller_type, Cabin, Route, Date_flown, Seat_comfort, Cabin_service, Food_bev, Entertainment, Ground_service, Value_for_money, Recommended);


### Create New Table:
#### Company
``` sql
CREATE TABLE Company
(
IATA_Designator VARCHAR(2) NOT NULL, 
AirlineName VARCHAR(100),

PRIMARY KEY ( IATA_Designator)
);
```

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

#### Airline_Reviews
``` sql
CREATE TABLE Airline_Reviews
(
Review_ID INT NOT NULL,
AirlineName VARCHAR(100) NOT NULL,
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




