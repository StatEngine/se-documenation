# Definitions

Some departments calculate `response time`, `event time`, `alarm handling` or other metrics differently than others.
To avoid confusion and to assure complete transparency, this section serves as a dictionary of common terms and calculation definitions in StatEngine.
StatEngine, in general, follows terminology and calculations set forth in NFAP [1710](https://www.nfpa.org/Codes-and-Standards/ARCHIVED/Safer-Act-Grant/NFPA-1710)/[1720](https://www.nfpa.org/Codes-and-Standards/ARCHIVED/Safer-Act-Grant/NFPA-1720) guidelines.


## Timestamp Fields

Field | Description
------------ | -------------
description.psap_answer_time| PSAP call is answered
description.event_opened | Incident is created in CAD
description.first_unit_dispatched | Earliest unit dispatched
description.first_unit_enroute | Earliest unit enroute
description.first_unit_arrived | Earliest unit arrived on scene
description.event_closed | Incident is closed in CAD


## Calculated Durations

***Alarm Transfer:*** The time interval from the receipt of the emergency alarm at the PSAP until the alarm is first received at the communication center.

<span style="color:red">StatEngine does not currently support the measurement of transfer time.  Therefore all values will be 0.</span>

<hr>
***Alarm Answering:*** The time interval that begins when the alarm is received at the communication center and ends when the alarm is acknowledged at the communication center.

<span class="formula"> alarm_answering_duration = event_opened - psap_answer_time </span>

<hr>
***Alarm Handling:*** The time interval from the receipt of the alarm at the primary PSAP until the beginning of the transmittal of the response information via voice or electronic means to emergency response facilities (ERFs) or the emergency response units (ERUs) in the field.

<span class="formula"> alarm_handling_duration = first_unit_dispatched - event_opened </span>

<hr>
***Alarm Processing:***
The time interval from when the alarm is acknowledged at the communication center until response information begins to be transmitted via voice or electronic means to emergency response facilities (ERFs) or the emergency response units (ERUs).  

<span class="formula"> alarm_processing_duration = first_unit_dispatched - psap_answer_time </span>

<hr>

***Turnout:***
The time interval that begins when the emergency response facilities (ERFs) and emergency response units (ERUs) notification process begins by either an audible alarm or visual annunciation or both and ends at the beginning point of travel time.  

<span class="formula"> turnout_duration = first_unit_enroute -  first_unit_dispatched </span>

<span style="color:orange"> Note: This calculation does not imply the first unit enroute was also the first unit dispatched.  It is simply the period of time before the first unit is enroute after *ANY* unit has been dispatched.  Per-unit turnout calculations are also calculated.</span>

<hr>
***Travel:***
The time interval that begins when a unit is enroute to the emergency incident and ends when the unit arrives at the scene.

<span class="formula"> travel_duration = first_unit_arrived -  first_unit_enroute </span>

<span style="color:orange"> Note: This calculation does not imply the first unit arrived was also the first unit enroute.  It is simply the period of time before the first unit arrives after after *ANY* unit has been enroute.  Per-unit travel calculations are also calculated.</span>

<hr>
***Total Response:***
The time interval from the receipt of the alarm at the primary PSAP to when the first emergency response unit is initiating action or intervening to control the incident.

<span class="formula"> total_respsonse_duration = first_unit_arrived -  psap_answer_time </span>

<hr>
***Total Event (Not defined by NFPA):***
The time interval from the incident creation in CAD to when the incident is closed in CAD.

<span class="formula"> total_event_duration = event_closed -  event_opened </span>
