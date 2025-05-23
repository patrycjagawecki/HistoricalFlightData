## Azure Blob Storage Configuration Setup for Extraction (Data_Extraction.ipynb)

The dataset utilized in this analysis is accessible exclusively via the private Azure Blob Storage connection string configured for this project. If you wish to conduct your own analysis, you can obtain similar data by accessing the [Historical Flight Data API by Aviation Edge](https://aviation-edge.com/historical-flight-schedules-api/).
*Please note that this API requires registration and is only available through a paid subscription.*

**A config.json file is required to connect to the source Azure Blob Storage and transfer data to your own Azure Blob Storage account.**

An example config.json file for data extraction is shown below:

*(Please note: this is an annonymized version for demonstration purposes only; make sure to replace all values with your own credentials and configuration details)*

{

  "ORIGIN_AZURE_CONNECTION_STRING" : "DefaultEndpointsProtocol=https;AccountName=***ORIGINACCOUNTNAME***;AccountKey=***ORIGINACCOUNTKEY***==;EndpointSuffix=***ORIGINENDPOINTSUFFIX***",
  "ORIGIN_CONTAINER_NAME": "***ORIGINCONTAINER***",
  "DESTINATION_AZURE_CONNECTION_STRING" : "DefaultEndpointsProtocol=https;AccountName=***DESTINATIONACCOUNTNAME***;AccountKey=***DESTINATIONACCOUNTKEY***==;EndpointSuffix=***DESTINATIONENDPOINTSUFFIX***",
  "DESTINATION_CONTAINER_NAME": "***DESTINATIONCONTAINER***"

}

