# Aviation Analytics: Exploring Relationships Between Aircraft, Flights, and Passenger Data
## Project Description: Data Analysis of Airline Operations
## Objective
The primary objective of this project is to analyze various aspects of airline operations using the provided relational database. This analysis aims to uncover insights regarding aircraft performance, flight schedules, passenger bookings, and revenue generation.
## Table of Contents
- [Data Overview](#DataOverview)
- [Analysis Goals](#AnalysisGoals)
- [Methodology](#Methodology)
- [License](#license)

## Data Overview
The database consists of eight interconnected tables, each holding vital information about the airline's operations. Here’s a brief overview of each table:

1) Aircrafts_data: Contains details about each aircraft in the fleet, including the aircraft code, model, and operational range.

2) Airports_data: Provides information about airports, including airport codes, names, cities, geographical coordinates, and time zones.

3) Boarding_passes: Holds records of boarding passes issued, linking ticket numbers with flight IDs, boarding numbers, and seat numbers.

4) Bookings: Captures booking information, including the booking reference, date, and total amount paid.

5) Flights: Details flight operations, including flight IDs, flight numbers, scheduled and actual departure/arrival times, departure airports, flight status, and associated aircraft.

6) Seats: Lists the seating arrangements on each aircraft, including seat numbers and fare conditions.

7) Ticket_flights: Connects tickets to flights, detailing fare conditions and amounts charged for each ticket.

8) Tickets: Contains information about each ticket, linking ticket numbers to booking references and passenger IDs.


![Alt text](https://github.com/Slndora/Aviation-Analytics/blob/main/Screenshot%202024-10-28%20122218.png)

## Analysis Goals
1) Flight Performance Analysis:
- Assess the on-time performance of flights by comparing scheduled and actual departure/arrival times.
- Identify patterns in delays and cancellations.
2) Revenue Analysis:
- Analyze total revenue generated from bookings and ticket sales.
- Investigate the impact of different fare conditions on overall revenue.
3) Passenger Behavior:
- Examine booking trends, including peak booking periods and average booking amounts.
- Identify the most popular routes based on ticket sales.
4) Aircraft Utilization:
- Evaluate the operational efficiency of different aircraft models by analyzing flight assignments and range capabilities.
- Assess the distribution of seat types and fare conditions to optimize capacity.
5) Airport Performance:
- Analyze flight traffic at various airports to determine busy and underutilized locations.
- Explore the relationship between airport characteristics (such as timezone and geographical location) and flight performance.

## Methodology
- Data Cleaning & Preparation: Ensure data integrity and consistency across all tables.
- Descriptive Analysis: Generate summary statistics and visualizations to identify trends.
- Inferential Analysis: Apply statistical methods to test hypotheses and draw conclusions.
- Data Visualization: Utilize tools like Power BI to create interactive dashboards.
 
## Technologies Used
- For the development and management of the relational database, SQL (Structured Query Language) was utilized for data manipulation, querying, and maintaining the integrity of the database. SQL enabled efficient retrieval and management of data across multiple tables, facilitating complex queries to derive meaningful insights from the data set.
- In addition, Power BI was employed as a powerful business analytics tool to visualize and analyze the data. With Power BI, data from the relational database can be transformed into interactive reports and dashboards, allowing for real-time insights into various metrics related to flights, bookings, and aircraft.
- This combination of SQL for data management and Power BI for visualization provides a robust framework for effective data analysis and decision-making.

## Importing the data
I successfully downloaded a relational database from Kaggle in SQLite format and converted it into CSV files for compatibility. Following the conversion, I imported the CSV files into MySQL Workbench, ensuring a seamless transition of the data. This process involved verifying data integrity and structure to facilitate efficient querying and analysis within the MySQL environment. The migration enhances the accessibility and usability of the data for further project development and insights.
``` 
create table flights (
flight_id int, flight_no varchar(30), scheduled_departure varchar(30), scheduled_arrival varchar(30), departure_airport varchar(20),
arrival_airport	varchar(20), status varchar(20), aircraft_code varchar(20), actual_departure varchar(30), actual_arrival varchar(30));
LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/flights.csv'
INTO TABLE flights
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;

create table tickets ( ticket_no varchar(50), book_ref varchar(20),	passenger_id varchar(20));
LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/tickets.csv'
INTO TABLE tickets
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;

create table airports_data (airport_code varchar(10), airport_name varchar(100), city varchar(100),	coordinates varchar(100), timezone varchar(50));
LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/airports_data.csv'
INTO TABLE airports_data
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;

create table boarding_passes (ticket_no varchar(50), flight_id int,	boarding_no int, seat_no varchar(10));
LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/boarding_passes.csv'
INTO TABLE boarding_passes
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;

create table bookings (book_ref	varchar(50), book_date varchar(50),	total_amount int);
LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/bookings.csv'
INTO TABLE bookings
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;

create table aircrafts_data (aircraft_code varchar(10),	model varchar(100),	`range` int);
LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/aircrafts_data.csv'
INTO TABLE aircrafts_data
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;

create table seats (aircraft_code varchar(10),	seat_no varchar(10),	fare_conditions varchar(10));
LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/seats.csv'
INTO TABLE seats
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;

create table ticket_flights (ticket_no varchar(50),flight_id int, fare_conditions varchar(10), amount int);
LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/ticket_flights.csv'
INTO TABLE ticket_flights
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;
```
## Data cleaning
The data cleaning process involved several essential steps to ensure data integrity and usability. Duplicate entries were removed, missing values were addressed, and data types were corrected for accurate representation. Formats were standardized for consistency, outliers were treated as necessary, and overall data integrity was validated. I am pleased to report that there are no significant issues with the data, aside from the missing values in flights table, which have been effectively managed.
```
delete from flights
where flight_id is null or
flight_no is null or
scheduled_departure is null or
scheduled_arrival is null or
departure_airport is null or
arrival_airport is null or
status is null or
aircraft_code is null or
actual_departure is null or
actual_arrival is null;
```
## Data manipulation
I updated columns across two distinct tables, transitioning their data types from text to date (Date and time). This change enhances data integrity and optimizes query performance by ensuring that the columns are now better suited for time-series analysis and event tracking. The adjustment not only improves data consistency but also facilitates more efficient data retrieval and processing, aligning with best practices in database management.
```
UPDATE flights
SET scheduled_departure = STR_TO_DATE(scheduled_departure, '%Y-%m-%d %H:%i:%s+03');
update flights
set scheduled_arrival = str_to_date(scheduled_arrival, '%Y-%m-%d %H:%i:%s+03');
UPDATE flights
SET actual_departure = STR_TO_DATE(actual_departure, '%Y-%m-%d %H:%i:%s+03');
UPDATE flights
SET actual_arrival = STR_TO_DATE(actual_arrival, '%Y-%m-%d %H:%i:%s+03');


update bookings
set book_date = str_to_date(book_date, '%Y-%m-%d %H:%i:%s+03');
```





