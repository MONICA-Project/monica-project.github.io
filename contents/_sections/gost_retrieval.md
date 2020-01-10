---
layout: default
name: OGC Historical Data Retrieval & Visualizations
---

# OGC Historical Data Retrieval & Visualizations
This tutorial is guides through the methods of fetching or visualizing the data stored in [GOST based OGC server](https://github.com/gost/server).

## Table of Contents
1. [Fetch Using OGC Server](#Fetch-Using-OGC-Server)
2. [Fetching Directly from PostgreSQL](#Fetching-Directly-from-PostgreSQL)
3. [Visualization Using Grafana](#Visualization-Using-Grafana)

## Fetch Using OGC Server
This approach is most suited when you are developing an application following OGC specification. The RESTful requests can follow the conventions as shown in the OGC specification.

Depending on the use cases, specific Observation or metadata can be fetched.

### A sample Python code to fetch OGC observations belonging to a datastream
```python
import requests
import pandas as pd
import sys
 
baseUrl = "http://example.com:8092/v1.0"  #Change it accordingly
dataStreamID = "54" #Change it accordingly
observations = requests.get(baseUrl+"/Datastreams("+dataStreamID+")/Observations?$count=true").json()
 
num_entries = observations['@iot.count']
values = observations['value']
 
 
df = pd.DataFrame(values)
skip = len(values)
 
while skip < num_entries :
    url = baseUrl+"/Datastreams("+dataStreamID+")/Observations?$skip="+str(skip)
    observations = requests.get(url).json()
    tempdf = pd.DataFrame(observations['value'])
    df = df.append(tempdf)
    skip += len(observations['value'])
    print("reading:"+str(skip))
 
     
df.to_csv('C:\\Your\\file\\Path.csv')
```
The above code can be extended to fetch all the observations belonging to a Thing, Sensor ,featureOfInterest, ObservedProperty or a Location. Or even with advanced filters.

eg: to get data after some time :
```
http://example.com:8092/v1.0/Datastreams(48)/Observations?$filter=resulttime%20lt%20%272018-09-11T21:15:00%27
```
Some more fancy query options can be found in [Sensorup](http://developers.sensorup.com/docs/) documentation.

## Fetching Directly from PostgreSQL
**Caution**: Be sure about what you are doing. Please make sure you do not modify the database or schema while fetching the data!!

This approach is suited when you just want to have a overview of the data without worrying much about the implementation aspects. Especially when the OGC server is not running for the Pilot you are expecting the data from.

One approach we tried and tested is wih the help of pgAdmin that can be downloaded and installed from [here](https://www.pgadmin.org/download/). 

1. Run PdAdmin. It will open a browser (or open http://localhost:5432 by default)
2. Object →Create → server  
  2.1. Give a name you like in "General" tab  
  2.2. In connection Tab give host name, enter user name and password  
  2.3. Press "Save button"
3. Now you have a connection
4. Now for custom queries go to "Tools→Query tool" and execute queries

## Visualization Using Grafana
![PostgreSQL data source](https://grafana.com/grafana/plugins/postgres) for grafana helps in visualizing the GOST data.

![Create datasource](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/Grafana_datasource.png)

Create a new dashboard and add a panel with a graph (refer to the Grafana documentation for details):

![Create dashboard](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/grafana_create_dashboard.png)


![Create panel](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/grafana_create_panel_with_graph.png)

Edit the panel:

![Edit panel](https://github.com/MONICA-Project/monica-project.github.io/raw/master/assets/img/grafana_edit_panel.png)

Then choose your Postgres data source and add the SQL. For a time series query, one column has to be named "time".

Timestamps in the Postgres database are UTC. In the settings of the Grafana dashboard you can tell Grafana to stick with UTC or to convert to local browser time. Make sure your dashboard displays the correct time period.

I would advise to use an SQL client (e.g. pgAdmin) to browse the GOST database to learn about the tables available. Here is an SQL example for a graph:

Observations per minute
```sql

SET timezone TO 'UTC';
select
to_timestamp(data->>'phenomenonTime','YYYY-MM-DD"T"HH24:MI') as time,
count(*) as observations
FROM v1.observation obs
-- join to stream and thing so you can add a suitable where clause if needed
join v1.datastream str on obs.stream_id = str.id
join v1.thing thi on str.thing_id = thi.id
group by time
order by time asc;
```

Refer to the [Postgres documentation](https://www.postgresql.org/docs/current/functions-json.html) to learn how to retrieve the data you want from the JSON object stored in table "observation".