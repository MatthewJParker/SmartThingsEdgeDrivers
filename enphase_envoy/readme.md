# SmartThings Edge Enphase IQ Gateway Driver
Reads the current solar generation, battery generation, and grid consumption

## Pre-requisites
- SmartThings hub capable of running Edge platform
- SmartThings account
- SmartThings mobile app
- Enphase IQ Gateway Solar and/or Batteries (Not tested without Batteries)
- Optional: EdgeBridge [By Taustin](https://github.com/toddaustin07/edgebridge) to register token

## Installation Steps
Use my shared projects Edge channel to complete these steps:
1. Enroll hub in my shared test driver Edge channel:  ?
2. Choose to install driver 'Enphase_envoy'
3. Once the driver is installed to your hub, use the "Add device" from your mobile app. Scan for nearby devices on the hub the driver is installed
4. Ensure you have EdgeBridge installed to be able to get a token from enphase web site
5. Change settings to point to your IQ Gateway, obtain the IP by command "ping envoy.local"
6. Change settings to point to your EdgeBridge server
7. Enter the serial number of your IQ Gateway by logining into [Enlighten Manager](https://enlighten.enphaseenergy.com/)
8. THe serial number is seen when selecting "Full System" pull down

#### Note: The IQ Gateway is accessed using a token key, so the intial authentication is performed over the enphase web portal. Once a Token Key is created it is a local access.

### Token Key Alternative
Because of the added complexity of maintaining an EdgeBridge I have created an alternative option to setup your key in the settings. This is split into two parts because the limitation of 255 chars for each text setting. If you leave this blank the default is to use the EdgeeBridge server approach. One thing to note is the key you get from enphase you need to follow these steps:
- Login with your enphase login to the [Enphase Token Generator](https://entrez.enphaseenergy.com/) to generate a token
- Split the token into two parts
- Paste first half into parameter "Token First Part (Max 255 chars)" and second half into parameter "Token Second Part (Max 255 chars)"

### Features
This driver shows the current Battery Charge, and exported, imported, produced, consumed, and charged energy.
A calculation is used to generate an artificial mode no based on the follow criteria, to help with rules:

#### If producing energy and exporting energy and not discharging energy
* 10: "Producing/Exporting"
#### If producing energy and charging energy
* 9: "Producing/Charging"
#### If producing energy and not charging energy and not importing energy and not discharging energy
* 8: "Producing"
#### If producing energy and discharging energy and not importing energy
* 7: "Producing/Discharging"
#### If not producing energy and discharging energy and not importing energy
* 6: "Discharging"
#### If producing energy and discharging energy and importing energy
* 5: "Producing/Discharging/Importing"
#### If producing energy and not discharging energy and importing energy
* 4: "Producing/Importing"
#### If not producing energy and discharging energy and importing energy
* 3: "Discharging/Importing"
#### If not producing energy and not discharging energy and importing energy
* 2: "Importing"
#### If discharging energy and exporting energy
* 1: "Discharging/Exporting"


### Documentation on the enphase local API
If your interested in the features of the local API, some documentation has been created by Enphase [TECHNICAL BRIEF](https://enphase.com/download/iq-gateway-access-using-local-apis-or-local-ui-token-based-authentication-tech-brief#:~:text=NOTE%3A%20Tokens%20are%20valid%20for%20a%20finite%20time.&text=If%20the%20user%20is%20a,is%20valid%20for%201%20year.&text=If%20the%20user%20is%20an,is%20valid%20for%2012%20hours).

