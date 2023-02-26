# smart_doorbell
Design, Setup, Install for the Smart Doorbell

[SmartDoorBell](https://github.com/cjramseyer/smart_doorbell) is a repository for the design, build, and installation of a smart doorbell based on an ESP8266 (Arduino or NodeMCU) that is specifically designed to work with legacy doorbell systems.
Typical Smart Doorbells require the replacement of the traditional button and chime.  This design adds smarts to an existing doorbell system.  This can then be integrated with Home Assistant (my choice) or other SmartHome setups such as Hubitat, SmartThings, etc.  This is dependant on ESPHome, but could be adapted to other solutions as well.

These scripts are updated frequently based on numerous requirements from consumers and maintaining and N-1 upgrade strategy.

My office during the day is located in our basement.  If I am on a call and someone rings the doorbell, I am not likely to hear it with my headset on.
I wanted to have an option to enable an automation that would alert me that someone rang the doorbell.
I also wanted to have the ability to send an alert to our phones when we are not home, and show us a camera feed or image.

Using this method, I am able to use our traditional DUMB doorbell (no rewiring necessary)
Plus, I don't need one of the "smart" doorbells, that are either wireless, and totally lacking in privacy, or simply don't function well.
This way, our doorbell can stay just the way it is, and should we move, just take this module with us.

I do my automations using NodeRed, so I have a simple flow to update the last date and time each of the doorbells was rang.
![](images/table%201-1.png)

This can be expanded if necessary for additional doors, and can certainly have additional sensors, I just used 2 of the GPIO pins, but this could easily support 8 of them.

Many scripts and modules live in their own repositories on GitHub. For example, the [HomeAssistant](https://github.com/cjramseyer/hassio) and [NodeRed](https://github.com/cjramseyer/nodered).

## License

Copyright (c) 2018-2023, CJ Ramseyer, All rights reserved.
