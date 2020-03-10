---
layout: default
title: IoT-DB Tutorial simple querying  <!--- This is required for the page to come in the side pane --->
---
<span style="font-size:2em;">IoT-DB Tutorial simple querying</span>
<!-- Using Span is a hack to avoid the title to come again in TOC.-->

This is a tutorial for how to make simple queries in the IoT-DB and is based on using the [Demonstration of staff management with LoRa based locators](https://github.com/MONICA-Project/staff-management-demo) simulated demonstration.

* TOC (Do not remove. This is required to show Table of contents)
 {:toc}

## Prerequistes
[Demonstration of staff management with LoRa based locators](https://github.com/MONICA-Project/staff-management-demo) needs to be launched in docker, follow the instructions there.
## Introduction
The IoT-DB is where all the collected data from the different sensors and fusion services are stored. The IoT-DB is a OGC SensorThings API compliant database that that supports different queries.
## The OGC Sensorthings API model
The OGC Sensorthings API model has a quite simple storage model:

![OGC](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/ogc.png "OGC")

The most important entities in the IoT-DB are:
- Sensor: represents the different input devices, such as trackers
- Datastream: represents the streams of data, for instance positions et c. (One sensor can have many datastreams)
- Observations: The actual values/results.

The complete standard is available at  [OGC Sensorthings API](http://docs.opengeospatial.org/is/15-078r6/15-078r6.html)

## Simple browsing of the IoT-DB
The best way of browsing the IoT-DB is to use the Firefox browser since it makes it possible to navigate using the links in the result. Otherwise you need to copy the links manually in the browser.

### List all sensors
Use the following URL in your browser to list all defined sensors in the IoT-DB:
<http://localhost:8090/v1.0/Sensors>

The result will display all the avialable sensors. In this case only one, "GPS".
![COPDBSensors](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/gost_sensors.PNG "COPDBSensors")

### List all associated Datastreams
In the previous result there is a link "Datastreams@iot.navigationLink" with the value

<http://localhost:8090/v1.0/Sensors(1)/Datastreams>

Following this link will display all the datastreams associated with this Sensor
![COPDBDatastreams](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/gost_datastreams.PNG "COPDBDatastreams")

### Listing Observations
In the previous result there is a link named "Observations@iot.navigationLink"

<http://localhost:8090/v1.0/Datastreams(22)/Observations>

Following this link will display all the Observations associated with this Datastream

![OGCObservations](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/ogc-observations.PNG "OGCObservations")

Each observation consists of this structure:
````json
 {
         "@iot.id": 34060,
         "@iot.selfLink": "http://localhost:8090/v1.0/Observations(34060)",
         "phenomenonTime": "2020-03-06T12:15:45.195Z",
         "result": {
            "type": "uwb",
            "tagId": "XE",
            "timestamp": "2020-03-06T12:15:45.1956577+00:00",
            "last_known_gps": "2020-03-06T12:15:45.1956634Z",
            "last_known_lat": 50.74455010534961,
            "last_known_lon": 7.153483710857724
         },
         "Datastream@iot.navigationLink": "http://localhost:8090/v1.0/Observations(34060)/Datastream",
         "FeatureOfInterest@iot.navigationLink": "http://localhost:8090/v1.0/Observations(34060)/FeatureOfInterest",
         "resultTime": "2020-03-06T12:15:45.206336+00:00"
      }
````
The important attributes in the Observation are:
- phenomenonTime: when the result was sampled
- resultTime: when the result was stored
- result: the observation itself. It can be a simple value or a JSON structure itself.

## Querying using filters and expand
The OGC Sensorthings allow for querying by using filters and also to include related entities by using expand.
### $filter
$filter is used for filtering and querying the IoT-DB. For example, to list all the Datastreams which are GPS coordinates we can filter on the Datastream description:

````
http://localhost:8090/v1.0/Datastreams?$filter=substringof('GPS/Localization-GPS',name)
````
This will retrieve all the Datastreams that have GPS/Localization-GPS in their name.

### $expand
A common case is that you select the Datastreams that you are interested in but you also want to include the latest Observation. This can be achieved by using $expand:

````
http://localhost:8090/v1.0/Datastreams?$filter=substringof('GPS/Localization-GPS',name)&$expand=Observations($top=1)
````
For each of the Datastreams the latest Observation will be included:
````json
{
         "@iot.id": 21,
         "@iot.selfLink": "http://localhost:8090/v1.0/Datastreams(21)",
         "name": "GPS-TRACKER-GW-REST/GPS/Localization-GPS/XE",
         "description": "uwb",
         "unitOfMeasurement": {
            "definition": "http://www.qudt.org/qudt/owl/1.0.0/unit/Instances.html#DegreeAngle",
            "name": "position",
            "symbol": [
               ""
            ]
         },
         "observationType": "http://www.opengis.net/def/observationType/OGC-OM/2.0/OM_Measurement",
         "observedArea": {
            "coordinates": [
               0,
               0
            ],
            "type": "Point"
         },
         "Thing@iot.navigationLink": "http://localhost:8090/v1.0/Datastreams(21)/Thing",
         "Sensor@iot.navigationLink": "http://localhost:8090/v1.0/Datastreams(21)/Sensor",
         "ObservedProperty@iot.navigationLink": "http://localhost:8090/v1.0/Datastreams(21)/ObservedProperty",
         "Observations": [
            {
               "@iot.id": 38031,
               "@iot.selfLink": "http://localhost:8090/v1.0/Observations(38031)",
               "phenomenonTime": "2020-03-06T12:44:37.417Z",
               "result": {
                  "lat": 50.74435864835979,
                  "lon": 7.15352407459757,
                  "snr": 9.75,
                  "hdop": 2.90000009536743,
                  "host": "loranode1",
                  "type": "uwb",
                  "tagId": "XE",
                  "height": 141.399993896484,
                  "timestamp": "2020-03-06T12:44:37.4171046Z",
                  "battery_level": 4.07999992370605
               },
               "Datastream@iot.navigationLink": "http://localhost:8090/v1.0/Observations(38031)/Datastream",
               "FeatureOfInterest@iot.navigationLink": "http://localhost:8090/v1.0/Observations(38031)/FeatureOfInterest",
               "resultTime": "2020-03-06T12:44:37.419518+00:00"
            }
         ]
      }
````
By changing $top one can determine how many of the last Observations are returned.
