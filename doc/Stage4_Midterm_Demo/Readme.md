
# Stage4: Midterm Demo
------------------------------------------

### A. node.js:
<p align="center">
  <img src="https://github.com/cs411-alawini/sp23-cs411-team018-FinalProject/blob/main/doc/Stage4_Midterm_Demo/Image/Function_table.png" alt="Function-table"/>
</p>

``` js
var express = require('express');
var bodyParser = require('body-parser');
var mysql = require('mysql2');
var path = require('path');
var connection = mysql.createConnection({
                host: '34.133.251.39',
                user: 'root',
                password: 'test1234',
                database: 'CS411'
});

connection.connect;


var app = express();

// set up ejs view engine 
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'ejs');
 
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
app.use(express.static(__dirname + '../public'));

/* GET home page, respond by rendering index.ejs */
app.get('/', function(req, res) {
  res.render('index', { title: 'Mark Attendance' });
});


app.get('/modify', function(req, res) {
      res.send({'message': 'Successfully changed the table!'});
});




// this code is executed when a user clicks the form submit "Update" button//
app.post('/modify', function(req, res) {
  var action = req.body.Action;
  var first_table = req.body.first_table;
  var second_table = req.body.second_table;
  var third_table = req.body.third_table;
  var first_condition = req.body.first_condition;
  var second_condition = req.body.second_condition;
  var third_condition = req.body.third_condition;
  var fourth_condition = req.body.fourth_condition;
  var fifth_condition = req.body.fifth_condition;
  var sixth_condition = req.body.sixth_condition;
  var seventh_condition = req.body.seventh_condition;

  var first_column_name = req.body.first_column_name;
  var second_column_name = req.body.second_column_name;
  var third_column_name = req.body.third_column_name;
  var fourth_column_name = req.body.fourth_column_name;
  var fifth_column_name = req.body.fifth_column_name;
  var sixth_column_name = req.body.sixth_column_name;
  var seventh_column_name = req.body.seventh_column_name;





  var sql11 = `SELECT * FROM ${first_table}`;
  var sql12 = `SELECT * FROM ${first_table} WHERE ${first_column_name} = '${first_condition}'`;
  var sql13 = `SELECT * FROM ${first_table} WHERE ${first_column_name} = '${first_condition}' AND ${second_column_name} = '${second_condition}'`;
  var sql21 = `INSERT INTO ${first_table} (${first_column_name}, ${second_column_name}) VALUES ('${first_condition}','${second_condition}')`;
  var sql22 = `INSERT INTO ${first_table} (${first_column_name}, ${second_column_name}, ${third_column_name}, ${fourth_column_name}, ${fifth_column_name}, ${sixth_column_name}) VALUES ('${first_condition}','${second_condition}', '${third_condition}','${fourth_condition}', '${fifth_condition}','${sixth_condition}')`;
  var sql32 = `DELETE FROM ${first_table} WHERE ${first_column_name} = '${first_condition}' AND ${second_column_name} = '${second_condition}'`;
  var sql33 = `DELETE FROM ${first_table} WHERE ${first_column_name} = '${first_condition}' AND ${second_column_name} = '${second_condition}' AND ${third_column_name} = '${third_condition}'`;
  var sql41 = `UPDATE ${first_table} SET ${second_column_name} = '${second_condition}' WHERE ${first_column_name} = '${first_condition}'`;
  var sql42 = `UPDATE ${first_table} SET ${third_column_name} = '${third_condition}' WHERE ${first_column_name} = '${first_condition}' AND ${second_column_name} = '${second_condition}'`;
  var sql51 = `SELECT * FROM ${first_table} JOIN ${second_table} ON ${first_table}.${first_column_name} = ${second_table}.${second_column_name}`;
  var sql52 = `SELECT * FROM ${first_table} JOIN ${second_table} ON ${first_table}.${first_column_name} = ${second_table}.${second_column_name} WHERE ${first_table}.${third_column_name} = '${third_condition}'`;
  var sql53 = `SELECT * FROM ${first_table} JOIN ${second_table} ON ${first_table}.${first_column_name} = ${second_table}.${second_column_name} WHERE ${first_table}.${third_column_name} = '${third_condition}' AND ${first_table}.${fourth_column_name} = '${fourth_condition}'`;
  var sql61 = `SELECT  DISTINCT ${first_column_name}, ${second_column_name} FROM ${first_table} JOIN ${second_table} ON ${first_table}.${third_column_name} = ${second_table}.${fourth_column_name} WHERE ${fifth_column_name} IN (SELECT ${fifth_column_name} FROM ${third_table} WHERE '${sixth_condition}' <= ${sixth_column_name} and ${seventh_column_name} <= '${seventh_condition}')`;
  var sql62 = `SELECT ${first_column_name}, AVG(${second_column_name} + ${third_column_name}) FROM ${first_table} WHERE ${fourth_column_name} IN (SELECT ${fourth_column_name} FROM ${second_table} WHERE ${fifth_column_name} = '${fifth_condition}') GROUP BY ${first_column_name}`;
  


  function DoAction(action, first_table) {
  	let result;
  if (action == "Search_all") {
    result = sql11;
  } else if (action == "Search_1_where"){
    result = sql12;
  } else if (action == "Search_2_where"){
    result = sql13;
  } else if (action == 'Insert' && first_table == 'Company'){
    result = sql21;
  } else if (action == 'Insert' && first_table != 'Company'){
    result = sql22;
  } else if (action == "Remove_2_where"){
    result = sql32;
  } else if (action == "Remove_3_where"){
    result = sql33;
  } else if (action == "Update_1_where"){
    result = sql41;
  } else if (action == "Update_2_where"){
    result = sql42;
  } else if (action == "Join_no_where"){
    result = sql51;
  } else if (action == "Join_1_where"){
    result = sql52;
  } else if (action == "Join_2_where"){
    result = sql53;
  } else if (action == "Advanced_1"){
    result = sql61;
  } else if (action == "Advanced_2"){
    result = sql62;
  }
  return result;
 };


console.log(DoAction(action, first_table));
connection.connect(function(err) {
  if (err) throw err;
  connection.query(DoAction(action, first_table), function (err, result, fields) {
    if (err) throw err;

        console.log(result);
        if (action == "Search_all" || action == "Search_1_where" || action == "Search_2_where" || action == "Advanced_1" || action == "Advanced_2" ) {
         var table =''; //to store html table
         var result0 = result[0];
         var result_key = Object.keys(result0);


         //create html table with data from result//
         for(var i=0; i<result.length; i++){
          table +='<tr><td>'+ (i+1);
          for(var j=0; j<result_key.length; j++){
           table += '</td><td>'+ result[i][result_key[j]];
                }
          table += '</td></tr>';          
         }
         table2 ='<table border="1"><tr><th>Nr.';
         for(var z=0; z<result_key.length; z++){
          table2 +='</th><th>' +  result_key[z];
         }
         table2 +='</th></tr>'+ table +'</table>';
         res.send(table2);
        } else {
        res.redirect('/modify');
        };
    });
  });
});

app.listen(80, function () {
    console.log('Node app is running on port 80');
});


```


### B. html .ejs file:
<p align="center">
  <img src="https://github.com/cs411-alawini/sp23-cs411-team018-FinalProject/blob/main/doc/Stage4_Midterm_Demo/Image/Function_table.png" alt="Function-table"/>
</p>

``` bash
<!DOCTYPE html>
<html lang="en">
 <head>
   <title>Flights System</title>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1">
   <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css">
 </head>

 <body>
   <div class="container mt-4">
     <div class="card">
       <div class="card-body">


		<img src="https://i.im.ge/2023/04/09/ue67JL.png" alt="ue67JL.png" border="0">

	  <h4>SQL action:</h4>
       <form action="modify" method="POST">
       	<div class="form-group">
        
        <h5>Select an action(action + where query):</h5>
            <select name="Action">
            	<optgroup label="Insert">
                  <option value="Insert" selected="selected">Insert</option>
                <optgroup label="Update">
                  <option value="Update_1_where" selected="selected">Update_1_where</option>
                  <option value="Update_2_where" selected="selected">Update_2_where</option>
                <optgroup label="Remove">             
                  <option value="Remove_2_where" selected="selected">Remove_2_where</option>
                  <option value="Remove_3_where" selected="selected">Remove_3_where</option>
                <optgroup label="Search">
                  <option value="Search_all" selected="selected">Search_all</option>
                  <option value="Search_1_where" selected="selected">Search_1_where</option>
                  <option value="Search_2_where" selected="selected">Search_2_where</option>
                <optgroup label="Join">
                  <option value="Join_no_where" selected="selected">Join_no_where</option>
                  <option value="Join_1_where" selected="selected">Join_1_where</option>
                  <option value="Join_2_where" selected="selected">Join_2_where</option>
		    <optgroup label="Advanced">
                  <option value="Advanced_1" selected="selected">Advanced_1</option>
			<option value="Advanced_2" selected="selected">Advanced_2</option>

            </select>	</br></br>

            
            
      	<h5>Select a table(Table2 will be used in joined only):</h5>
            <select name="first_table">
            	<optgroup label="Table1">
                  <option value="Company" selected="selected">Company</option>
                  <option value="Airline_Reviews" selected="selected">Airline_Reviews</option>
                  <option value="Airplane_Record" selected="selected">Airplane_Record</option>
                  <option value="Airport" selected="selected">Airport</option>
                  <option value="Flight" selected="selected">Flight</option>
            </select>
            <select name="second_table">
            	<optgroup label="Table2">
                  <option value="Company" selected="selected">Company</option>
                  <option value="Airline_Reviews" selected="selected">Airline_Reviews</option>
                  <option value="Airplane_Record" selected="selected">Airplane_Record</option>
                  <option value="Airport" selected="selected">Airport</option>
                  <option value="Flight" selected="selected">Flight</option>
            </select>
		<select name="third_table">
            	<optgroup label="Table3">
                  <option value="Company" selected="selected">Company</option>
                  <option value="Airline_Reviews" selected="selected">Airline_Reviews</option>
                  <option value="Airplane_Record" selected="selected">Airplane_Record</option>
                  <option value="Airport" selected="selected">Airport</option>
                  <option value="Flight" selected="selected">Flight</option>
            </select>	</br></br>

            

            
		<h5>Select the '1st' column name(Rule: Where --> Update or remove):</h5>
            <select name="first_column_name">
              <optgroup label="Company">
              	<option value="IATA_Designator" selected="selected">IATA_Designator</option>
                <option value="AirlineName" selected="selected">AirlineName</option>
              </optgroup>
              <optgroup label="Airline_Reviews">
              	<option value="Review_ID" selected="selected">Review_ID</option>
                <option value="AirlineName" selected="selected">AirlineName</option>
                <option value="Overall" selected="selected">Overall</option>
                <option value="Author" selected="selected">Author</option>
                <option value="Review_date" selected="selected">Review_date</option>
                <option value="Aircraft" selected="selected">Aircraft</option>
                <option value="Traveller_type" selected="selected">Traveller_type</option>
                <option value="Cabin" selected="selected">Cabin</option>
                <option value="Route" selected="selected">Route</option>
                <option value="Date_flown" selected="selected">Date_flown</option>
                <option value="Seat_comfort" selected="selected">Seat_comfort</option>
                <option value="Cabin_service" selected="selected">Cabin_service</option>
                <option value="Food_bev" selected="selected">Food_bev</option>
                <option value="Entertainment" selected="selected">Entertainment</option>
                <option value="Ground_service" selected="selected">Ground_service</option>
                <option value="Value_for_money" selected="selected">Value_for_money</option>
                <option value="Recommended" selected="selected">Recommended</option>                      
             </optgroup>  
             <optgroup label="Airplane_Record">
             	<option value="IATA_Designator" selected="selected">IATA_Designator</option>
                </option><option value="FlightNumber" selected="selected">FlightNumber</option>
                <option value="Month" selected="selected">Month</option>
                <option value="Day" selected="selected">Day</option>
                <option value="DayOfWeek" selected="selected">DayOfWeek</option>
                <option value="TailNumber" selected="selected">TailNumber</option>
                <option value="Departure_Time" selected="selected">Departure_Time</option>
                <option value="Departure_Delay" selected="selected">Departure_Delay</option>
                <option value="Taxi_Out" selected="selected">Taxi_Out</option>
                <option value="Elapsed_Time" selected="selected">Elapsed_Time</option>
                <option value="Air_Time" selected="selected">Air_Time</option>
                <option value="Taxi_In" selected="selected">Taxi_In</option>
                <option value="Arrival_Time" selected="selected">Arrival_Time</option>
                <option value="Arrival_Delay" selected="selected">Arrival_Delay</option>                       
             </optgroup>  
             <optgroup label="Airport">
             	<option value="IATA_Code" selected="selected">IATA_Code</option>
                <option value="Airport" selected="selected">Airport</option>
                <option value="City" selected="selected">City</option>
                <option value="State" selected="selected">State</option>
                <option value="Latitude" selected="selected">Latitude</option>
                <option value="Longtitude" selected="selected">Longtitude</option>                             
             </optgroup>     
             <optgroup label="Flight">
             	<option value="IATA_Designator" selected="selected">IATA_Designator</option>  
                <option value="FlightNumber" selected="selected">FlightNumber</option>   
                <option value="Original_Airport" selected="selected">Original_Airport</option>  
                <option value="Destination_Airport" selected="selected">Destination_Airport</option>       
                <option value="Schedule_Departure" selected="selected">Schedule_Departure</option>       
                <option value="Scheduled_Time" selected="selected">Scheduled_Time</option>   
                <option value="Scheduled_Arrival" selected="selected">Scheduled_Arrival</option>   
                <option value="Distance" selected="selected">Distance</option>       
             </optgroup>                 
            </select>

				<label for="first_condition">Filled in the 1st condition for action:</label>
          		<input type="text" class="form-control col-lg-9" id="first_condition" aria-describedby="emailHelp" placeholder="Enter condition" name="first_condition"></br>
          
		<h5>Select the '2nd' column name(Rule: Where --> Update or remove):</h5>           
            <label for="second_column_name">Filled in the 2nd column name:</label>
            <input type="text" class="form-control col-lg-9" id="second_column_name" aria-describedby="emailHelp" placeholder="Enter column name" name="second_column_name">
            <label for="second_condition">Filled in the 2nd condition for action:</label>
            <input type="text" class="form-control col-lg-9" id="second_condition" aria-describedby="emailHelp" placeholder="Enter condition" name="second_condition"></br>          
            
		<h5>Select the '3rd' column name(Rule: Where --> Update or remove):</h5>           
            <label for="third_column_name">Filled in the 3rd column name:</label>
            <input type="text" class="form-control col-lg-9" id="third_column_name" aria-describedby="emailHelp" placeholder="Enter column name" name="third_column_name">
            <label for="third_condition">Filled in the 3rd condition for action:</label>
            <input type="text" class="form-control col-lg-9" id="third_condition" aria-describedby="emailHelp" placeholder="Enter condition" name="third_condition"></br>
            
            
		<h5>Select the '4th' column name(Rule: Where --> Update or remove):</h5>           
            <label for="fourth_column_name">Filled in the 4th column name:</label>
            <input type="text" class="form-control col-lg-9" id="fourth_column_name" aria-describedby="emailHelp" placeholder="Enter column name" name="fourth_column_name">
            <label for="fourth_condition">Filled in the 4th condition for action:</label>
            <input type="text" class="form-control col-lg-9" id="fourth_condition" aria-describedby="emailHelp" placeholder="Enter condition" name="fourth_condition"></br>
            
		<h5>Select the '5th' column name(Rule: Where --> Update or remove):</h5>           
            <label for="fifth_column_name">Filled in the 5th column name:</label>
            <input type="text" class="form-control col-lg-9" id="fifth_column_name" aria-describedby="emailHelp" placeholder="Enter column name" name="fifth_column_name">
            <label for="fifth_condition">Filled in the 5th condition for action:</label>
            <input type="text" class="form-control col-lg-9" id="fifth_condition" aria-describedby="emailHelp" placeholder="Enter condition" name="fifth_condition"></br>    
            
            
		<h5>Select the '6th' column name(Rule: Where --> Update or remove):</h5>           
            <label for="sixth_column_name">Filled in the 6th column name:</label>
            <input type="text" class="form-control col-lg-9" id="six_column_name" aria-describedby="emailHelp" placeholder="Enter column name" name="sixth_column_name">
            <label for="sixth_condition">Filled in the 6th condition for action:</label>
            <input type="text" class="form-control col-lg-9" id="sixth_condition" aria-describedby="emailHelp" placeholder="Enter condition" name="sixth_condition"></br>  
            
       <h5>Select the '7th' column name(Rule: Where --> Update or remove):</h5>           
            <label for="seventh_column_name">Filled in the 7th column name:</label>
            <input type="text" class="form-control col-lg-9" id="seventh_column_name" aria-describedby="emailHelp" placeholder="Enter column name" name="seventh_column_name">
            <label for="seventh_condition">Filled in the 7th condition for action:</label>
            <input type="text" class="form-control col-lg-9" id="seventh_condition" aria-describedby="emailHelp" placeholder="Enter condition" name="seventh_condition"></br>  
            
       </div>
       </div>
           <button type="submit" class="btn btn-primary">Submitt</button>
     </form></br></br>
   </div>
 </div>
 </body>
</html>



```


### C. Demo code:
#### 1. Insertion:
##### i. Company(2-parameters only):
``` sql
INSERT INTO Company (IATA_Designator, AirlineName) VALUES ('af','2')
``` 
it will automaticall execute as below function: 

`INSERT INTO ${first_table} (${first_column_name}, ${second_column_name}) VALUES ('${first_condition}','${second_condition}')`;


##### ii. Other Tables(2-parameters only):
``` sql
INSERT INTO Airplane_Record (IATA_Designator, FlightNumber, Month, Day, DayOfWeek, TailNumber) VALUES ('VX', 9999, 10, 10, 10, 9997);
``` 

``` 
Double check:
``` sql
SELECT * FROM Airplane_Record WHERE IATA_Designator = 'VX';
``` 

it will automaticall execute as below function: 

`INSERT INTO ${first_table} (${first_column_name}, ${second_column_name}, ${third_column_name}, ${fourth_column_name}, ${fifth_column_name}, ${sixth_column_name}) VALUES ('${first_condition}','${second_condition}', '${third_condition}','${fourth_condition}', '${fifth_condition}','${sixth_condition}')`;



#### 2. Update:
##### i. Update_1_where:
``` sql
UPDATE Company SET AirlineName = '1' WHERE IATA_Designator = 'ag';

``` 
Double check:
``` sql
SELECT * FROM Company;
``` 
it will automaticall execute as below function: 

`UPDATE ${first_table} SET ${second_column_name} = '${second_condition}' WHERE ${first_column_name} = '${first_condition}'`;



##### ii. Update_2_where:
``` sql
UPDATE Airplane_Record SET TailNumber = '9996' WHERE IATA_Designator = 'VX' AND TailNumber = '9997';
``` 

Double check:
``` sql
SELECT * FROM Airplane_Record WHERE IATA_Designator = 'VX';
``` 

it will automaticall execute as below function: 



#### 3. Remove:
##### i. Remove_2_where:
``` sql
DELETE FROM Company WHERE IATA_Designator = 'ag' AND AirlineName = '2';
``` 
Double check:
``` sql
SELECT * FROM Company;
``` 
it will automaticall execute as below function: 



##### ii. Remove_3_where:
``` sql
DELETE FROM Airplane_Record WHERE IATA_Designator = 'VX' AND FlightNumber = '9999' AND TailNumber = '9996';
``` 

Double check:
``` sql
SELECT * FROM Airplane_Record WHERE IATA_Designator = 'VX';
``` 
it will automaticall execute as below function: 



#### 3. Search:
##### i. Search_all:
``` sql
SELECT * FROM Company;
``` 
Double check:
``` sql
SELECT * FROM Company;
``` 

it will automaticall execute as below function: 



##### ii. Search_1_where:
``` sql
SELECT * FROM Company WHERE IATA_Designator = 'zc';
``` 
Double check:
``` sql
SELECT * FROM Company WHERE IATA_Designator = 'zc';
``` 
it will automaticall execute as below function: 



##### iii. Search_2_where:
``` sql
SELECT * FROM Airplane_Record WHERE IATA_Designator = 'VX';
``` 
Double check:
``` sql
SELECT * FROM Airplane_Record WHERE IATA_Designator = 'VX';
``` 
it will automaticall execute as below function: 


#### 4. Join:
##### i. Join_no_where:
``` sql
SELECT * FROM Company JOIN Airplane_Record ON Company.IATA_Designator = Airplane_Record.IATA_Designator;
``` 
Double check:
``` sql
SELECT * FROM Company JOIN Airplane_Record ON Company.IATA_Designator = Airplane_Record.IATA_Designator;
``` 
it will automaticall execute as below function: 



##### ii. Join_1_where:
``` sql
SELECT * FROM Company JOIN Airplane_Record ON Company.IATA_Designator = Airplane_Record.IATA_Designator WHERE Company.IATA_Designator = 'VX';
``` 
Double check:
``` sql
SELECT * FROM Company JOIN Airplane_Record ON Company.IATA_Designator = Airplane_Record.IATA_Designator WHERE Company.IATA_Designator = 'VX';
``` 
it will automaticall execute as below function: 


##### iii. Join_2_where:
``` sql
SELECT * FROM Airplane_Record JOIN Company ON Airplane_Record.IATA_Designator = Company.IATA_Designator WHERE Airplane_Record.IATA_Designator = 'VX' AND Airplane_Record.FlightNumber = '9999';
``` 
Double check:
``` sql
SELECT * FROM Airplane_Record JOIN Company ON Airplane_Record.IATA_Designator = Company.IATA_Designator WHERE Airplane_Record.IATA_Designator = 'VX' AND Airplane_Record.FlightNumber = '9999';
``` 
it will automaticall execute as below function: 



#### 5. Advanced:
##### i. Advanced_1:
``` sql
SELECT  DISTINCT FlightNumber, City FROM Flight JOIN Airport ON Flight.Original_Airport = Airport.IATA_Code WHERE FlightNumber IN (SELECT FlightNumber FROM Airplane_Record WHERE '1' <= Month and Month <= '3')
``` 
Double check:
``` sql
SELECT  DISTINCT FlightNumber, City FROM Flight JOIN Airport ON Flight.Original_Airport = Airport.IATA_Code WHERE FlightNumber IN (SELECT FlightNumber FROM Airplane_Record WHERE '1' <= Month and Month <= '3')
``` 
it will automaticall execute as below function: 



##### ii. Advanced_2:
``` sql
SELECT IATA_Designator, AVG(Departure_Delay + Arrival_Delay) FROM Airplane_Record WHERE DayOfWeek IN (SELECT DayofWeek FROM Airplane_Record WHERE DayOfWeek = 4) GROUP BY IATA_Designator;
``` 
Double check:
``` sql
SELECT IATA_Designator, AVG(Departure_Delay + Arrival_Delay) FROM Airplane_Record WHERE DayOfWeek IN (SELECT DayofWeek FROM Airplane_Record WHERE DayOfWeek = 4) GROUP BY IATA_Designator;
``` 

it will automaticall execute as below function: 

