# API Guide

## Oceans 3.0 API overview

Check [here](https://wiki.oceannetworks.ca/display/O2A/API+Overview) for more information.

## Glossary of terms

Check [here](https://wiki.oceannetworks.ca/display/O2A/Glossary+of+Terms) for more information.

## The ONC class

The [ONC](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC) (Python) / Onc (MATLAB) class provides a wrapper for Oceans 3.0 API requests.
All the client library's functionality is provided as methods of this class.
Each [Oceans 3.0 public API](https://data.oceannetworks.ca/OpenAPI) has a corresponding public method in this class.
In addition, the ONC class provides some useful helper methods that involve multiple APIs to simplify the workflow.

Create an ONC (Python) / Onc (MATLAB) object to access this library's functionalities.

```python
# Python
from onc import ONC

onc = ONC("YOUR_TOKEN_HERE")
```

```
% MATLAB
onc = Onc('YOUR_TOKEN_HERE')
```

## Discovery methods

Discovery methods can be used to search for available locations, deployments, device categories, devices, properties, and data products.
They support numerous filters and might resemble an "advanced search" function for ONC data sources.

Use discovery methods to:

- Obtain the identification codes required to use other API services.
- Explore what's available in a certain location or device.
- Obtain the deployment dates for a device.
- List available data products for download in a particular device or location.

::: {note}

- Locations can contain other locations.
  - "Cambridge bay" may contain separate children locations for its underwater network and shore station.
- Locations can contain device categories, which contain devices, which contain properties.
- Searches can be performed without considering the hierarchy mentioned above.
  - You can search for locations with data on a specific property or search for all properties in a specific location.

:::

|                                   API Endpoint                                   |             Description             |                                                              Python                                                               |        MATLAB        |
| :------------------------------------------------------------------------------: | :---------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------: | :------------------: |
|        [/locations](https://data.oceannetworks.ca/OpenAPI#get-/locations)        |          Return locations           |        [getLocations](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getLocations)        |     getLocations     |
|   [/locations/tree](https://data.oceannetworks.ca/OpenAPI#get-/locations/tree)   |       Return a location tree        |    [getLocationsTree](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getLocationsTree)    | getLocationHierarchy |
|      [/deployments](https://data.oceannetworks.ca/OpenAPI#get-/deployments)      | Return a list of device deployments |      [getDeployments](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getDeployments)      |    getDeployments    |
| [/deviceCategories](https://data.oceannetworks.ca/OpenAPI#get-/deviceCategories) | Return a list of device categories  | [getDeviceCategories](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getDeviceCategories) | getDeviceCategories  |
|          [/devices](https://data.oceannetworks.ca/OpenAPI#get-/devices)          |      Return a list of devices       |          [getDevices](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getDevices)          |      getDevices      |
|       [/properties](https://data.oceannetworks.ca/OpenAPI#get-/properties)       |     Return a list of properties     |       [getProperties](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getProperties)       |    getProperties     |
|     [/dataProducts](https://data.oceannetworks.ca/OpenAPI#get-/dataProducts)     |   Return a list of data products    |     [getDataProducts](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getDataProducts)     |   getDataProducts    |

## Data product download methods

Data product download methods allow you to request and download more than 120 different types of [ONC data products](https://wiki.oceannetworks.ca/display/O2A/Available+Data+Products),
with granular control over what data to obtain, from where, and in what time frame.
They are comparable to the download functionality from ONC's [Data Search](https://data.oceannetworks.ca/DataSearch) tool.

Examples of usage include:

- Downloading PNG plots of sensor readings in a device
- Downloading sensor readings as .mat files, text files, or in commercial manufacturer formats
- Downloading compressed or raw audio files from hydrophones

:::{note}

If the data product requested doesn't exist in our archive, it will be generated by our servers before your download starts.

:::

|                                               API Endpoint                                               |                  Description                  |                                                              Python                                                               | MATLAB              |
| :------------------------------------------------------------------------------------------------------: | :-------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------: | ------------------- |
|  [/dataProductDelivery/request](https://data.oceannetworks.ca/OpenAPI#get-/dataProductDelivery/request)  |            Request a data product             |  [requestDataProduct](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.requestDataProduct)  | requestDataProduct  |
|   [/dataProductDelivery/status](https://data.oceannetworks.ca/OpenAPI#get-/dataProductDelivery/status)   | Check status of a <br> requested data product |    [checkDataProduct](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.checkDataProduct)    | checkDataProduct    |
|      [/dataProductDelivery/run](https://data.oceannetworks.ca/OpenAPI#get-/dataProductDelivery/run)      |         Run a requested data product          |      [runDataProduct](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.runDataProduct)      | runDataProduct      |
|   [/dataProductDelivery/cancel](https://data.oceannetworks.ca/OpenAPI#get-/dataProductDelivery/cancel)   |         Cancel a running data product         |   [cancelDataProduct](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.cancelDataProduct)   | cancelDataProduct   |
|  [/dataProductDelivery/restart](https://data.oceannetworks.ca/OpenAPI#get-/dataProductDelivery/restart)  |       Restart a cancelled data product        |  [restartDataProduct](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.restartDataProduct)  | restartDataProduct  |
| [/dataProductDelivery/download](https://data.oceannetworks.ca/OpenAPI#get-/dataProductDelivery/download) |            Download a data product            | [downloadDataProduct](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.downloadDataProduct) | downloadDataProduct |

Helper methods are listed below.

|                Description                |                                                           Python                                                            | MATLAB           |
| :---------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------: | ---------------- |
| Request, run, and download a data product | [orderDataProduct](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.orderDataProduct) | orderDataProduct |

## Near real-time data access methods

Near real-time (as fast as they get into our database) data access methods allow the extraction of sensor data as time-series,
either as processed scalar data with [Quality Assurance and Control flags](https://wiki.oceannetworks.ca/display/DP/Quality+Assurance+Quality+Control) (QAQC)
or directly as raw data obtained from the device in its specific output format.
In contrast to the Data product download methods, this data can be downloaded directly without waiting for any kind of generation process.

Common use cases include:

- Plotting time series from properties in a specific time frame or in "near real-time"
- Quickly obtaining the latest reading from a particular sensor
- Obtaining raw unprocessed data from our instruments (data might require processing to be readable)

::: {note}

The methods `getScalardataByLocation()` and `getRawdataByLocation()` obtain data readings from a location
no matter what device it came from (hence the need to specify a _device category code_ instead of a single _device code_).
You might want to obtain data by location instead of by device, as individual devices are often replaced/repositioned.

Each request to our API can return a maximum of 100,000 samples; larger data requests must be downloaded as a sequence of pages.
Use the _allPages_ parameter to automatically download all pages required for your requested time frame.

:::

|                                      API Endpoint                                      |                             Description                              |                                                                  Python                                                                   | MATLAB                 |
| :------------------------------------------------------------------------------------: | :------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------------: | ---------------------- |
| [/scalardata/location](https://data.oceannetworks.ca/OpenAPI#get-/scalardata/location) | Return scalar data <br> from a specific location and device category | [getScalardataByLocation](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getScalardataByLocation) | getDirectByLocation    |
|   [/scalardata/device](https://data.oceannetworks.ca/OpenAPI#get-/scalardata/device)   |              Return scalar data from a specific device               |   [getScalardataByDevice](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getScalardataByDevice)   | getDirectByDevice      |
|    [/rawdata/location](https://data.oceannetworks.ca/OpenAPI#get-/rawdata/location)    |  Return raw data <br> from a specific location and device category   |    [getRawdataByLocation](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getRawdataByLocation)    | getDirectRawByLocation |
|      [/rawdata/device](https://data.oceannetworks.ca/OpenAPI#get-/rawdata/device)      |                Return raw data from a specific device                |      [getRawdataByDevice](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getRawdataByDevice)      | getDirectRawByDevice   |

Helper methods are listed below.

|                                     Description                                      |                                                                 Python                                                                  | MATLAB |
| :----------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------: | ------ |
| Return a list of sensor category codes <br> prior to querying the scalardata service | [getSensorCategoryCodes](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getSensorCategoryCodes) |        |
|                                  Return scalar data                                  |          [getScalardata](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getScalardata)          |        |
|                                   Return raw data                                    |             [getRawdata](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getRawdata)             |        |

## Archive file download methods

These methods allow users to directly download previously generated data product files from our archive.

ONC systems auto-generate and archive files of different types at set time intervals.
These archived files can be downloaded without waiting for a generation process to finish
(potentially faster than [Data product download methods](#data-product-download-methods)).

::: {note}

Archived files have a unique filename (e.g. "NAXYS_HYD_007_20091231T235919.476Z-spect.png")
that includes the device code ("NAXYS_HYD_007") and the UTC date-time
when the data in the file started being measured ("20091231T235919.476Z").
The filename might contain additional information.

:::

::: {caution}

Due to security regulations, some very recent files (e.g. hydrophone.wav files in the last hour) might not be made immediately available.

:::

|                                       API Endpoint                                       |                                        Description                                         |                                                                   Python                                                                    | MATLAB            |
| :--------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------: | ----------------- |
| [/archivefile/location](https://data.oceannetworks.ca/OpenAPI#get-/archivefile/location) | Return a list of available archive files <br> from a specific location and device category | [getArchivefileByLocation](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getArchivefileByLocation) | getListByLocation |
|   [/archivefile/device](https://data.oceannetworks.ca/OpenAPI#get-/archivefile/device)   |            Return a list of available archive files <br> from a specific device            |   [getArchivefileByDevice](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getArchivefileByDevice)   | getListByDevice   |
| [/archivefile/download](https://data.oceannetworks.ca/OpenAPI#get-/archivefile/download) |                                  Download an archive file                                  |      [downloadArchivefile](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.downloadArchivefile)      | getFile           |

Helper methods are listed below.

|                              Description                               |                                                                    Python                                                                     | MATLAB         |
| :--------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------: | -------------- |
| Download a list of archived files <br> that match the filters provided | [downloadDirectArchivefile](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.downloadDirectArchivefile) | getDirectFiles |
|                Return a list of available archive files                |            [getArchivefile](https://oceannetworkscanada.github.io/api-python-client/autoapi/onc/index.html#onc.ONC.getArchivefile)            |                |
