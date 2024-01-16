## Project Summary

Flight Delays and Cancellations are not uncommon. There may be patterns in these occurrences, and being able to visualize them in a simple way can help people determine what airlines to avoid. Our project will record data from DOT’s 2015 airline statistics and plot them on an interactive map displaying major airports (As long as the data continues to be updated in the same format, our application should be able to model these changes so we are not limited to displaying data from 2015). 

Color coding will be used to indicate the frequency of delayed or canceled flights for destination and origin airports, as well as airlines. Some other features will include the formation of tables that display the number of flights delayed per origin and departure airport, a running leaderboard ranking airlines with the fewest number of delays and cancellations to the ones with the most. Graphical representations of the data will also be presented along with the map and tables, which will predict future flight delays (based on either location or airport). 

* Data
The data we will be using consist of flight delays and cancellations from 2015 published by the DOT's Bureau of Transportation Statistics. We will extract IATA_code, airport, city, state, departure delay, and dates from the three CSV files of flight information. We plan on utilizing geographical data (airport, city, state, etc) to aid in the construction of our map, and other statistics (such as departure time, weather delays, cancelations, etc) to create our own tables, rankings, and predictions. 


* Basic Functions
The purpose of our website is to visualize flight delay and cancelation data in a comprehensive and user-friendly way. The main functions will consist of a map with all the airport locations marked in color-coordinated symbols indicating details like delayed, on-time, diverted, and canceled flights per location. Some simple functions include having multiple summarizing tables and displaying delay and cancelation frequencies for respective airlines and locations, allowing users to make better decisions when booking flights for the future. One of the more complicated functions is the prediction feature, which will allow users to input airlines or flight paths (origin and destination) to view a program-generated estimate of whether delays will occur. 

### Creative Component

Since we have a substantial amount of data to work with, we run into the possibility of our map becoming overcrowded. A way to combat this while adding a unique feature is to implement a toggling option, specifically, a hover display function where when the user hovers their mouse over a dot and more detailed information will be presented from the columns of the flights.csv. If possible, we would also like to make our map interactive, meaning that users can zoom in to see view specific locations in higher detail. 

### Description

Flight delays and cancellations are inevitable, and there are a variety of causes for them. They are all conditional, but only through the visualization of large amounts of data are trends identifiable. There is currently no easy or consistent way for people to predict if their flight will be delayed or not, and our application aims to address this. Our website will consist mainly of a map and a few tables/charts that present patterns in raw data that are otherwise uninterpretable to users without highly specific tools and knowledge. We aim to make flight data accessible and comprehensive by modeling it in an intuitive manner (seeing physical lines representing flights and symbols representing airports) while ensuring credible data sourcing (new data must be consistent with DOT’s reports in order to be appended). We can therefore analyze which airport exhibits frequent late departures through correlations and potentially suggest airline companies improve the accuracy of their departure times.

### Usefulness

Statistic-based applications exist, but they usually do not provide enough information about flights. An example includes the Bureau of Transportation Statistics’ own [website](https://www.transtats.bts.gov/ontime/Cancellation.aspx), which states that it provides detailed cancelation statistics, but as no visualization features are present, the interface becomes unappealing and inefficient to use. Instead, we plan to use aggregation to note how many hours the flight delays, and how frequently flights from specific airlines are delayed. Flightview by [OAG also exists](https://www.flightview.com/traveltools/), which allows users to live track flights in real-time, but it provides little to know historical data. Our application will incorporate similar elements as Flightview’s to create a working map, but we will attempt to implement prediction analysis as well. Essentially, our application will provide a comprehensive and easily accessible visualization tool that users can use to determine what airline they should choose in order to have the highest chance of avoiding delays. 

### Realness
For this project, we will be using the Kaggle dataset “2015 Flight Delays and [Cancellations](https://www.kaggle.com/datasets/usdot/flight-delays?select=flights.csv). Here is a description of the dataset: “The U.S. Department of Transportation's (DOT) Bureau of Transportation Statistics tracks the on-time performance of domestic flights operated by large air carriers. Summary information on the number of on-time, delayed, canceled, and diverted flights are published in DOT's monthly Air Travel Consumer Report and in this dataset of 2015 flight delays and cancellations.” Some of the names of the relevant columns we will be using for this project are airline, origin, destination, year, month, day of the week, and departure delay. As mentioned in the Functionality section below, users will be able to add entries that prompt the mandatory inputs date of delay/cancelation, airline, flight number, origin airport, destination airport, scheduled departure, and departure time in order to ensure that valid flights are added; However, this function will be limited to those who request clearance from the website implementers and new data will not be reflected unless it has been confirmed to be consistent with official records from the DOT in order to ensure credible data entry. 

### Functionality
* Users will be able to add, delete, and edit any raw data (We are using flight data from 2015, but as long as raw data is altered in the same format/columns, then our website should accurately reflect that. This allows our application to be generalized beyond solely 2015 data) They will be able to do this on a specific portion of the website where entries prompt mandatory inputs (date of delay/cancelation, airline, flight number, origin airport, destination airport, scheduled departure, and departure time).
* Users will be able to use keyword searching to easily access airport and airline rankings in both the map and tables and filtering of entries will allow users to quickly locate what they are looking for.
* Low-fidelity UI mockup(Website map):

<p align="center">
  <img src="https://github.com/cs411-alawini/sp23-cs411-team018-FinalProject/blob/main/Image/UI%20mock%20up.png" alt="Low-fidelity UI mockup(Website map)"/>
</p>



* Website tables (dummy numbers for demonstration): 

<p align="center">
  <img src="https://github.com/cs411-alawini/sp23-cs411-team018-FinalProject/blob/main/Image/Schema%20simulation.png" alt="Website tables"/>
</p>

Functionality List:
* Search and filter for flights from specific airlines, destinations, status (cancelled, on time, or delayed) to display on map
* Add or delete airline and flight entries in database
* Display all flight paths on a visual map that can be selectively viwed/toggled given the raw data (2015 data in this case)
* Generate correlation/prediction graphs for the probability of delays for each airline 
* Generate tables ranking airlines with least delays/cancellations to most


### Project work distribution
* **Backend:**
The backend portion of our project is expected to be divided into 4 main subcategories. 
  - The first would be in filtering flights based on their origin or destination airport by directly selecting and analyzing these columns of the raw data. [Sriya Mikkilineni](https://github.com/sriyamikki) will be primarily responsible for this task. 
  - The second task is to analyze flight delays and cancellations per airline requiring airline-specific filtering of the data. [Rushika Kumarswamy](https://github.com/rushikak2) will be primarily responsible for this task. 
  - The third task would be to generate statistics and new columns of data based on flights delayed per time of year. [Enya Sun](https://github.com/esun2cs) will be primarily responsible for this task. 
  - The fourth task would be to analyze the data per week to understand the trends of cancellations/delays per day of the week. [Chen Wang](https://github.com/ollill0823) will be primarily responsible for this task. 

* **Frontend:**
  - [Sriya Mikkilineni](https://github.com/sriyamikki) and [Enya Sun](https://github.com/esun2cs) will be responsible for the UI which includes designing the map visualization, color coding, and hover information display components. 
  - [Rushika Kumarswamy](https://github.com/rushikak2) and 
will be primarily responsible for working on integrating frontend and backend APIs to use derived information and connect it to what information to display. Possible addition (if extra time) of airlines ranking leaderboard and statistics relating to the amount of time delayed, which everyone will work on together.

* **(Additional Breakdown):**
All visualizations will be per origin or destination respectively
  - [Rushika Kumarswamy](https://github.com/rushikak2): (Airline Specific) Create a ranking of all airlines in terms of delays
  - [Chen Wang](https://github.com/ollill0823): (Time of the year) Generate statistics and new columns of data based on flights delayed per time of year
  - [Sriya Mikkilineni](https://github.com/sriyamikki): (day of the week) Generate statistics to display flights delayed based on the day of the week
  - [Enya Sun](https://github.com/esun2cs): Taking in user input and displaying relevant information. Ex: origin/destination/Airlines/Time of year


* **Data cleaning/compression note:**
	Since we will not be using entire dataset, we plan to randomly select roughly 850 rows from each month to ensure accurate representation of compressed data (we are mainly focusing on the frequency of delays per airline instead of per month). Everyone will work together to write a function for this task. 


