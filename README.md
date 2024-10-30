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
