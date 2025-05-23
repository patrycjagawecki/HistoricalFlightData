 # **Historical Flight Data Warehouse**
Patrycja Gawecki

## **Business Requirements**
I plan to enter the airline market by opening a US-based airline company with global routes. My airline will depart from the following US airports:

* John F. Kennedy International Airport (New York City, New York)
* Hartsfield-Jackson Atlanta International Airport (Atlanta, Georgia)
* Charlotte Douglas International Airport (Charlotte, North Carolina)
* Chicago O'Hare International Airport (Chicago, Illinois)
* George Bush Intercontinental Airport (Houston, Texas)
* Dallas-Fort Worth International Airport (Dallas, Texas)
* Los Angeles International Airport (Los Angeles, California)
* Seattle–Tacoma International Airport (Seattle, Washington)
* Miami International Airport (Miami, Florida)
* Denver International Airport (Denver, Colorado)

I want to stand out from my competitors by researching where delays are more frequent, allowing my company to improve operational efficiency and enhance the customer experience when traveling. Below, I have provided a few business requirements I would like to explore:

* Which arrival and departure destinations have seen the highest amounts of delays in 2024? (I will explore this business requirement to identify patterns in delays to increase customer satisfaction.)

* What patterns are seen with flight cancellations? (My company will focus on ensuring that there will be minimized cancellations with commonly cancelled routes, so that my airline is more reliable to customers than my competitors.)

* What are the most common departure times domestically? (I will research flight schedules to identify peak travel times and demand. If more flights are scheduled at a certain time, it means other airlines have planned those departures to meet high demand.)

## **Functional Requirements**
I will display my extensive research in a variety of ways. Below, I have provided a list of my functional requirements:

* The system must successfully pull accurate data from an Azure Storage Blob, including details such as departure and arrival times, statuses, airports, and others.

* The system must be capable of handling large volumes of historical flight data and ensure that there are quick response times for data retrieval.

* Dashboard will provide insightful visuals supporting my business requirements, including insights on flight performance, delays, cancellations, departure and arrival times, and other operational insights. I will allow an extensive amount of filtering and drilling down to view data on specific times and airports.

* The system must support quick and efficient ELT processes so that data can be consistently cleaned, transformed, and stored in a structured format to support advanced analysis and reporting.

## **Data Requirements**
This data is sourced from an Azure Blob and includes airport and airline information. The data retrieved from the blob is originally from a Historical Flight Data API, which is in JSON format.

Data: Historical Flight Schedules API by Aviation Edge

Data Source: https://aviation-edge.com/developers/#historicala

This data contains:

* Flight Type
* Flight Status
* IATA Codes (Flights, Airlines, Airports)
* ICAO Codes (Flights, Airlines, Airports)
* Scheduled Departure and Arrival Times
* Estimated Departure and Arrival Times
* Flight Numbers
* Airline Names
* Codeshare Airlines and Flight Numbers

**Time Range: January 1, 2024-December 31, 2025**

## **Information Architecture**
<img width="1075" alt="CIS 4400 Homework 1 Information Architecture" src="https://github.com/user-attachments/assets/5e19b2bb-a6d5-444a-ae50-38b65d837cf9" />


## **Data Architecture**
<img width="1074" alt="CIS 4400 Homework 1 Data Architecture" src="https://github.com/user-attachments/assets/21cfb999-065a-4589-9c49-6d69f4d3b2e6" />


## **Technical Architecture**
* Data Sourcing: Aviation Edge Historical Flight Data API (Extracted from [Professor Bien-Aime's](https://github.com/ancgate) Azure Blob Storage)
* Data Extraction: Python
* Data Cloud Storage: Microsoft Azure
* Data Transformation (Cleaning and Reformatting): Python
* Data Warehouse: Snowflake
* Data Visualization and Business Intelligence: PowerBI 

## Dimensional Model
<img width="894" alt="image" src="https://github.com/user-attachments/assets/a68a20f8-9464-428c-99ec-145c59340bd8" />

**Flight Fact**
Displays keys used to connect to dimension tables, along with date information and calculated fields such as delay and estimated flight duration.

Size: 8.4m rows

**Flight Dimension**
Further details on the specific flight. Displays flight details including flight type, status, number, IATA code, and ICAO code.

Size: 93.5k rows

**Gate Dimension**
Details on the gate the flight will depart from or arrive at. Displays details including gate number, airport IATA, and airport ICAO.

Size: 11.5k rows
