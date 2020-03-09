---
layout: default
title: <COP UI Tutorial for staff tracking>  <!--- This is required for the page to come in the side pane --->
---
<span style="font-size:2em;">COP UI Tutorial for staff tracking</span>
<!-- Using Span is a hack to avoid the title to come again in TOC.-->
This is a tutorial for how to use the COP (Common Operational Picture) UI and is based on using the [Demonstration of staff management with LoRa based locators](https://github.com/MONICA-Project/staff-management-demo) simulated demonstration.

* TOC (Do not remove. This is required to show Table of contents)
 {:toc}

## Prerequistes
[Demonstration of staff management with LoRa based locators](https://github.com/MONICA-Project/staff-management-demo) needs to be launched in docker, follow the instructions there.
## Introduction
The COP UI is a simple map based interface for displaying the current state of an event. The COP UI is built using predefined Points Of Interest POI, called instance data, and mixing it with sensor derived dynamic information. All the functionality exposed in the COP UI is using the COP API.
## Basic Components of the UI
The user interface is built with a main menu that selects which view the user shown.

![COP UI](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/CNet%20Cop.PNG "COP UI")

In this case we have three modes:
- MAP, which is the active view in this picture
- STAFF, shows the staff view
- LOGOUT, that  will logout the user

The number views depends on the application and can include views for sound and incident management.

## The MAP view functionality
## Zoom and movement of the MAP
In the MAP view the user can zoom in and out of the map and also move the MAP. All this is achieved by using the normal Google Maps interface, i.e dragging the map with the mouse or fingers, zoom by pinching or by using the "+" and "-" controls in the map.

### Filtering of the MAP
Filtering of the MAP allows the user to select what will be shown in the map. Below the map there are dropdown filters where the user can select which items are displayed in the map:

![COP UI Filter](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/Filters.PNG "COP UI Filter")

By clicking or pointing on the different categories the user can toggle which ones are shown in the map. The ones that are "checked" will be displayed in the COP map. Filters can apply both to points of interest as well as other data, in this case there is a categorization of staff that can be filtered on as well.

Additionally, there is a shortcut to see which filters are active, on top of the map there is a filter list of the active filters, i.e. the ones shown on the map (Marked yellow in the image). By clicking or pointing at the "x" for a category it will be immediatelly removed from the map.

## The STAFF view functionality
The STAFF view displays information about which staff is known to the system and which role thay have:
![COPStaffView](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/COP%20Role.PNG "COP STAFF view")
It possible to change the role of a person by changing it in a drop down box, for instance, changin the role to Police from MONICA. This will be reflected in the MAP view and the person will have a different icon.

**NB!** If you test this, remember to enable the filter for the new category.

The staff view in this demonstration is quite simplified, for instance, when the staff tracking is done using smart glasses it has been possible to send direct messages or images to the individual or groups of staff.