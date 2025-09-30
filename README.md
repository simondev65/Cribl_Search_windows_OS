# Cribl Search Windows OS
----

This pack is for 

* windows eventlogs data
* process events (sysmon)
* [system_state](https://docs.cribl.io/edge/sources-system-state/) input from  Cribl Edge Agent (or splunk winhostmon input)
* Active Directory logs

it allows you to :
* parse windows event from XML
* parse windows event from classic format
* get instant analytics on eventcode, host issues, user behavior
* build an asset list
* Get mitre attack alignement with eventID
* and much more

## About this Pack

This pack assumes you are windows event logs in _XML_ or _classic_ format. (Set datatype to `Microsoft Windows Datatypes`)
* You could also parse the events to json before sending to lake and search. If you do so  `set a json datatype` to your dataset.



## Deployment. MUST READ

After installing this Pack :

**Step 1:**
choose a dataset to send your windows event to. (if you are using cribl lake, create a lake dataset first). Once created set the datatype to "windows_datatype_for_pack"  (you can find it inside the pack). This is mandatory for cribl search to parse the XML or classic windows event.

**step 2:**
 configure the macros depending on your data available : 
    set macro  "windows_log_dataset" for windows events to point to your log dataset. This is assuming you have only 1 dataset for your windows events.
    set macro "windows_state_dataset" for system state. You can get [system_state](https://docs.cribl.io/edge/sources-system-state/) input from  Cribl Edge Agent, or use winhostmon input from a Splunk universal Forwarder, etc..
    set macro "windows_process_dataset" for your sysmon events.
    set macro "windows_ad_dataset" to point to your Active directory logs dataset.

**Step 3 :**
run the saved search. "windows_assets" to build the host list. Let it run, not seeing result is normal. search ${search_windows_assets} to verify it completed

**Step 4 :** 
[schedule](https://docs.cribl.io/api/save-search-get-alerts/#schedule-search) this savedsearch search to run every day.

OPTIONAL : 
Step 4 : 
In macros, set the dataset for the [system_state](https://docs.cribl.io/edge/sources-system-state/) data

## Advanced setup

**Security**

Adjust suspicious eventcode to your liking in the macros : suspicious_EventID

**Other sources**

If you collect other sources such as *Windows Update Log*, we recommend you set a field dataType=WindowsUpdateLog for this source (you can do so in Cribl Edge or Stream) and send these logs in the win event log dataset. Adjust the Windows_Update_Log macro accrodingly.

## Upgrades

Empty for now

## Release Notes



### Version 0.1.0 - 2025-10-05

Initial release for windows event log, process event, system state and AD logs

## Contributing to the Pack
 

To contribute to this Pack,  DM on Cribl community slack : Simon_cribl.io
 [Cribl Community Slack](https://cribl-community.slack.com).

## Contact
To contact us please email sduchene@cribl.io

## License
All publicly posted Packs must include a license that allows for use by the general public, such as Apache 2.0, MIT, or GNU.
(Most Packs use the Apache 2.0 license.)

This Pack uses the following license: [`Apache 2.0`](https://github.com/criblio/appscope/blob/master/LICENSE).