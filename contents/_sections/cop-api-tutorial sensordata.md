---
layout: default
title: COP API Tutorial for retrieving sensordata  <!--- This is required for the page to come in the side pane --->
---
<span style="font-size:2em;">COP API Tutorial for retrieving sensordata</span>
<!-- Using Span is a hack to avoid the title to come again in TOC.-->

This is a tutorial for how to use the COP (Common Operational Picture) API to retrieve which sensors are available [Demonstration of Sound Monitoring an event using Sound Level Meters](https://github.com/MONICA-Project/DockerSoundDemo) simulated demonstration.

* TOC (Do not remove. This is required to show Table of contents)
 {:toc}

## Prerequistes
[Demonstration of Sound Monitoring an event using Sound Level Meters](https://github.com/MONICA-Project/DockerSoundDemo) needs to be launched in docker, follow the instructions there.
## Introduction
The COP API provides builders of apps and user interfaces the means of accessing the underlying MONICA functionality. This tutorial will focus on how to access and retrieve different sensor values, i.e. the known sensors and their current values.
## Basic Components of the API
The API is JSON REST based and has a swagger web interface available, which can be used for testing the different parts of the API. If you have installed [Demonstration of Sound Monitoring an event using Sound Level Meters](https://github.com/MONICA-Project/DockerSoundDemo) it will be available on http://127.0.0.1:8800. The swagger interface lists all available API calls: 

![COP API Swagger](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/cop-api-start.PNG "COP API Swagger")

Each of the API calls are grouped by functionality, such as EventAPI. If one scrolls towards the there is a section in the swagger detailing the different models, i.e. objects, used in the API:
![COP API Models](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/cop-api-models.PNG "COP API Models")



## Testing the API
The swagger definition allows also for testing the API directly in the browser, showing the result and also all settings needed when calling the method. This is a great help when implementing calls from another component, such as an app.
### List all sound level meters
The first example is to list all known sound level meters in the MONICA system. Locate the GET /things operation in the ThingApi section in the swagger


![Swagger ThingApi](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/cop-api-get-things1.png "Swagger ThingApi")

Then click on "Try it out" and fill in thingType with: 
```
Soundmeter
```
**NB!** The API requires a static authentication key:
````
6ffdcacb-c485-499c-bce9-23f76d06aa36
````
Execute the API call by clicking on the Execute button below.
The result of the call is shown below and contains all the known sound level meters
![Swagger GetThings](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/cop-api-get-thingsresult.png "Swagger GetThings")

If all went well, the result of the call should look like this:
```json
[
  {
    "id": 639,
    "name": "MONICA0010_100090_Id1",
    "description": "Audience Main stage",
    "thingtype": null,
    "thingTemplate": "Soundmeter",
    "status": 1,
    "lat": 45.797271,
    "lon": 4.95223,
    "ogcid": "MONICA0010_100090_Id1"
  },
  {
    "id": 632,
    "name": "MONICA0011_000514_Id8",
    "description": "Neighbour Meyzieu",
    "thingtype": null,
    "thingTemplate": "Soundmeter",
    "status": 1,
    "lat": 45.774659,
    "lon": 4.995161,
    "ogcid": "MONICA0011_000514_Id8"
  },
  {
    "id": 638,
    "name": "MONICA0008_100091_Id2",
    "description": "Audience Woodsfloor",
    "thingtype": null,
    "thingTemplate": "Soundmeter",
    "status": 1,
    "lat": 45.798225,
    "lon": 4.952834,
    "ogcid": "MONICA0008_100091_Id2"
  },
  {
    "id": 636,
    "name": "MONICA0001_000526_Id4",
    "description": "Audience Chapiteau",
    "thingtype": null,
    "thingTemplate": "Soundmeter",
    "status": 1,
    "lat": 45.797394,
    "lon": 4.95103,
    "ogcid": "MONICA0001_000526_Id4"
  },
  {
    "id": 635,
    "name": "MONICA0002_000504_Id5",
    "description": "Neighbour Miribel",
    "thingtype": null,
    "thingTemplate": "Soundmeter",
    "status": 1,
    "lat": 45.822395,
    "lon": 4.95298,
    "ogcid": "MONICA0002_000504_Id5"
  },
  {
    "id": 634,
    "name": "MONICA0004_000608_Id6",
    "description": "Neighbour Neyron",
    "thingtype": null,
    "thingTemplate": "Soundmeter",
    "status": 1,
    "lat": 45.814751,
    "lon": 4.93279,
    "ogcid": "MONICA0004_000608_Id6"
  },
  {
    "id": 637,
    "name": "MONICA0007_100092_Id3",
    "description": "Audience Scène St Denis",
    "thingtype": null,
    "thingTemplate": "Soundmeter",
    "status": 1,
    "lat": 45.797346,
    "lon": 4.952655,
    "ogcid": "MONICA0007_100092_Id3"
  },
  {
    "id": 633,
    "name": "MONICA0009_000415_Id7",
    "description": "Neighbour Vaulx-en-Velin",
    "thingtype": null,
    "thingTemplate": "Soundmeter",
    "status": 1,
    "lat": 45.787803,
    "lon": 4.924371,
    "ogcid": "MONICA0009_000415_Id7"
  }
]
```


### Retrieving a specific thing with together with its observations
One can also query for a specific thing and retieve a number of the last Observations it has made. Locate the 
GET/thingsWithObservation/{id}
![Swagger GetThingWithObservation](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/cop-api-get-thingbyidwithobs.png "Swagger GetThingWithObservation")

Then click on "Try it out" and fill in id and noOfObservations with: 
```
id 634 (Or any ID from the previous result)
noOfObservations 1
```
**NB!** The API requires a static authentication key:
````
6ffdcacb-c485-499c-bce9-23f76d06aa36
````
Execute the API call by clicking on the Execute button below.

![Swagger GetThingWithObservation](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/cop-api-get-thingbyidwithobsresult.png "Swagger GetThingWithObservation")

The resulting json looks like the following. Note that some datastreams, such as CPBLZeq, have been removed for space.
```json
{
  "id": 634,
  "name": "MONICA0004_000608_Id6",
  "description": "Neighbour Neyron",
  "thingTemplate": "Soundmeter",
  "status": 1,
  "lat": 45.814751,
  "lon": 4.93279,
  "ogcid": "MONICA0004_000608_Id6",
  "observations": [
    {
      "thingId": 634,
      "datastreamId": "SLM-GW/SLM/LCeq/MONICA0004_000608_Id6",
      "type": "",
      "personid": null,
      "zoneid": null,
      "phenomenTime": "2020-04-13T14:40:17.344+00:00",
      "observationResult": "{\n  \"@iot.id\": 737,\n  \"@iot.selfLink\": \"http://localhost:8090/v1.0/Observations(737)\",\n  \"phenomenonTime\": \"2020-04-13T14:40:17.344Z\",\n  \"result\": {\n    \"response\": {\n      \"value\": [\n        {\n          \"values\": [\n            52.7,\n            53.16,\n            53.04,\n            53.0,\n            52.63,\n            52.3,\n            52.52,\n            52.99,\n            52.82,\n            52.95,\n            52.34,\n            53.17,\n            53.25,\n            52.72,\n            52.85\n          ],\n          \"endTime\": \"2020-04-13T14:40:17.344625+00:00\",\n          \"startTime\": \"2020-04-13T14:40:02.344633+00:00\"\n        }\n      ],\n      \"@nextLink\": null\n    },\n    \"valueType\": \"LCeq\"\n  },\n  \"Datastream@iot.navigationLink\": \"http://localhost:8090/v1.0/Observations(737)/Datastream\",\n  \"FeatureOfInterest@iot.navigationLink\": \"http://localhost:8090/v1.0/Observations(737)/FeatureOfInterest\",\n  \"resultTime\": \"2020-04-13T14:40:17.3446045+00:00\"\n}"
    },
    {
      "thingId": 634,
      "datastreamId": "SLM-GW/SLM/Annoyance/MONICA0004_000608_Id6",
      "type": "",
      "personid": null,
      "zoneid": null,
      "phenomenTime": "2020-04-13T14:39:27.828+00:00",
      "observationResult": "{\n  \"@iot.id\": 599,\n  \"@iot.selfLink\": \"http://localhost:8090/v1.0/Observations(599)\",\n  \"phenomenonTime\": \"2020-04-13T14:39:27.828Z\",\n  \"result\": {\n    \"response\": {\n      \"value\": [\n        {\n          \"values\": [\n            1.0\n          ],\n          \"endTime\": \"2020-04-13T14:39:27.8286369+00:00\",\n          \"startTime\": \"2020-04-13T14:38:29.0312705+00:00\"\n        }\n      ],\n      \"@nextLink\": null\n    },\n    \"valueType\": \"Annoyance\"\n  },\n  \"Datastream@iot.navigationLink\": \"http://localhost:8090/v1.0/Observations(599)/Datastream\",\n  \"FeatureOfInterest@iot.navigationLink\": \"http://localhost:8090/v1.0/Observations(599)/FeatureOfInterest\",\n  \"resultTime\": \"2020-04-13T14:39:27.8286159+00:00\"\n}"
    },
    {
      "thingId": 634,
      "datastreamId": "SLM-GW/SLM/LAeq/MONICA0004_000608_Id6",
      "type": "",
      "personid": null,
      "zoneid": null,
      "phenomenTime": "2020-04-13T14:40:17.341+00:00",
      "observationResult": "{\n  \"@iot.id\": 735,\n  \"@iot.selfLink\": \"http://localhost:8090/v1.0/Observations(735)\",\n  \"phenomenonTime\": \"2020-04-13T14:40:17.341Z\",\n  \"result\": {\n    \"response\": {\n      \"value\": [\n        {\n          \"values\": [\n            47.76,\n            47.23,\n            46.95,\n            47.04,\n            47.14,\n            46.8,\n            46.5,\n            46.35,\n            46.18,\n            46.11,\n            46.31,\n            47.3,\n            46.55,\n            46.39,\n            46.8\n          ],\n          \"endTime\": \"2020-04-13T14:40:17.3417129+00:00\",\n          \"startTime\": \"2020-04-13T14:40:02.34173+00:00\"\n        }\n      ],\n      \"@nextLink\": null\n    },\n    \"valueType\": \"LAeq\"\n  },\n  \"Datastream@iot.navigationLink\": \"http://localhost:8090/v1.0/Observations(735)/Datastream\",\n  \"FeatureOfInterest@iot.navigationLink\": \"http://localhost:8090/v1.0/Observations(735)/FeatureOfInterest\",\n  \"resultTime\": \"2020-04-13T14:40:17.3416794+00:00\"\n}"
    }
  ]
}
```
As seen here one thing can have many datastreams and also that the Observations are encoded json that needs to be parsed and is following the OGC Sensorthings API specification. The noOfObservations parameter controls how many historical Observations are retrieved and returned.

### Retrieving all things of a specific thingType together with their observations

One can also retrieve all things of a specific type together with Observations. Locate the 
GET/thingsWithObservation method
![Swagger GetThingWithObservation](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/cop-api-get-thingswithobs.png "Swagger GetThingWithObservation")

Then click on "Try it out" and fill in thingType and noOfObservations with: 
```
thingType Soundmeter
noOfObservations 1
```
**NB!** The API requires a static authentication key:
````
6ffdcacb-c485-499c-bce9-23f76d06aa36
````
Execute the API call by clicking on the Execute button below.

![Swagger GetThingWithObservation](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/cop-api-get-thingswithobsresult.png "Swagger GetThingWithObservation")


