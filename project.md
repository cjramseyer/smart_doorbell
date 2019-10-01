**Materials:**

These are the materials/items I used to build this

1. NodeMCU - ESP8266 12E [Amazon](https://www.amazon.com/gp/product/B010N1SPRK/ref=ppx_yo_dt_b_asin_title_o01_s00?ie=UTF8&psc=1)
2. 2 Channel Relay Module [Amazon](https://www.amazon.com/gp/product/B0057OC6D8/ref=ppx_yo_dt_b_asin_title_o06_s00?ie=UTF8&psc=1)
3. AC-to-DC step converter (Qty. 2) [Amazon](https://www.amazon.com/gp/product/B00BXAM694/ref=ppx_yo_dt_b_asin_image_o00_s00?ie=UTF8&psc=1)
4. Jumper wires/header wires [Amazon](https://www.amazon.com/gp/product/B06XRV92ZB/ref=ppx_yo_dt_b_asin_title_o02_s00?ie=UTF8&psc=1)

This project requires ZERO soldering, and can be assembled in about 15-30 minutes.

Purpose: The module intended purpose is to track when the doorbell has been triggered by a visitor.

Use case: We have a large yard (approx. 1 acre) and a relatively long house (60ft. front to back single story ranch) with a deck at the back.  If someone walked to our front door and we are outside with the doorwall closed, we would not hear them ring the doorbell.

The solution: This module monitors when the doorbeel has been triggered front either the front or back door.  Using these two triggers I can track what time the doorbell was triggered.  More importantly, I can use other data (nobody home) and send an alert of our cellphones, trigger the camera to take a picture, etc.


How it works:

The sensor module is based on a NodeMCU ESP3266 12E micro-processor.  This is connected to a 2 channel relay board to act as the triggers for the sensor.  The input of the relay board (to trigger the relays themselves) is connected to an AC-to-DC step-down converter to switch the doorbell from 16v-24v AC to 5v DC voltage.  The relay module can handle higher voltage through the relays themselves, but I am essentially using the relay in reverse to control a dry-contact sensor.  One of the contacts is connected to the normally open (NO) contacts on one relay (i.e. front door).  With no power the relay is open.  When the doorbell is pushed, voltage flows to the doorbell itself (this is 16v-24v AC) AND to the converter module to also send 5v to trigger the relay.  When the relay is triggered, it becomes CLOSED which is picked up by the NodeMCU.


WHY THIS WAY:

If you search the interwebs, there are other example of a smart doorbell project.  I am sure they probably work as well.  However, one of my main goals is to avoid breaking existing functionality by making something smart.  For this one, the sensor module can lose power (for itself), become corrupt, etc. but the basic doorbell functionality will NOT be affected in anyway, I am just "sensing" when someone presses the button.


Step 1 - Build the sensor processor:

Using ESPHone, I flashed the NodeMCU using this config:

binary_sensor:
  - platform: gpio
    pin:
      number: D1
      mode: INPUT_PULLUP
    name: "Front DoorBell"
    device_class: window
    filters:
      - delayed_on: 5ms
  - platform: gpio
    pin:
      number: D2
      mode: INPUT_PULLUP
    name: "Side DoorBell"
    device_class: window
    filters:
      - delayed_on: 5ms

If you haven;t used ESPHome, the config also includes WiFi configurationg, logging, device web server and a restart switch.  You can find the yaml file in the repository with the full config.


Step 2 - Assemble the sensor module:

1.  Attach a header wire from D1 to one side of the normally open (NO) contact on one of the relays on the relay module
2.  Attach a second header wire to one of the GND pins on the NodeMCU and to the other NO contact of the SAME relay on the relay module
3.  Repeat this for the other relay using another GND pin and the D2 pin on the NodeMCU
    NOTE: These become the front and back/side door sensors
4.  Connect each of the AC-to-DC step-down converters on the DC side to the trigger pin on the relay module, do the same for the DC       ground
5.  The AC side of the step-down convert will be what connects to the doorbell itself
6.  Mount this assembly in a project box of your choosing (I have not put mine into a project box yet)

    NOTE: These instructions will be updated when the build is updated
    
Step 3 - Installation

NOTE: A typical house doorbell uses a transformer that is connected to MAINS VOLTAGE (120v AC).  Please use extreme caution.  If possible, turn the doorbell circuit off before the installation.

1.  Locate the doorbell transformer (frequently found in the basement)
    NOTE: The sensor module requires constant power so access to a plug nearby is necessary
    This would probably also work if mounted near the doorbell module itself as long as the assembly can be plugged in to power the NodeMCU
2.  Connect the OUTPUT of the doorbell transformer (16v to 24v NOT 120v) to the input of the step-down converters.
    NOTE: There are TWO step-down converters.  Each convert will have a connection to one leg of the out put from the transformer of the doorbell.  The other leg is connected to the switched leg of each button.
3.  Plug in the USB power supply to the NodeMCU
4.  Connect this to your favorite home automation hub (I use ESPhome via home Assistant)



