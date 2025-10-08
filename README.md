# Cribl Search Windows OS
----

Greetings!
This search pack is for 

* Windows eventlogs data
* process events (sysmon)
* [system_state](https://docs.cribl.io/edge/sources-system-state/) input from  Cribl Edge Agent (or Splunk winhostmon input)
* Active Directory logs

It allows you to :
* Parse Windows event from XML
* parse Windows event from classic format
* get instant analytics on eventcode, host issues, and user behavior
* build an asset list
* Get mitre attack alignment with eventID
* and much more

## About this Pack

This is for Cribl Search.

This pack assumes you are receiving Windows event logs in XML or classic format, in an unparsed format (recommended).
* Data collection can be done with [Cribl Edge](https://docs.cribl.io/edge/usecase-windows-observability/) or third party (Elastic agent, NXlog, Splunk UF...) 
* If you decide to parse the events to json before sending to the lake and search : set a json datatype to your dataset.



## Deployment. MUST READ

After installing this Pack :

**Step 1:**
Choose a dataset to send your Windows event to. This search pack assumes you will be grouping multiple datasets: 
* Windows events logs: This dataset is getting those journals: WinEventLog://Application, WinEventLog://Security, WinEventLog://System, WinEventLog://ForwardedEvents
* system state: This dataset is getting either Cribl Edge Agent [system_state](https://docs.cribl.io/edge/sources-system-state/) input, windows update log (collect $WINDIR\WindowsUpdate.log),  or those inputs from a Splunk universal Forwarder  winhostmon, winprintmon, win update ( default data sent to the windows index, [see table](https://help.splunk.com/en/splunk-it-service-intelligence/content-packs-for-itsi-and-ite/windows-dashboards-and-reports/1.4/content-pack-for-windows-dashboards-and-reports/get-windows-server-data#ariaid-title3)
* Windows processes: sysmon events
* Active Directory: if you are using Splunk Universal Forwarder, and following [this input-to-index setting](https://help.splunk.com/en/splunk-it-service-intelligence/content-packs-for-itsi-and-ite/windows-dashboards-and-reports/1.4/content-pack-for-windows-dashboards-and-reports/get-windows-server-data#ariaid-title3), the inputs toward the msad index are typically the source needed for this dataset
    
Create the dataset and assign the datatype : 

In Cribl Lake, create the datasets.
In Cribl search->data->dataset [assign the datatype](https://docs.cribl.io/search/set-up-azure-blob/#process-accel) to "windows_datatype_for_pack"  (you can find it inside the pack). This is mandatory for Cribl search to parse the XML or classic Windows event.

**step 2:**
 configure the macros depending on the data available : 
 * Windows events logs : set macro  "windows_log_dataset" for Windows events logs  to point to the dataset you chose in step 1.
 * system state : set macro "windows_state_dataset" for system state. You can get [system_state](https://docs.cribl.io/edge/sources-system-state/) input from  Cribl Edge Agent, or use winhostmon, winprintmon input from a Splunk universal Forwarder, etc..
 * Windows processes : set macro "windows_process_dataset" for your Sysmon events.
 * Active Directory: Set macro "windows_ad_dataset" to point to your Active Directory logs dataset. I

**Step 3:**
Run the saved search. "windows_assets" to build the host list. Let it run; not seeing any result is normal. search ${search_windows_assets} to verify it completed

**Step 4:** 
[schedule](https://docs.cribl.io/api/save-search-get-alerts/#schedule-search) this savedsearch search to run every day.

OPTIONAL : 
Step 4 : 
In macros, set the dataset for the [system_state](https://docs.cribl.io/edge/sources-system-state/) data

## Advanced setup

**Security**

Adjust suspicious eventcode to your liking in the macros : suspicious_EventID

**Other sources**

If you collect other sources such as *Windows Update Log*, we recommend you set a field dataType=WindowsUpdateLog for this source (you can do so in Cribl Edge or Stream) and send these logs in the Windows Event log dataset. Adjust the Windows_Update_Log macro accordingly.

## Upgrades

Empty for now

## Release Notes



### Version 0.9.0 - 2025-10-05

Initial release for Windows event log, process event, system state, and AD logs

## Contributing to the Pack
 

To contribute to this Pack,  DM on Cribl community Slack: Simon_cribl.io
 [Cribl Community Slack](https://cribl-community.slack.com).

## Contact
To contact us please email sduchene@cribl.io

## License


This Pack uses the following license: [`Apache 2.0`](https://github.com/criblio/appscope/blob/master/LICENSE).