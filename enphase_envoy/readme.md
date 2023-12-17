# SmartThings Edge Enphase IQ Gateway Driver
Reads the current solar generation, battery generation, and grid consumption

## Pre-requisites
- SmartThings hub capable of running Edge platform
- SmartThings account
- SmartThings mobile app
- Enphase IQ Gateway Solar and/or Batteries
- Optional: EdgeBridge [By Taustin](https://github.com/toddaustin07/edgebridge) to register token
## Installation Steps
Use my shared projects Edge channel to complete these steps:
1. Enroll hub in my shared test driver Edge channel:  ?
2. Choose to install driver 'Enphase_envoy'

### Enphase device discovery and SmartThings device creation
Once the driver is installed to your hub, use the "Add device" from your mobile app. Scan for nearby devices.

### Features
This driver shows the current Battery Charge, and exported, imported, produced, consumed, and charged energy.
A calculation is used to generate an artificial mode no based on the follow criteria, to help with rules:

If producing denergy and exporting energy and not discharging denergy
        10: "Producing/Exporting"
If producing energy and not charging energy and not importing energy and not discharging energy
        9: "Producing"
If producing energy and charging energy
        8: "Producing/Charging"
If producing energy and not charging energy and not importing energy and not discharging energy
        8: "Producing"
If producing energy and discharging energy and not importing energy
        7: "Producing/Discharging"
If not producing energy and discharging energy and not importing energy
        6: "Discharging"
If producing energy and discharging energy and importing energy
        4: "Producing/Discharging/Importing"
If producing energy and not discharging energy and importing energy
        5: "Producing/Importing"
If not producing energy and discharging energy and importing energy
        3: "Discharging/Importing"
If not producing energy and not discharging energy and importing energy
        2: "Importing"
If discharging energy and exporting energy then
        1: "Discharging/Exporting"


### Documentation on the enphase local API
https://enphase.com/download/iq-gateway-access-using-local-apis-or-local-ui-token-based-authentication-tech-brief#:~:text=NOTE%3A%20Tokens%20are%20valid%20for%20a%20finite%20time.&text=If%20the%20user%20is%20a,is%20valid%20for%201%20year.&text=If%20the%20user%20is%20an,is%20valid%20for%2012%20hours.

