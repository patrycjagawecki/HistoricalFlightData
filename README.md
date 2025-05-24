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

**Function**: This page provides a high-level overview of KPIs using Power BI card visuals and calculated measures. It addresses core business questions, using:

* On-Time Flight Ratio: Calculated as # of Non-Delayed Flights / Total Flights, helping identify airports and routes with the lowest on-time performance.

* Average Delay: Highlights destination and arrival airports/routes with the highest average delays.

* Cancellation Rate: Measured as # of Cancelled Flights / Total Flights, identifying areas with the highest cancellation percentages.

* Flight Volume by Month: Displays the scheduled departure months with the highest and lowest flight volumes.

**Insights**: Below are the key takeaways from the summary page, which can be used to support business decision-making and address the primary business questions:

* DFW (Dallas-Fort Worth International Airport, Dallas, TX) has the highest delay rate among departure airports, while AAF (Apalachicola Regional Airport, Apalachicola, Florida) leads among destination airports; the ATL (Hartsfield-Jackson Atlanta International Airport, Atlanta, Georgia) to AAF (Apalachicola Regional Airport, Apalachicola, Florida) route shows the most delays overall—prompting further investigation into whether these are caused by external factors (such as weather, air traffic congestion, etc) or internal operational issues that can be addressed.
* Doing further analysis into delay, IAH (George Bush Intercontinental Airport, Houston, TX) has the highest average of delays when departing, while POU (Hudson Valley Regional Airport, Dutchess County, New York) has the highest average of delays as an arrival airport. When examining routes, LAX (Los Angeles International Airport, Los Angeles, California) to SLP (San Luis Potosí International Airport, San Luis Potosí, Mexico) has the highest average delays. These are further airports and routes we need to consider when our company is looking into fixing the issue of flight delays.
* The highest percentage of cancellations comes from DFW (Dallas-Fort Worth International Airport, Dallas, TX) as a departing airport, while ANB (Anniston Regional Airport, Calhoun County, Alabama) has the highest percentage of cancellations as an arrival airport. When looking at routes, ATL (Hartsfield-Jackson Atlanta International Airport, Atlanta, Georgia) to COD (Yellowstone Regional Airport, Cody, Wyoming) has the highest rates of cancellations. This suggests a need to look more closely at operations and conditions affecting these specific airports and routes, as to why they are being cancelled.
* The highest amount of active flights takes place in May, while the lowest occurs in January. This helps identify high and low peak seasons, reflecting fluctuations in travel demand.

Through this, we notice a pattern in DFW (Dallas-Fort Worth International Airport, Dallas, TX) and ATL (Hartsfield-Jackson Atlanta International Airport, Atlanta, Georgia) as recurring airports in both delay and cancellation analytics. This consistency indicates that we need to take a closer look at the operations of these airports and the flights they depart, to understand the root causes and potential areas for improvement.

### **Page 2: Delays**

![image](https://github.com/user-attachments/assets/44a792ff-688e-4870-977f-63abe74ec607)

**Function**: This page provides a detailed overview of delays using different visualizations. If the user would like to look further into specific departure and arrival airports, routes, and estimated departure and arrival dates, they can do so using the slicers in the heading.

**Insights**: Below are the key takeaways from the delays page, which can be used to support business decision-making and address the primary business questions:

* There is a 75.04% rate of delayed flights out of all recorded flights. This high percentage is visually emphasized with a red gauge indicator (conditional formatting), signaling a significant issue that needs to be investigated by my company.
* There are 23.92 average delay minutes when looking at the overall average delay minutes. While this doesn't seem too high, our company is striving to lower that number as delays impact operations and customer satisfaction negatively.
* LAX (Los Angeles International Airport, Los Angeles, California) to ORD (Chicago O'Hare International Airport, Chicago, Illinois) has the largest sum of delays. Out of 66k flights, only 9k flights are on time, which indicates a significant number of delays and suggests this may not be a coincidence. This is a common route, with 66k total flights in the database; further investigation is needed to identify and address potential scheduling or operational issues.
* The largest average delays were recorded in July 2024, with an average delay of 33 minutes. This peak may be attributed to seasonal travel demand, as it follows closely after May, our busiest travel month, or other underlying factors. Further analysis is needed in the next stage of research to identify the root causes and explore potential solutions our airline will implement.
* Although the scatterplot of delays by estimated flight duration appears largely clustered across different durations, there is a noticeable decrease in the density of scatter points as flight duration increases. This suggests that shorter flights tend to experience more frequent delays compared to longer ones, and the reason should be investigated in further analytics.

### **Page 3: Cancellations**

![image](https://github.com/user-attachments/assets/c81644be-b323-441e-96f2-f77cc6f77e32)

**Function**: This page provides a detailed overview of cancellations using different visualizations. If the user would like to look further into specific departure and arrival airports, routes, and estimated departure and arrival dates, they can do so using the slicers in the heading.

**Insights**: Below are the key takeaways from the cancellations page, which can be used to support business decision-making and address the primary business questions:

* There is a 22.41% rate of cancelled flights out of all recorded flights. This percentage is visually represented with a green gauge indicator (using conditional formatting), suggesting that while cancellations are not significantly high, they still represent a meaningful portion of total flights and something our company should further investigate.
* ATL (Hartsfield-Jackson Atlanta International Airport, Atlanta, Georgia) has the largest number of cancelled flights as a departing airport, with around 440,000 flights cancelled. Given ATL's role as a major airport and one of the few airports our airline departs, this high volume of cancellations could have an impact on flight reliability, making it a priority for further review.
* ATL (Hartsfield-Jackson Atlanta International Airport, Atlanta, Georgia) to MCO (Orlando International Airport, Orlando, Florida) has the largest number of cancellations, operating 94k flights, of which 22k are cancelled. ATL has already been identified in this analysis as the airport with the highest number of cancellations, and this further reinforces the need to investigate its departure operations and recurring issues on heavily traveled routes like ATL to MCO.
* The highest number of cancellations occurs between May and August, aligning with our earlier analysis identifying May as a peak travel month. This correlation suggests that increased flight volume during peak season may contribute to a higher rate of cancellations.
* The scatterplot shows that cancellations are more common on shorter flights, with a noticeable peak of over 10,000 cancelled flights on routes with an estimated duration of around one hour. This suggests that shorter routes may be more vulnerable to disruptions or deprioritization during scheduling adjustments, which our company is aware of and an area it will work on.

### **Page 3: Common Scheduled Departure Times**

![image](https://github.com/user-attachments/assets/2f0100f5-91a5-4fda-b8f6-5274fa8cdf23)

**Function**: This page provides a detailed overview of flight scheduling using a line plot displaying counts of active flights by scheduled departure months and a table displaying our departing airports, their peak month based on their maximum active flight count. If the user would like to look further into specific departure and arrival airports, routes, and estimated departure and arrival dates, they can do so using the slicers in the heading.

**Insights**: Below are the key takeaways from the scheduled departures page, which can be used to support business decision-making and address the primary business questions:

* There are approximately 593,000 active flights in May, indicating a peak travel season with higher demand for flights. Additionally, May appears as the most common peak month for several major airports, including CLT, DEN, ORD, and DFW (noting that the sample includes only 4 flights from DFW). This suggests that scheduling efforts should prioritize May as a key month for increasing flight availability at departure airports. Moreover, the supporting table can be used to optimize flight scheduling by identifying and aligning with the busiest months for each individual departure airport.

## **Conclusion**
