---
layout: default
title: SCRAL integration tutorial <!--- This is required for the page to come in the side pane --->
---
<span style="font-size:2em;">SCRAL integration tutorial</span>
<!-- Using Span is a hack to avoid the title to come again in TOC.-->

<img src="https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/SCRAL-Logo-V1.1.png" alt="SCRAL logo" width="350"/> <br>
This tutorial will help you to understand how to start using SCRAL and how to develop your own SCRAL module.

<!--
## Table of Contents
1. [Prerequisites](#Prerequisites)
2. [SCRAL quickstart with docker-compose](#SCRAL-quickstart-with-docker-compose)
3. [Run SCRAL Python code](#Run-SCRAL-Python-code)
4. [Implement a new SCRAL module](#Implement-a-new-SCRAL-module)
-->

* TOC (Do not remove. This is required to show Table of contents)
 {:toc}


## Prerequisites

### Docker
To start working with SCRAL is necessary to have Docker installed on your machine.
To install the proper version for your operating system, have a look to the [Docker documentation page](https://docs.docker.com/).

### GOST
SCRAL depends on GOST, a [Go](https://golang.org/) implementation of the Sensing OGC [SensorThings API](http://developers.sensorup.com/docs).
To learn more about OGC and GOST visit the [GOST GitHub page](https://github.com/gost/server) or the MONICA tutorial about 
[OGC Historical Data Retrieval & Visualizations](https://monica-project.github.io/sections/gost_retrieval.html).


## SCRAL quickstart with docker-compose
SCRAL is an adaptation framework that contains different integration modules.
Inside SCRAL repository is available a docker-compose folder to help you start working with SCRAL and GOST.

### Quickstart introduction
A user can start a "quickstart" docker-compose file going inside "docker-compose" folder published inside SCRAL repository and running the command:
```bash
$ docker-compose -f <file_name> up -d
```

To have a first start the complete environment (GOST+SCRAL), we suggest starting from "docker-compose.yml" file.

### Before Starting
For running a SCRAL docker-compose, it is necessary that few environmental variables are set.
•	To enable the usage of the other environmental variables is necessary to have variable "CONFIG" sets to value "custom".
•	To start a SCRAL module is necessary to specify the name of the docker image to load (e.g.: monicaproject/scral:glasses)

```docker-compose
scral:
    image: monicaproject/scral:${SCRAL_MODULE}
    container_name: "SCRAL-${SCRAL_MODULE}"
    environment:
        CONFIG: “custom”
```

*Note*: you can run only a quickstart image present inside the [SCRAL archive of MONICA docker-hub](https://hub.docker.com/r/monicaproject/scral/tags).
*Note2*: for certain modules is necessary to specify additional environmental variables, for more details have a look to the [MONICA SCRAL dockerhub](https://hub.docker.com/r/monicaproject/scral).

### Testing SCRAL capabilities
When SCRAL is up and running, it can manage data flow mainly through REST or MQTT messages.
You can interact with SCRAL using the APIs available [here](www.example.org).
<!-- generate and publish Swagger SCRAL API -->

Each SCRAL module with a REST endpoint exposes also a landing page useful both for testing reachability of the endpoint 
and for having a quick overview of the available SCRAL API
(e.g.: for gps_tracker_rest the URL is http://localhost:8000/scral/v1.0/gps-tracker-gw).


## Run SCRAL Python code
SCRAL open source code is available inside [MONICA project repository](https://github.com/MONICA-Project/scral-framework).
It is possible to fork (or simply download) the repository and start working directly on the source code.
As already mentioned, it is necessary to have already started a GOST instance to make SCRAL properly work.
To do that, it is possible to download a docker-compose file from [GOST repository](https://github.com/gost/docker-compose)
or to start the file "docker-compose-gost.yml" contained inside the "docker-compose" folder of SCRAL repository through the command:
```bash
$ docker-compose -f docker-compose-gost.yml up -d
```

### Running a SCRAL module from the source code
To give to developers the possibility to quickly switch between different configuration, SCRAL can work also using configuration files.
The configuration files must be called “preference.json”.
If nothing is specified, in each module folder, the default configuration file must be stored inside "config/local".

When you start working with SCRAL, you can decide if you prefer to modify the content of the default file, or if you want to create a new folder inside the already present "config" folder (e.g.: "config/my_config_folder").

To start the execution just go in the SCRAL main folder and run the following command:
```bash
python <module_name>/<start_module.py> -p <my_config_folder>
```
For example, if you want to start the smart glasses module and you want to store your preferences inside: "smart_glasses/config/test/preferences.json", you can run the following command:
```bash
python smart_glasses/start_smart_glasses.py -p test
```
Note: if the environmental variable CONFIG exists is set to "custom" the configuration file is not read.

#### Python Packages
To work properly SCRAL requires the following Python packages (with the recommended versions):
 - [Eclipse Paho](https://pypi.org/project/paho-mqtt/1.5) 1.5
 - [Flask](https://pypi.org/project/Flask/1.0.2) 1.0.2
 - [CherryPy](https://pypi.org/project/CherryPy/18.1.0) 18.1.0
 - [arrow](https://pypi.org/project/arrow/0.14.2) 0.14.2 (arrow 0.15 not supported)
 - [requests](https://pypi.org/project/requests/2.22.0) 2.22.0
 - [configparser](https://pypi.org/project/configparser/3.7.1) 3.7.1


## Implement a new SCRAL module
The following picture present the high-level architecture of the SCRAL framework.
<img src="https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/SCRAL_architecture.png" alt="SCRAL high level architecture" width="350"/> <br>

To create a new SCRAL module, you can start from the "template_rest" folder and modify it according to your needs.
This folder contains a generic "ready-to-use" SCRAL module that expose a REST <em>resource manager</em> and an MQTT <em>connector</em> (look at the previous picture).

### Step 1: Prepare the OGC Configuration
As already mentioned, SCRAL is strongly connected to the OGC Sensor Things model. To start work with the model I strongly suggest you to have a look at the [official documentation](http://developers.sensorup.com/docs/#sensorthingsAPISensing).
Inside ./template_rest/config you will find the file "ogc_config_template.conf", go there and modify the entities if you need it.

#### OGC MONICA Thing
In our paradigm, an OGC Thing represent a platform (e.g. a gateway, a hub) and should be unique for each SCRAL module.
Close to this parameter you have to specify the number of the other entities (every field is mandatory, but it could be set to 0).

#### OGC MONICA Sensor
In our paradigm, an OGC Sensor represent a class of device --- i.e. not a specific device like the wristband 579 but the generic wristband device. If necessary, you could define many different devices for each module (in our example we will use just one).

#### OGC (Observed) Property
An Observed Property represent a measure that could be observed. E.g.: a location, a temperature, a pressure, etc...
If necessary, you could define many different Observed Property for each sensor, but you will have to assign every property to the right device class (again, in our example we will use just one).

#### OGC Datastream (not part of the ogc_config.conf)
The datastream is the entity that will manage the dataflow. The datastreams should not be modelled in this file because they are generated at runtime.

#### Virtual Entities (Sensor, Property and Datastream)
The Virtual Entities are not part of the OGC Sensor Things API - Sensing. They were introduced to create a distinction between class of Sensor that are used only for sensing and class of Sensor that are used only for send a command (actuate).
When you want to define an Observed Property that will be written (instead of been read), you have to define a Virtual Sensor, a Virtual Property and a Virtual Datastream.

### Step 2: Modify the preferences
As already explained in section "Running a SCRAL module from the source code", if you need different settings, you can go inside folder "./config/local" and modify the content of "preferences.json" or create a new folder with a "preferences.json" file inside.

### Step 3: Checking or adding new REST endpoints
Inside file "start_template_module.py" you can see all the exposed endpoint through Flask.
When you run the "template rest module", a list of the available endpoints could also be reached at the following URL: http://localhost:8000/scral/v1.0/your_module (you can change all the URL going inside file "constants.py" of the template module).

By default, the template module exposes 5 endpoints:
1. testing/documentation (GET): useful to test if the module is correctly running;
1. registering devices (POST): to add new devices in the MONICA IoT platform;
1. deleting devices (DELETE): to remove a device from the MONICA IoT platform;
1. sending observations (PUT): to send measure related to an already registered device;
1. active devices: to have a list of the already registered devices;

Note: the PUT endpoint must be coded to recognize the same Observed Property defined inside the "ogc_config_template.conf" file.

### Step 4: Adding your logic and functionalities
The SCRAL core already provides some basic functionalities that you can use in your own module (like the OGC registration and the interactions with the MQTT broker).

Two functionality that must be coded in each new SCRAL module are:
- the method for registering new datastreams (usually called "ogc_datastream_registration")
- the method for managing new observations received (usually called "ogc_observation_registration")

You can start from the code in "template_rest_module.py" to understand how to code these functionalities.

[... still work in progress ...]
