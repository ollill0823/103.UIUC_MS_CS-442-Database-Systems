# Final project: Analyzing Flight Delays and Cancellations in the USA


## This file includes:

### Data file:
- [Flight Delays and Cancellations in the USA](https://drive.google.com/drive/folders/11ZzNzQQLywrrOj0_A4Rksx0I5l-8rBPW?usp=sharing) Raw data from [Kaggle](https://www.kaggle.com/datasets/usdot/flight-delays)
- The data we will be using consist of flight delays and cancellations from 2015 published by the DOT's Bureau of Transportation Statistics. We will extract IATA_code, airport, city, state, departure delay, and dates from the three CSV files of flight information. We plan on utilizing geographical data (airport, city, state, etc) to aid in the construction of our map, and other statistics (such as departure time, weather delays, cancelations, etc) to create our own tables, rankings, and predictions.

### SQL
- [Code here](https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/tree/main/doc/Stage3_Database_Implementatio_and_Indexing)

### Introduction
- Flight delays and cancellations are inevitable, and there are a variety of causes for them. They are all conditional, but only through the visualization of large amounts of data are trends identifiable. There is currently no easy or consistent way for people to predict if their flight will be delayed or not, and our application aims to address this. Our website will consist mainly of a map and a few tables/charts that present patterns in raw data that are otherwise uninterpretable to users without highly specific tools and knowledge. We aim to make flight data accessible and comprehensive by modeling it in an intuitive manner (seeing physical lines representing flights and symbols representing airports) while ensuring credible data sourcing (new data must be consistent with DOT’s reports in order to be appended). We can therefore analyze which airport exhibits frequent late departures through correlations and potentially suggest airline companies improve the accuracy of their departure times.


### Empirical results:
  **Stage1 Project Proposal:** [Stage1](https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/tree/main/doc/Stage1_Project_Proposal)
  
  **Stage2 Conceptual and Logical Database Design:** [Stage2](https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/tree/main/doc/Stage2_Conceptual_and_Logical_Database_Design)
  
  - Using draw.io for visual design, create a URL version diagram, disclose an ER-diagram, and provide the corresponding SQL command.
  
  **Stage3 Database Implementation and Indexing:** [Stage3](https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/tree/main/doc/Stage3_Database_Implementatio_and_Indexing)

  - Implementing raw data and its corresponding SQL schema into the Google Cloud platform system, followed by code execution to test functionality and usefulness.
  
  **Stage4 Midterm Demo:** [Stage4](https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/tree/main/doc/Stage4_Midterm_Demo)
  
  - Utilizing Neo4j to create a question-and-answer HTML page, along with the design of engaging and interesting questions.
  
  **Stage5 Final Demo:** [Stage5](https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/tree/main/doc/Stage5_Final%20Demo_%20Putting%20everything%20together)

  - Testing all functions and incorporating diversity into the HTML page.
  
  **Stage6 roject Report, demo, and discussion:** [Stage6](https://github.com/ollill0823/103.UIUC_MS_CS-442-Database-Systems/tree/main/doc/Stage6_Project%20Report%20and%20Demo%20Video)

  - Comprehensive project recap, detailing encountered technical challenges, strategies for overcoming them, suggestions for improvement in future steps, and personal reflection.

### References:
- [2015 Flight Delays and Cancellations Kaggle](https://www.kaggle.com/datasets/usdot/flight-delays)
