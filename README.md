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

* What are the most common departure times flying out of the airports my airline is departing from? (I will research flight schedules to identify peak travel months and demand. If more flights are scheduled at around a certain season, it means other airlines have planned those departures to meet high demand.)

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

![Historical Flight Data Architecture drawio](https://github.com/user-attachments/assets/d22c30a1-994d-40a8-9d6f-79785c6412fa)

* Data Sourcing: Aviation Edge Historical Flight Data API (Extracted from [Professor Bien-Aime's](https://github.com/ancgate) Azure Blob Storage)
* Data Extraction: Python
* Data Cloud Storage: Microsoft Azure
* Data Transformation (Cleaning and Reformatting): Python
* Data Warehouse: Snowflake
* Data Visualization and Business Intelligence: PowerBI

## **Medallion Architecture**

* Bronze (Azure Data): Raw JSON files containing historical flight data, extracted directly from Azure Blob Storage without any transformations or cleaning. Records for each day are stored in different JSON files.
* Silver (Python Data): The data was cleaned in Python (ELT.ipynb) where unnecessary columns and rows were dropped, columns were renamed, and the different JSON records consolidated into one dataframe.
* Gold (PowerBI Data): The data was reorganized into a star schema, which was connected in PowerBI, and now we can create metrics and visuals for our analytics.

## **Dimensional Model**
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

## **PowerBI Report**

### **Page 1: Summary**

![image](https://github.com/user-attachments/assets/806876e4-a1f7-41e2-b8cf-9e552fa4d382)

**Function**: This page provides a high-level overview of key performance indicators using Power BI card visuals and calculated measures. It addresses core business questions, including:

* On-Time Flight Ratio: Calculated as # of Non-Delayed Flights / Total Flights, helping identify airports and routes with the lowest on-time performance.

* Average Delay: Highlights destination and arrival airports/routes with the highest average delays.

* Cancellation Rate: Measured as # of Cancelled Flights / Total Flights, identifying areas with the highest cancellation percentages.

* Flight Volume by Month: Displays the scheduled departure months with the highest and lowest flight volumes.

**Insights**: Below are the key takeaways from the summary page, which can be used to support business decision-making and address the primary business questions:

* DFW (Dallas-Fort Worth International Airport, Dallas, TX) has the highest delay rate among departure airports, while AAF (Apalachicola Regional Airport, Apalachicola, Florida) leads among destination airports; the ATL (Hartsfield-Jackson Atlanta International Airport, Atlanta, Georgia) to AAF (Apalachicola Regional Airport, Apalachicola, Florida) route shows the most delays overall—prompting further investigation into whether these are caused by external factors (such as weather, air traffic congestion, etc) or internal operational issues that can be addressed.
* Doing further analysis into delay, IAH (George Bush Intercontinental Airport, Houston, TX) has the highest average of delays when departing, while POU (Hudson Valley Regional Airport, Dutchess County, New York) has the highest average of delays as an arrival airport. When examining routes, LAX (Los Angeles International Airport, Los Angeles, California) to SLP (San Luis Potosí International Airport, San Luis Potosí, Mexico) has the highest average delays. These are further airports and routes we need to consider when our company is looking into fixing the issue of flight delays.
* The highest percentage of cancellations comes from DFW (Dallas-Fort Worth International Airport, Dallas, TX) as a departing airport, while ANB (Anniston Regional Airport, Calhoun County, Alabama) has the highest percentage of cancellations as an arrival airport. When looking at routes, ATL (Hartsfield-Jackson Atlanta International Airport, Atlanta, Georgia) to COD (Yellowstone Regional Airport, Cody, Wyoming) has the highest rates of cancellations. This suggests a need to look more closely at operations and conditions affecting these specific airports and routes, as to why they are being cancelled.
* The highest amount of active flights takes place in May, while the lowest occurs in January. This helps identify high and low peak seasons, reflecting fluctuations in travel demand.

Through this, we notice a pattern in DFW (Dallas-Fort Worth International Airport, Dallas, TX) and ATL (Hartsfield-Jackson Atlanta International Airport, Atlanta, Georgia) as recurring airports in both delay and cancellation analytics. This consistency indicates that we need to take a closer look into the operations of these airports and flights they depart, to understand the root causes and potential areas for improvement.
