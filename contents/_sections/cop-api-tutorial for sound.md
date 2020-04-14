---
layout: default
title:  COP UI Tutorial for sound monitoring  <!--- This is required for the page to come in the side pane --->
---
<span style="font-size:2em;">COP UI Tutorial for sound monitoring</span>
<!-- Using Span is a hack to avoid the title to come again in TOC.-->

This is a tutorial for how to use the COP (Common Operational Picture) UI and is based on using the [Demonstration of Sound Monitoring an event using Sound Level Meters](https://github.com/MONICA-Project/DockerSoundDemo) simulated demonstration.

* TOC (Do not remove. This is required to show Table of contents)
 {:toc}

## Prerequistes
[Demonstration of Sound Monitoring an event using Sound Level Meters](https://github.com/MONICA-Project/DockerSoundDemo) needs to be launched in docker, follow the instructions there.
## Introduction
The COP UI is a simple map based interface for displaying the current state of an event. The COP UI is built using predefined Points Of Interest POI, called instance data, and mixing it with sensor and service derived dynamic information. All the functionality exposed in the COP UI is using the COP API.
## Basic Components of the UI
The user interface is built with a main menu that selects which view the user shown.

![COP UI](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/tut-sound-slm.png "COP UI")

In this case we have five modes:
- SOUND, which is the active view in this picture and shows the values from the sound level meters
- MAP, shows the MAP view including the calculculated sound heatmap.
- AUDIENCE AREA, that has audience area information
- NEIGHBOUR AREA, shows the neighbour area information
- LOGOUT, that will logout the user

The number views depends on the application and can include views for sound and incident management.

## The SOUND view functionality
The SOUND view shows the "real time" data from the Sound Level Meters at the event. For each of the Sound Level Meters the following are shown:
* 1/3 octave spectra showing the sound pressure levels at different frequencies
* LAeq (A-weighted equivalent in decibels)
* LCeq (C-weighted equivalent in decibels)
* A limit bar that controls the redline in the graphs. 


## The MAP view functionality
### Zoom and movement of the MAP
In the MAP view the user can zoom in and out of the map and also move the MAP. All this is achieved by using the normal Google Maps interface, i.e dragging the map with the mouse or fingers, zoom by pinching or by using the "+" and "-" controls in the map.

### Sound heatmap
The map view for sound shows the calculated sound heat map. The [Sound Heat Map Generator](https://github.com/MONICA-Project/sound-heat-map) genarates the sound heat map using the sound level meters.
![Sound Heat Map](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/tut-sound-heatmap.png "Sound Heat Map")
As one can see there are three active stages at this event.

If the heat map is not shown, check the filter setting so that is selected for display:
![COP UI Filter](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/tut-sound-noheatmap.png "COP UI Filter")

In the map the positions of the SLMs are also indicated. By clicking on the symbol a detail view will be shown with the name and id. There are additional SLMs placed in the neighbouring areas, by zooming out the map these can be seen.
![Detail](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/tut-sound-withdetails.png "Detail")

## The AUDIENCE AREA functionality

The AUDIENCE AREA displays information about sound pressure levels in the audiencie area:
![Audience](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/tut-sound-audiencelimits.png "Audience")
The sound pressure values for dBA and dBC are processed by the Decision Support System [(DSS)](https://github.com/MONICA-Project/sound-heat-map) producing a sliding average over time. Any exceedings of limits will generate incidents from the DSS which are shown in the Exceedings "box".

## The NEIGHBOUR AREA functionality
The NEIGHBOUR AREA displays information about sound pressure levels in the neighbourging areas.
![Neighbour](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/tut-sound-neighbour.png "Neighbour")
It shows the sound pressure level and a 15 minute average. In addition to this it also display the calculated contribution of sound from the different stages. The calculations are done by the [(DSS)](https://github.com/MONICA-Project/sound-heat-map). In this case the limits have been exceeded a number of times and they are shown in the exceedings box.

In addition to the dBA there is also as a view of the calculated octave bands.

![Neighbour](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/tut-sound-neighbouroctave.png "Neighbour")

This also shows the calculated sound contribution from each of stages. You change the selected band by using the drop down list.