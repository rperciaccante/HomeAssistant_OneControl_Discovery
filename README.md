HomeAssistant_OneControl_Discovery
=========================================

### About

This is a project that is designed to utilize Node Red to connect to your Lippert OneControl cloud bridge and download the entities into your Home Assistant instance, allowing you to control most items in your RV.

This has been tested on my 2021 Grand Design Momentum 397TH-R.  Additional samples are always appreciated.

### Requirements
- MUST have a network that contains the OneControl Cloud Bridge (even if you are not subscribed to the cloud service)
- Home Assistant installed and attached to the network inside your RV.
- MQTT Discovery must be enabled on your Home Assistant instance: https://www.home-assistant.io/docs/mqtt/discovery/
- MQTT broker 
- Node Red installed as a service on same device as your Home Assistant instance (recommend the official Home Assistant add-on)
- "SSE-Client" node must be installed from the hamburger menu -> Manage Pallette -> Install.  Details can be found here - https://flows.nodered.org/node/node-red-contrib-sse-client

### How it Works

#### Downloading and installing
Download the "flows.json" file.  In your Node Red instance, from the hanburger menu, select "Import" and then "Select a file to import".  Select the "flows.json" file you downloaded, and import.

#### About the Discovery process
Please note that there are three flows in this config:
- OneControl - Improved Discovery
  - Referred to hereafter as "Discovery" flow
  - This is used to connect to your OneControl system and create the necessary Home Assistant entities
  - This created the needed entities and inserts them into Home Assistant via MQTT discovery
- OneControl - Command and Event Stream
  - Referred to hereafter as "Monitor" flow
  - This flow connects to the OneControl event stream to download state information via SSE-Client
  - State information is transformed as necessary and published to the appropriate MQTT topics
  - MQTT is also monitored for commands from Home Assistant that are then sent to OneControl via HTTP
- Tools
  - This flow contains useful tools to help in troubleshooting and enahancements.

Inside the Discovery flow, there is a node named "Process Configuration" and it contains a number of tools available to you.  Please familairize yourself
with the options before running the tool.

### Limitations:
- Physical devices such as slides and awnings are NOT currently supported due to the complexity of the integration and the risks associated with the potential for damage.
