---
layout: default
title: COP API Tutorial creating POIs and Zones  <!--- This is required for the page to come in the side pane --->
---
<span style="font-size:2em;">COP API Tutorial creating POIs and Zones</span>
<!-- Using Span is a hack to avoid the title to come again in TOC.-->

This is a tutorial for how to use the COP (Common Operational Picture) API to create new points of interest (POI) and is based on using the [Demonstration of staff management with LoRa based locators](https://github.com/MONICA-Project/staff-management-demo) simulated demonstration.

* TOC (Do not remove. This is required to show Table of contents)
 {:toc}

## Prerequistes
[Demonstration of staff management with LoRa based locators](https://github.com/MONICA-Project/staff-management-demo) needs to be launched in docker, follow the instructions there.
## Introduction
The COP API provides builders of apps and user interfaces the means of accessing the underlying MONICA functionality. This tutorial will focus on how to add POI information to the COP, i.e. predefined Points Of Interest POI, called instance data. This can be areas/zones of interest as well as individual POIs like stages, exits et c.
## Basic Components of the API
The API is JSON REST based and has a swagger web interface available, which can be used for testing the different parts of the API. If you have installed [COP API](https://github.com/MONICA-Project/staff-management-demo) it will be available on http://127.0.0.1:8800. The swagger interface lists all available API calls: 

![COP API Swagger](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/cop-api-start.PNG "COP API Swagger")

Each of the API calls are grouped by functionality, such as EventAPI. If one scrolls towards the there is a section in the swagger detailing the different models, i.e. objects, used in the API:
![COP API Models](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/cop-api-models.PNG "COP API Models")



## Testing the API
The swagger definition allows also for testing the API directly in the browser, showing the result and also all settings needed when calling the method. This is a great help when implementing calls from another component, such as an app.
### Add a POI using the swagger interface
The first example is to add a simple POI which represents a Cocktail Stand at a specific point. Find the ZoneApi in the swagger definition and expand the POST method.


![Swagger ZoneAPI](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/cop-api-zone.PNG "Swagger ZoneAPI")

The click on "Try it out" and fill in these values 
```json
{
  "id": 0,
  "name": "MONICA POI",
  "description": "A place for a drink",
  "metadata": "",
  "type": "Cocktail Stand",
  "capacity": 0,
  "peoplecount": 0,
  "boundingPolygon": [
    [
      50.749111, 7.203320
    ]
  ]
}
```
**NB!** The API requires a static authentication key:
````
6ffdcacb-c485-499c-bce9-23f76d06aa36
````
Execute the API call by clicking on the Execute button below:
![Swagger POICreate](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/cop-api-add-zone.PNG "Swagger POICreate")

If all went well, the result of the call is displayed, there should be a new Cocktail Stand shown in the COP UI.
(The UI is available on http://127.0.0.1:8900 and make sure that the filter for Cocktail Stands is activated)

![Swagger POIAdded](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/added%20POI.PNG "Swagger POIAdded")


### Adding a Zone using the swagger interface
One can also add more complex zones/areas which are created from a series of coordinates and will create an area that is highlited in the COP UI. It uses the same API call as the previous example but the parameter should contain a list of coordinates.

```json
{
  "id": 0,
  "name": "MONICA Zone",
  "description": "An area",
  "metadata": "",
  "type": "Zone",
  "capacity": 0,
  "peoplecount": 0,
  "boundingPolygon": [
   [50.7433786,7.1545255],
[50.7434805,7.1552765],
[50.744268,7.1558558],
[50.7449876,7.1551585],
[50.7444106,7.1542465],
[50.7433786,7.1545255]
  ]
}
```
Change the parameter to the above one and execute the API call by clicking on the Execute button.
If all went well, there should be a new Zone shown in the COP UI.
(The UI is available on http://127.0.0.1:8900 and make sure that the filter for Zone is activated)
![COP UI Filter](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/Zone%20added.PNG "COP UI Filter")

You see the zone as the blue area in the map.

