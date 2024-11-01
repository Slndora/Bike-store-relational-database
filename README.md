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


![Alt text](https://github.com/Slndora/Aviation-Analytics/blob/19ae7cf9165416778eff4f09de1ea203252650fe/Screenshot%202024-10-28%20122218.png)

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
## SQL for Data Insights

### 1) Number of seats available per aircraft model
```
SELECT AD.model, COUNT(S.seat_no) AS available_seats 
FROM Aircrafts_data AD 
JOIN Seats S ON AD.aircraft_code = S.aircraft_code 
GROUP BY AD.model 
ORDER BY available_seats DESC ;
```
![alt text](https://github.com/Slndora/Aviation-Analytics/blob/19ae7cf9165416778eff4f09de1ea203252650fe/Screenshot%202024-10-26%20225959.png)

### 2) List of the top 10 flights ranked by total tickets sold.
```
SELECT F.flight_id, COUNT(T.ticket_no) AS total_tickets 
FROM Flights F 
JOIN Ticket_flights TF ON F.flight_id = TF.flight_id 
JOIN Tickets T ON TF.ticket_no = T.ticket_no 
GROUP BY F.flight_id
order by total_tickets desc
limit 10 ;
```
![alt text](https://github.com/Slndora/Aviation-Analytics/blob/19ae7cf9165416778eff4f09de1ea203252650fe/Screenshot%202024-10-26%20230828.png)

### 3) List of top 20 flights ranked by income generated.
```
SELECT F.flight_id, F.flight_no, SUM(TF.amount) AS total_income 
FROM Flights F 
JOIN Ticket_flights TF ON F.flight_id = TF.flight_id 
JOIN Tickets T ON TF.ticket_no = T.ticket_no 
JOIN Bookings B ON T.book_ref = B.book_ref 
GROUP BY F.flight_id, F.flight_no
ORDER BY total_income DESC
limit 20;
```
![alt text](https://github.com/Slndora/Aviation-Analytics/blob/19ae7cf9165416778eff4f09de1ea203252650fe/Screenshot%202024-10-26%20231238.png)

### 4)  Analyze booking trends by month and calculate the average ticket price for each month across all bookings.
```
SELECT DATE_FORMAT(b.book_date, '%Y-%m') AS booking_month, 
       COUNT(t.Ticket_no) AS total_tickets, 
       AVG(tf.amount) AS avg_ticket_price 
FROM Bookings b 
JOIN Tickets t ON b.Book_ref = t.book_ref 
JOIN Ticket_flights tf ON t.Ticket_no = tf.Ticket_no 
GROUP BY booking_month 
ORDER BY booking_month;
```
![alt text](https://github.com/Slndora/Aviation-Analytics/blob/19ae7cf9165416778eff4f09de1ea203252650fe/Screenshot%202024-10-27%20103915.png)

### 5) Generate a report of passengers ranked by the total amounts spent and the number of flights taken.
```
SELECT t.passenger_id, 
       COUNT(DISTINCT tf.flight_id) AS flights_taken, 
       SUM(tf.amount) AS total_spent 
FROM Tickets t 
JOIN Ticket_flights tf ON t.Ticket_no = tf.Ticket_no 
GROUP BY t.passenger_id 
ORDER BY total_spent DESC;
```
![alt text](https://github.com/Slndora/Aviation-Analytics/blob/19ae7cf9165416778eff4f09de1ea203252650fe/Screenshot%202024-10-27%20104418.png)

### 6) Identify the most popular routes based on the number of flights and total tickets sold for each route.
```
SELECT f.departure_airport, f.arrival_airport, 
       COUNT(f.Flight_id) AS total_flights, 
       SUM(CASE WHEN bp.boarding_no IS NOT NULL THEN 1 ELSE 0 END) AS total_tickets 
FROM Flights f 
LEFT JOIN Boarding_passes bp ON f.Flight_id = bp.flight_id 
GROUP BY f.departure_airport, f.arrival_airport 
ORDER BY total_tickets DESC;
```
![alt text](https://github.com/Slndora/Aviation-Analytics/blob/19ae7cf9165416778eff4f09de1ea203252650fe/Screenshot%202024-10-27%20104447.png)

### 7) Analyze the relationship between aircraft range and ticket sales to see if longer-range flights yield more sales.
```
SELECT ad.range, COUNT(tf.Ticket_no) AS total_sales, AVG(tf.amount) AS avg_ticket_price 
FROM Aircrafts_data ad 
JOIN Flights f ON ad.aircraft_code = f.aircraft_code 
JOIN Ticket_flights tf ON f.Flight_id = tf.flight_id 
GROUP BY ad.range 
ORDER BY ad.range;
```
![alt text](https://github.com/Slndora/Aviation-Analytics/blob/19ae7cf9165416778eff4f09de1ea203252650fe/Screenshot%202024-10-27%20104530.png)

### 8) Assess the impact of booking date on ticket sales, comparing early versus last-minute bookings.
```
SELECT CASE 
           WHEN DATEDIFF(f.scheduled_departure, b.book_date) > 30 THEN 'Early' 
           ELSE 'Last Minute' 
       END AS booking_type, 
       COUNT(t.Ticket_no) AS total_tickets, 
       AVG(tf.amount) AS avg_amount 
FROM Bookings b 
JOIN Tickets t ON b.Book_ref = t.book_ref 
JOIN Ticket_flights tf ON t.Ticket_no = tf.Ticket_no 
JOIN Flights f ON tf.flight_id = f.Flight_id 
GROUP BY booking_type;
```
![alt texxt](https://github.com/Slndora/Aviation-Analytics/blob/19ae7cf9165416778eff4f09de1ea203252650fe/Screenshot%202024-10-27%20105149.png)

### 9) Investigate flight delays by correlating scheduled and actual departure times, along with the number of affected passengers.
```
SELECT f.flight_no, 
       COUNT(bp.boarding_no) AS affected_passengers, 
       AVG(TIMESTAMPDIFF(MINUTE, f.scheduled_departure, f.actual_departure)) AS avg_delay 
FROM Flights f 
LEFT JOIN Boarding_passes bp ON f.Flight_id = bp.flight_id 
WHERE f.actual_departure IS NOT NULL AND f.scheduled_departure < f.actual_departure 
GROUP BY f.flight_no 
ORDER BY affected_passengers DESC;
```
![alt text](https://github.com/Slndora/Aviation-Analytics/blob/19ae7cf9165416778eff4f09de1ea203252650fe/Screenshot%202024-10-27%20105827.png)

### 10) Generate a comprehensive report analyzing the performance of each airport based on bookings, flights, ranked by revenue.
```
SELECT a.airport_name, 
       COUNT(DISTINCT f.flight_id) AS total_flights, 
       COUNT(b.book_ref) AS total_bookings,
       SUM(b.total_amount) AS total_revenue
FROM Airports_data a
LEFT JOIN Flights f ON a.airport_code = f.departure_airport
LEFT JOIN Ticket_flights tf ON f.flight_id = tf.flight_id
LEFT JOIN Tickets t ON tf.ticket_no = t.ticket_no
LEFT JOIN Bookings b ON t.book_ref = b.book_ref
GROUP BY a.airport_name
ORDER BY total_revenue DESC;
```
![alt text](https://github.com/Slndora/Aviation-Analytics/blob/19ae7cf9165416778eff4f09de1ea203252650fe/Screenshot%202024-10-27%20110237.png)

### 11) Investigate the correlation between booking amounts and flight delays across all flights.
```
SELECT f.flight_no, 
       SUM(b.total_amount) AS total_booking_amount, 
       (TIMESTAMPDIFF(MINUTE, f.scheduled_departure, f.actual_departure)) AS delay_minutes 
FROM Flights f 
JOIN Ticket_flights tf ON f.flight_id = tf.flight_id 
JOIN Tickets t ON tf.ticket_no = t.ticket_no 
JOIN Bookings b ON t.book_ref = b.book_ref 
WHERE f.actual_departure IS NOT NULL 
GROUP BY f.flight_no, f.scheduled_departure, f.actual_departure 
HAVING delay_minutes IS NOT NULL
order by delay_minutes desc
LIMIT 0, 50000;
```
![alt text](https://github.com/Slndora/Aviation-Analytics/blob/19ae7cf9165416778eff4f09de1ea203252650fe/Screenshot%202024-10-27%20111006.png)

### 12) Passenger Behavior Analysis.
```
WITH PassengerStats AS (
    SELECT 
        t.passenger_id,
        COUNT(t.ticket_no) AS booking_count,
        SUM(tf.amount) AS total_spent,
        AVG(tf.amount) AS avg_ticket_price
    FROM 
        Tickets t
    JOIN 
        Ticket_flights tf ON t.ticket_no = tf.ticket_no
    GROUP BY 
        t.passenger_id
)
SELECT 
    passenger_id,
    booking_count,
    total_spent,
    avg_ticket_price,
    dense_rank() OVER (ORDER BY total_spent DESC) AS spending_rank
FROM 
    PassengerStats
ORDER BY 
    spending_rank;
```
![alt text](https://github.com/Slndora/Aviation-Analytics/blob/19ae7cf9165416778eff4f09de1ea203252650fe/Screenshot%202024-10-27%20152222.png)

### 13) A stored procedure to dynamically adjust ticket prices based on real-time demand and seat availability.
```
DELIMITER //
CREATE PROCEDURE AdjustTicketPrices(IN flightId INT)
BEGIN
    DECLARE totalSeats INT;
    DECLARE bookedSeats INT;
    DECLARE occupancyRate DECIMAL(5,2);
    
    SELECT COUNT(*) INTO totalSeats 
    FROM Seats 
    WHERE Aircraft_code = (SELECT aircraft_code FROM Flights WHERE flight_id = flightId);
    
    SELECT COUNT(*) INTO bookedSeats 
    FROM Boarding_passes 
    WHERE flight_id = flightId;

    SET occupancyRate = (bookedSeats / totalSeats) * 100;

    IF occupancyRate > 80 THEN
        UPDATE Ticket_flights 
        SET fare_conditions = 'High Demand' 
        WHERE flight_id = flightId;
    ELSEIF occupancyRate < 50 THEN
        UPDATE Ticket_flights 
        SET fare_conditions = 'Discount' 
        WHERE flight_id = flightId;
    END IF;
END //
DELIMITER ;
```

## Insights generated with SQL Queries

### 1) Number of seats available per aircraft model
- Capacity Planning: Airlines can determine how many passengers they can accommodate on specific routes based on aircraft capacity.
- Scheduling: Helps in scheduling flights by matching aircraft with expected passenger loads.
- Fleet Management: Assists in making decisions about fleet composition and optimization.
- Revenue Management: Aids in pricing strategies by understanding potential capacity and demand.
- Operational Efficiency: Allows airlines to assess and optimize the utilization of their fleet.

### 2) List of the top 10 flights ranked by total tickets sold.
- Sales Performance Analysis: Identifies which flights are performing well, helping airlines understand market demand.
- Revenue Management: Assists in optimizing pricing strategies based on high-demand flights.
- Route Optimization: Provides insights into which routes might need additional capacity or more frequent service.
- Marketing Strategies: Helps in targeting promotions and advertising efforts to boost sales on less popular flights.
- Operational Planning: Informs decisions on staffing, aircraft allocation, and scheduling based on passenger demand.
- Competitor Benchmarking: Allows airlines to compare their performance with competitors on specific routes.

### 3) List of top 20 flights ranked by income generated.
- Revenue Analysis: Helps airlines understand which flights are the most profitable, guiding financial decisions.
- Resource Allocation: Informs decisions on where to allocate resources, such as aircraft and crew, based on profitability.
- Pricing Strategies: Assists in developing dynamic pricing models by analyzing which flights yield the highest income.
- Route Development: Identifies potential for expanding or increasing service on profitable routes.
- Performance Benchmarking: Enables comparison of flight performance across different routes and seasons.
- Financial Forecasting: Aids in projecting future income based on historical performance of the top flights.

### 4)  Analyze booking trends by month and calculate the average ticket price for each month across all bookings.
- Trend Analysis: Helps airlines understand seasonal variations in bookings, identifying peak travel times and slower months.
- Pricing Strategy: Aids in setting competitive pricing by observing how average ticket prices fluctuate throughout the year.
- Revenue Forecasting: Allows airlines to predict future revenue based on historical booking patterns and pricing trends.
- Marketing Campaigns: Informs targeted marketing strategies during peak times or slower months to boost sales.
- Capacity Planning: Helps in adjusting flight schedules and capacities according to expected demand based on monthly trends.
- Customer Insights: Provides insights into customer behavior and preferences, potentially leading to improved service offerings.

### 5) Generate a report of passengers ranked by the total amounts spent and the number of flights taken.
- Customer Segmentation: Identifies high-value customers, allowing for targeted marketing and personalized offers.
- Loyalty Programs: Helps in designing or enhancing loyalty programs based on passenger spending and travel frequency.
- Revenue Optimization: Assists in understanding which customers contribute most to revenue, guiding pricing strategies.
- Service Improvement: Provides insights into frequent travelers' preferences, enabling airlines to enhance services and amenities.
- Performance Tracking: Allows airlines to monitor passenger spending trends over time, assessing the effectiveness of marketing campaigns.
- Business Strategy: Informs broader business decisions, such as partnerships, promotions, or changes to service offerings.

### 6) Identify the most popular routes based on the number of flights and total tickets sold for each route.
- Route Performance Analysis: Helps airlines assess which routes are most in demand, guiding operational decisions.
- Capacity Management: Informs decisions on whether to increase or decrease flight frequency on specific routes.
- Market Demand Understanding: Provides insights into customer preferences and travel patterns.
- Revenue Optimization: Aids in identifying routes that generate the most revenue, which can influence pricing strategies.
- Strategic Planning: Assists in evaluating potential new routes or expanding existing ones based on proven demand.
- Competitor Benchmarking: Allows for comparison of route performance against competitors, informing competitive strategies.

### 7) Analyze the relationship between aircraft range and ticket sales to see if longer-range flights yield more sales.
- Market Insights: Helps airlines understand if longer-range flights attract more customers, which can inform route planning.
- Capacity and Fleet Planning: Informs decisions about acquiring new aircraft or adjusting routes based on performance related to range.
- Revenue Management: Assists in evaluating whether to focus on long-haul versus short-haul routes based on ticket sales performance.
- Pricing Strategy: Provides insights into how range affects pricing strategies and ticket sales, allowing for optimized pricing models.
- Customer Preferences: Helps identify customer preferences for longer versus shorter flights, potentially guiding marketing efforts.
- Operational Efficiency: Can inform operational decisions about scheduling and resource allocation based on performance data.

### 8) Assess the impact of booking date on ticket sales, comparing early versus last-minute bookings.
- Pricing Strategy: Helps airlines understand how booking timing affects sales, informing dynamic pricing strategies.
- Revenue Forecasting: Provides insights into potential revenue based on booking patterns, aiding in financial planning.
- Marketing Campaigns: Informs targeted marketing efforts to encourage early bookings or last-minute deals.
- Capacity Management: Assists in planning flight capacities and adjusting schedules based on expected booking behavior.
- Customer Behavior Analysis: Reveals patterns in customer booking preferences, which can guide service offerings and promotions.
- Operational Efficiency: Helps airlines optimize operations by understanding demand fluctuations based on booking timing.

### 9) Investigate flight delays by correlating scheduled and actual departure times, along with the number of affected passengers.
- Operational Efficiency: Identifies patterns in delays, helping airlines improve scheduling and reduce future delays.
- Customer Service Improvement: Assists in understanding the impact of delays on passengers, guiding better communication and service recovery strategies.
- Performance Metrics: Provides key performance indicators for on-time performance, which can be used for reporting and benchmarking.
- Resource Allocation: Helps in optimizing gate assignments and crew scheduling based on delay patterns.
- Regulatory Compliance: Aids in ensuring compliance with industry regulations regarding delays and passenger rights.
- Strategic Planning: Informs decisions on route adjustments or operational changes to minimize delays in the future.



















