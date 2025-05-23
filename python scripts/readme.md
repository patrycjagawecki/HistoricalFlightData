## Azure Blob Storage Configuration Setup for Extraction (Data_Extraction.ipynb)

To access the historical flight data, I used an Azure Blob Storage connection string to copy the data from a container in another account (provided by the professor) to my own Azure Blob Storage account.

The data utilized in this analysis is accessible exclusively via the private Azure Blob Storage connection string configured for this project. If you wish to conduct your own analysis, you can obtain similar data by accessing the [Historical Flight Data API by Aviation Edge](https://aviation-edge.com/historical-flight-schedules-api/).
*Please note that this API requires registration and is only available through a paid subscription.*

**A config.json file is required to connect to the source Azure Blob Storage and transfer data to your own Azure Blob Storage account. DO NOT UPLOAD THIS FILE TO GITHUB**

An example config.json file for data extraction is shown below:

*(Please note: this is an annonymized version for demonstration purposes only; make sure to replace all values with your own credentials and configuration details)*

{

  "ORIGIN_AZURE_CONNECTION_STRING" : "DefaultEndpointsProtocol=https;AccountName=***ORIGINACCOUNTNAME***;AccountKey=***ORIGINACCOUNTKEY***==;EndpointSuffix=***ORIGINENDPOINTSUFFIX***",
  "ORIGIN_CONTAINER_NAME": "***ORIGINCONTAINER***",
  "DESTINATION_AZURE_CONNECTION_STRING" : "DefaultEndpointsProtocol=https;AccountName=***DESTINATIONACCOUNTNAME***;AccountKey=***DESTINATIONACCOUNTKEY***==;EndpointSuffix=***DESTINATIONENDPOINTSUFFIX***",
  "DESTINATION_CONTAINER_NAME": "***DESTINATIONCONTAINER***"

}

## ELT Process (ELT.ipynb)

For this project, I implemented an ELT (Extract, Load, Transform) process. A high-level overview of the steps involved in this process is outlined below:

1. I extracted the data using an Azure Connection (please see "Azure Blob Storage Configuration Setup for Extraction" section above for more details).
2. I loaded the data into Snowflake using the user interface. A stage was created to connect to my Azure storage account, where I then configured the connection to the container using a SAS token. From there, I used the "Load Data" wizard to select the JSON file, define the file format, and import the data into the appropriate Snowflake table.
3. I used a config.json file to load Snowflake configuration values, so that I can establish a connection to Snowflake. From there, I started my extraction process, where I extracted data from Snowflake into a Pandas dataframe and cleaned the data, and formatted the data into fact and dimension tables (More details on cleaning and reformatting can be found in the ELT.ipynb file).
4. After preparing the transformed version of my data, I used SQLAlchemy to upload both the fact and dimension tables back into Snowflake in chunks for efficient data transfer.

Cleaning and Formatting Done for the Transformation Process:
* Dropped unnecessary columns
* Updated data types to ensure consistency and compatibility
* Utilized joins to connect dimension tables to fact tables
* Assigned surrogate keys
* Created business calculations such as flight duration and delay

**Please note: A config.json file is required to establish a connection to Snowflake. DO NOT UPLOAD THIS FILE TO GITHUB**

*(Please note: this is an annonymized version for demonstration purposes only; make sure to replace all values with your own Snowflake credentials)*

