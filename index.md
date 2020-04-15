---
layout: default
---

# MONICA Development Toolbox
Sound and security applications for large, open-air events in the city using IoT-enabled devices such as smart wristbands, video cameras, sound level meters and mobile phones.

The MONICA project was a large-scale demonstration of new and existing IoT applications, see https://www.monica-project.eu/ for more information.

The MONICA Development Toolbox consists of:
* Tutorials, see left column.
* Packages, which are ready to go complete environments based on Docker that immediately are runnable and also contain simulated data sources.
* Resusable tools and components which are mostly Open Source.
* Third party tools that have been used and tested by the MONICA project at different pilot and worked well.

## Packages

### Staff Management
[Staff management package]( https://github.com/MONICA-Project/staff-management-demo)

### Monitor crowd based on capacity
[Crowd management using smart wristbands and cameras](https://github.com/MONICA-Project/DockerGlobalWristbandSimulation)

### Sound monitoring
[Sound Monitoring an event using Sound Level Meters](https://github.com/MONICA-Project/DockerSoundDemo)

### Safety incidents
[Managing weather related incidents Demo](https://github.com/MONICA-Project/DockerEnvironmentSensorDemo)

## MONICA Platform Tools
### Generic Tools
  1. [High Level Data Fusion and Anomaly Detection Module (HLDFAD)](https://github.com/MONICA-Project/HLDFAD_SourceCode)
  2. [The Smart City Resource Adaptation Layer (SCRAL)](https://github.com/MONICA-Project/scral-framework)
  3. [Decision Support System (DSS)](https://github.com/MONICA-Project/DSS)
  4. Common Operational Picture COP Tools.
     * [COP UI](https://github.com/MONICA-Project/COP-UI) - The generic MONICA COP user interface.
     * [COP APi](https://github.com/MONICA-Project/COP.API) - The MONICA COP API.    
     * [COP Updater](https://github.com/MONICA-Project/COPUpdater) - Is the link between the COP and the IoT Devices, pushing individual updates to the COP.    
     * [COP DB](https://github.com/MONICA-Project/COP.DB) - The MONICA COP DB used for storing the state of the COP.
     
### Sound 
  1. [Sound Heat Map Generator](https://github.com/MONICA-Project/sound-heat-map)
### Cameras
  1. [Security Fusion Node SFN](https://github.com/MONICA-Project/sfn)
  2. [VCA Core](https://github.com/MONICA-Project/sfn/blob/master/VCAcore_Installation.md)
### Wearables
  1. [ORA Smartglasses](https://github.com/MONICA-Project/MonicOra)
  2. [Staff Management application](https://github.com/MONICA-Project/map-project)
  3. [LoTrack (LoRaWAN trackers)](https://github.com/MONICA-Project/LoTrack)
  4. [RIOT-OS based GPS tracking devices using LoRaWAN](https://github.com/MONICA-Project/lorawan-tracker)
### Simulators
  1. [OGC Sensorthings Observation Replayer](https://github.com/MONICA-Project/observation-replayer)
  2. [OGC Sensorthings Observation Simulator](https://github.com/MONICA-Project/RunSimulation)
  3. [Smart Wristband Simulator](https://github.com/MONICA-Project/WristbandGwMqttEmulator)
### Developer Tools
  1. [SignalR Listener](https://github.com/MONICA-Project/WristbandGwMqttEmulator)
## Third Party Tools  
  1. [mqttFx](https://mqttfx.jensd.de/) MQTT Client for debugging
  2. [HeidiSQL](https://www.heidisql.com/) Database Access
  3. [mosquitto](https://mosquitto.org/) MQTT Broker
  4. [GOST](https://www.gostserver.xyz/) OGC Sensorthings API database


