# Zuber Ride Analysis

The purpose of this project was to use SQL to explore ride data and identify patterns in taxi company activity, customer preferences, and the effect of weather on ride durations in Chicago.

## Table of Contents

- [Zuber Ride Analysis](#zuber-ride-analysis)
  - [Data](#data)
  - [Description](#description)
  - [Assumptions](#assumptions)
  - [Process](#process)
  - [Findings](#findings)
  - [SQL Queries](#sql-queries)
    - [Query 1: Rides per Taxi Company (Nov 15–16)](#query-1-rides-per-taxi-company-nov-15–16)
    - [Query 2: Rides for Companies with "Yellow" or "Blue" (Nov 1–7)](#query-2-rides-for-companies-with-yellow-or-blue-nov-1–7)
    - [Query 3: Categorized Ride Counts (Nov 1–7)](#query-3-categorized-ride-counts-nov-1–7)
    - [Query 4: Retrieve Loop and O’Hare IDs](#query-4-retrieve-loop-and-ohare-ids)
    - [Query 5: Classify Weather Conditions](#query-5-classify-weather-conditions)
    - [Query 6: Ride Durations with Weather (Loop → O’Hare)](#query-6-ride-durations-with-weather-loop--ohare)

## Data

* 'neighborhoods' table: data on city neighborhoods
	* 'name': name of the neighborhood
	* 'neighborhood_id': neighborhood code
* 'cabs' table: data on taxis
	* 'cab_id': vehicle code
	* 'vehicle_id': the vehicle's technical ID
	* 'company_name': the company that owns the vehicle
* 'trips' table: data on rides
	* 'trip_id': ride code
	* 'cab_id': code of the vehicle operating the ride
	* 'start_ts': date and time of the beginning of the ride (time rounded to the hour)
	* 'end_ts': date and time of the end of the ride (time rounded to the hour)
	* 'duration_seconds': ride duration in seconds
	* 'distance_miles': ride distance in miles
	* 'pickup_location_id': pickup neighborhood code
	* 'dropoff_location_id': dropoff neighborhood code
* 'weather_records' table: data on weather
	* 'record_id': weather record code
	* 'ts': record date and time (time rounded to the hour)
	* 'temperature': temperature when the record was taken
	* 'description': brief description of weather conditions, e.g. "light rain" or "scattered clouds"

## Description

This project consists of multiple SQL queries that perform exploratory data analysis and evaluate the impact of weather conditions on ride durations between the Loop and O’Hare neighborhoods.

## Assumptions

* There is no direct relationship between the **trips** and **weather_records** tables; they are joined using **start_ts** and **ts**
* **neighborhood_id** is the primary key in the **neighborhoods** table
* **trip_id**, **cab_id**, and **record_id** are unique in their respective tables

## Process

1. Counted total rides for each taxi company during November 15–16, 2017
2. Filtered and grouped rides for companies with "Yellow" or "Blue" in their name for November 1–7, 2017
3. Categorized rides into "Flash Cab," "Taxi Affiliation Services," and "Other" and counted rides per group
4. Retrieved the **neighborhood_id** values for Loop and O'Hare
5. Used **CASE** to classify weather descriptions as “Good” or “Bad”
6. Analyzed Saturday rides from Loop (pickup_id 50) to O’Hare (dropoff_id 63), including duration and weather condition

## Findings

* Flash Cab had the most rides on November 15–16, with *19,558 rides*
* On November 1–7:
	* **Blue Diamond** had 6,764 rides
	* **Blue Ribbon Taxi Association Inc.** had 17,675 rides
	* **Taxi Affiliation Service Yellow** had 29,213 rides
	* **Yellow Cab** had 22,658 rides
* For November 1–7 overall:
	* **Flash Cab** had 64,084 rides
	* **Taxi Affiliation Services** had 37,583 rides
	* All other companies combined had 335,771 rides
* **Loop** neighborhood ID: 50
* **O’Hare** neighborhood ID: 63
* Weather was classified using keywords; for example, descriptions with “rain” or “storm” were labeled as **Bad**, others as **Good**
* The ride durations from Loop to O'Hare on Saturdays under **Good** weather conditions ranged from **1,380** to **2,410** seconds

# SQL Queries

1. Print the company_name field. Find the number of taxi rides for each taxi company for November 15-16, 2017, name the resulting field trips_amount and print it, too. Sort the results by the trips_amount field in descending order.

![Query 1](SQL_1.png)

2. Find the number of rides for every taxi companies whose name contains the words "Yellow" or "Blue" for November 1-7, 2017. Name the resulting variable trips_amount. Group the results by the company_name field.

![Query 2](SQL_2.png)

3. For November 1-7, 2017, the most popular taxi companies were Flash Cab and Taxi Affiliation Services. Find the number of rides for these two companies and name the resulting variable trips_amount. Join the rides for all other companies in the group "Other." Group the data by taxi company names. Name the field with taxi company names company. Sort the result in descending order by trips_amount.

![Query 3](SQL_3.png)

4. Retrieve the identifiers of the O'Hare and Loop neighborhoods from the neighborhoods table.

![Query 4](SQL_4.png)

5. For each hour, retrieve the weather condition records from the weather_records table. Using the CASE operator, break all hours into two groups: Bad if the description field contains the words rain or storm, and Good for others. Name the resulting field weather_conditions. The final table must include two fields: date and hour (ts) and weather_conditions. (both good & bad scrrenshots)

![Query 5](SQL_5.png)

![Query 6](SQL_6.png)

6. Retrieve from the **trips** table all the rides that started in the Loop (*pickup_location_id*: 50) on a Saturday and ended at O'Hare (*dropoff_location_id*: 63). Get the weather conditions for each ride. Use the method you applied in the previous task. Also, retrieve the duration of each ride. Ignore rides for which data on weather conditions is not available.
The table columns should be in the following order:

*start_ts*
*weather_conditions*
*duration_seconds*

Sort by *trip_id*.

![Query 7](SQL_7.png)
