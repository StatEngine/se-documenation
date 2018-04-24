# On-Premise Installation

## Overview

The on-premise solution is best suited if you prefer managing all aspects of data, security, and extensions of the platform yourself. The on-premise solution is also useful for experimenting with customizations, developing your own extensions, and utilizing in constrained testing environments. As things can get a bit technical, we only recommend using the on-premise method if you have skilled IT personnel available to setup and support the platform.


## Prerequisites

The on-premise solution is delivered in a [*.box*](https://www.vagrantup.com/docs/boxes/format.html) format.  
Utilizing *.box* and Vagrant provisioning, the on-premise solution can run on Windows, Linux, and OS X operating systems.

The following prerequisites are needed

* [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* [Vagrant](https://www.vagrantup.com/downloads.html)
* [Wget or Curl](https://www.vagrantup.com/downloads.html)

## Quick Start

### Download Latest Release

Lets download the latest release and add to vagrant.
Run the following in your terminal:
```
$ mkdir stat-engine
$ cd stat-engine
$ wget https://s3.amazonaws.com/statengine-public-artifacts/statengine-appliance-latest.box
$ vagrant box add statengine-appliance-latest.box --name statengine/statengine-appliance
```

### Provisioning

It is time to boot up StatEngine.
Run the following from your terminal:
```
$ vagrant init statengine/statengine-appliance
$ vagrant up
```
This command will finish and you will have a virtual machine running StatEngine. You will not actually see anything though, since Vagrant runs the virtual machine without a UI.

### Start Exploring

1.  Open your favorite browser (we recommend [Chrome](https://www.google.com/chrome/)) and navigate to [http://localhost:8080](http://localhost:8080).  You will see the landing page.  

  ![landing](assets/landing.png)

2.  Click the ```Sign In``` button on right side of the top navigation bar.  Login to the application using the following credentials

  > username: ```demo```

  > password: ```password```

  ![signIn](assets/signIn.png)

3.  Click the ```Dashboard``` button to access your the data.  That's it. Simple as that!

  > Screenshot to be supplied.

### Next Steps

For more information on how to use StatEngine, check out the [User Guide](userGuide.md) for more info on how to use the dashboard or checkout some of the other [resources](resources).  

If you want to continue using the on-premise solution to connect and ingesting your own data, follow our advanced guides.


## Advanced

Great, you love StatEngine and you want to start consuming on your data!  This section is intended for developers who to start writing their own normalizers and
ingesting into an On-premise instance of StatEngine.  

## Tutorial - San Francisco Fire Department

For this tutorial, we are going to write our own normalizer to ingest San Francisco Fire Department publicaly available at [DataSF](https://datasf.org/).  The dataset includes fire units responses to calls. Each record includes the call number, incident number, address, unit identifier, call type, and disposition. All relevant time intervals are also included. Because this dataset is based on responses, and since most calls involved multiple units, there are multiple records for each call number. Addresses are associated with a block number, intersection or call box, not a specific address.  The dataset also includes API, which will be useful for polling for recent data.

### Part 1:  Developing your own Siamese plugin

#### Introduction
A *siamese* project is responsible for transforming *raw* source data into a normalized StatEngine data structures as defined by our schemas.  
In our case, the *raw* source data is the data provided by the [DataSF](https://datasf.org/) API, but can come from any RMS or CAD export and in a variety of formats such as XML, JSON, CSV, or flat files.  

Raw fire incident data will vary from source to source, but generally we can expect the data to include geographic locations, timestamp, and other attributes such as incident number, priority level, and information on apparatus responding to the call.

A sample *raw* source file from San Francisco:
```
{
     ":@computed_region_ajp5_b2md": "21",
     ":@computed_region_bh8s_q3mv": "28857",
     ":@computed_region_fyvs_ahh9": "21",
     ":@computed_region_jx4q_fizf": "1",
     ":@computed_region_p5aj_wyqh": "1",
     ":@computed_region_rxqg_mtj9": "10",
     ":@computed_region_yftq_j783": "5",
     "address": "600 Block of POWELL ST",
     "als_unit": false,
     "available_dttm": "2017-10-08T21:32:36.000",
     "battalion": "B01",
     "box": "1361",
     "call_date": "2017-10-08T00:00:00.000",
     "call_final_disposition": "Fire",
     "call_number": "172813828",
     "call_type": "Alarms",
     "call_type_group": "Alarm",
     "city": "San Francisco",
     "dispatch_dttm": "2017-10-08T21:31:12.000",
     "entry_dttm": "2017-10-08T21:31:05.000",
     "final_priority": "3",
     "fire_prevention_district": "1",
     "incident_number": "17118402",
     "location": {
         "type": "Point",
         "coordinates": [
             -122.408784626776,
             37.790494992376
         ]
     },
     "neighborhoods_analysis_boundaries": "Nob Hill",
     "number_of_alarms": "1",
     "original_priority": "3",
     "priority": "3",
     "received_dttm": "2017-10-08T21:29:39.000",
     "rowid": "172813828-T13",
     "station_area": "02",
     "supervisor_district": "3",
     "unit_id": "T13",
     "unit_sequence_in_call_dispatch": "3",
     "unit_type": "TRUCK",
     "watch_date": "2017-10-08T00:00:00.000",
     "zipcode_of_incident": "94108"
}
```
The resulting normalized incident:
> To be supplied.

You will notice the same information appears in both structures, but mapped to different fields.  For example, incident_number, ***17118402*** is mapped to *description.incident_number* in the normalized incident.

You may also notice mapped, but also transformed fields.  For example, the unit_type ***TRUCK*** not only appears under *apparatus[index].unit_type*, but is also *transformed* to ***Truck/Aerial***.

Siamese projects can do any number for mappings, transformations, or other modifications to *raw* source data.

#### Developing your own Siamese project

##### Prerequisites

The following prerequisites are needed

* [node.js](https://nodejs.org/en/)
* [npm](https://www.npmjs.com/get-npm)


1. Install Yeoman

  ```
  npm install -g yo
  ```

2. Install Siamese Generator
  ```
  npm install -g generator-siamese
  ```

3. Generate new Siamese project
  ```
  yo siamese
  ```

> More to follow....


### Part 2:  Ingesting Real-time Data with Spade

> To be supplied.
