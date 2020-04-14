---
layout: default
title: COP UI Tutorial for Security Monitoring  <!--- This is required for the page to come in the side pane --->
---
<span style="font-size:2em;">COP UI Tutorial for Security Monitoring</span>
<!-- Using Span is a hack to avoid the title to come again in TOC.-->

This is a tutorial for how to use the COP (Common Operational Picture) for Security Monitoring using environmental sensors. It uses the [https://github.com/MONICA-Project/DockerEnvironmentSensorDemo](https://github.com/MONICA-Project/DockerSoundDemo) simulated demonstration.

* TOC (Do not remove. This is required to show Table of contents)
 {:toc}

## Prerequistes
[https://github.com/MONICA-Project/DockerEnvironmentSensorDemo](https://github.com/MONICA-Project/DockerSoundDemo) needs to be launched in docker, follow the instructions there.
## Introduction
The COP UI is a simple map based interface for displaying the current state of an event. The COP UI is built using predefined Points Of Interest POI, called instance data, and mixing it with sensor and service derived dynamic information. All the functionality exposed in the COP UI is using the COP.API.
## Basic Components of the UI
The user interface is built with a main menu, to the left, that selects which view the user shown.

![COP UI](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/tut-sec-dashboard.png "COP UI")

In this case we have five modes:
- DASHBOARD, which is the active view in this picture and shows the values from the sound level meters
- SENSORS, for viewing the sensor datastreams
- MAP, shows the MAP view including points of interest and sensor positions.
- ALERTS, That displays the ongoing alerts/incidents
- LOGOUT, that will logout the user

The number views depends on the application

## The DASHBOARD view functionality
The DASHBOARD view shows an overview of the current conditions using the following:
* Vistor Count, showing the number of vistors that have entered (disabled in this demo)
* ALERTS, the number of ongoing alerts
* Windspeed, current value as well as min, max and average.
* Temperature, current value as well as min, max and average. 

The intention is that one can get a quick overview of the current situation from this view.

## SENSORS
In the sensor view shows the values of the individual sensors.
![SENSORS](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/tut-sec-sensors.png "SENSORS")
The history of values are also shown giving a possibility to look at different trends. For each of the sensors also the time of the last measurement is shown.
## The MAP view functionality
![MAP](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/tut-sec-map.png "MAP")

In the MAP view the user can zoom in and out of the map and also move the MAP. All this is achieved by using the normal Google Maps interface, i.e dragging the map with the mouse or fingers, zoom by pinching or by using the "+" and "-" controls in the map.

The map also shows the position of the sensors as well as the point of interest. Below the map there are dropdown list that can be used to select what is rendered on the map.

## The ALERTS view functionality
The ALERTS view displays all the ongoing alerts that have been created by [(DSS)](https://github.com/MONICA-Project/sound-heat-map).

![ALERT](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/tut-sec-alert.png "ALERT")

In this case the windspeed has exceeded the limit and the DSS has created an security incident. In this case the incident includes an intervention plan that which actions should be done. In this case a number of rides should be stopped and some other actions done as well.

The user can choose between dismissing the incident or resolve it. The action chosen is stored with the incident and can later be used to check when the incident started and what the action was.
