# Elasticsearch First Steps

This is the project and resources accompnaying the Elasticsearch First Steps Live Online Ttraining on O'Reilly on 11th May 2020. 

https://learning.oreilly.com/live-training/courses/elasticsearch-first-steps/0636920387459/

## Installation 

Follow the steps below to install and get your Elasticsearch and Kibana up and running.

### Download Software

Visit elastic.co/downloads for set of downloads

Software | Version | Link
------------ | -------------| -----------
Elasticsearch | 7.6.2| https://www.elastic.co/downloads/elasticsearch
Kibana | 7.6.2|https://www.elastic.co/downloads/kibana

Click on the Downloads for the appropriate binary for your Operating System. *We use Binary/Archive for this class* 

### Install Elasticsearch on Windows OS
This step is for Windows OS, please look at the Elastic link for the instructions for other OSs.

* Unpack the binary to your favourite folder
* cd <ELASTICSEARCH_INSTALL_DIR>/bin
* Execute the batch file:
`elasticsearch.bat`
You will see a message like 'Server started' in the command prompt console.

### Sanity Test
Once the server was up and running, let's check out the status by visiting `http://localhost:9200` on your internet browser. This should provide a JSON respone on the browser like the following:
````JSON
{
  "name" : "HOMESERVER",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "hqNGMOhIRfKhW0tTMAHbyw",
  "version" : {
    "number" : "7.6.2",
    "build_flavor" : "default",
    "build_type" : "zip",
    "build_hash" : "ef48eb35cf30adf4db14086e8aabd07ef6fb113f",
    "build_date" : "2020-03-26T06:34:37.794943Z",
    "build_snapshot" : false,
    "lucene_version" : "8.4.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
````
Now, let's test the Kibana tool too, as mentioned in the next section.

### Install Kibana on WindowsOS

* Unpack the Kibana binary to your favourite folder
* cd <KIBANA_INSTALL_DIR>/bin
* Execute the batch file:
`kibana.bat`

You will see a message like below in the command prompt console.
````
  log   [12:41:36.302] [info][listening] Server running at http://localhost:5601
  log   [12:41:36.453] [info][server][Kibana][http] http server running at http://localhost:5601
````
![Kibana Web Application ](/images/kibana_command_prompt.png)

### Sanity Test
Once the Kibana web app was up and running, visit `http://localhost:5601`. This should take you to a Web UI, home of Kibana. If you see a beautiful UI on your browser, your Kibana tool is all set and ready to go!

## Checking the state of the cluster

Let's issue a simple command to check the state of the cluster. Go to Kibaba, on your DevTools tab (left hand menu), enter the following API call:
```json
GET _cluster/health
```
This should respnd with
```json
{
  "cluster_name" : "elasticsearch",
  "status" : "yellow",
  "timed_out" : false,
  "number_of_nodes" : 1,
  "number_of_data_nodes" : 1,
  "active_primary_shards" : 16,
  "active_shards" : 16,
  "relocating_shards" : 0,
  "initializing_shards" : 0,
  "unassigned_shards" : 10,
  "delayed_unassigned_shards" : 0,
  "number_of_pending_tasks" : 0,
  "number_of_in_flight_fetch" : 0,
  "task_max_waiting_in_queue_millis" : 0,
  "active_shards_percent_as_number" : 61.53846153846154
}
```

The `yellow` status indicates you have no replicas for your shards available. That is, should your Elasticsearch vanishes off, you'll be loosing all the data. Let's see if we can start a new node but on the same machine and using the same binary (you wouldn't do the same on PROD environment though!)

### Starting a Second Node Using the Same Binary

If you wish to start a new node on the same host using the same binary, we need to provide couple of additional arguments to the script -  the data and logs path directories.

Provide those paths as command line arguments to the script as shown below and execute the command:

`elasticsearch -Epath.data=c:\dev\temp\data -Epath.logs=c:\dev\temp\logs`

This will start the additional node in the server 


