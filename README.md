**Install Thingernet Thermostat in sonoff NS Panel**

Disclaimer:

DO IT ONLY IF YOU HAVE SOME EXPERIENCE WITH THAT KIND OF DEVICE AND YOU
ARE FAMILIAR WITH THE FOLLOWING PROCEDURE.

USE UNDER YOUR RESPONSIBILITY. NOTICE THAT YOU CAN BRICK THE DEVICE.
I'll not be responsible in any way for this. I've warned you....

**Useful links:**

-   <https://github.com/ppernias/thingernet_thermostate> (repository)

-   <https://raw.githubusercontent.com/ppernias/thingernet_thermostate/master/nspanel_mikasa.tft>
    (NSPanel Firmware). Optional. You can use WWW directory in HA or
    another local URL removing/adding comments to the code.

**Information you'll need:**

**From HA configuration of sensors/switches**

-Device Name. The name you want to assign to the Thermostat Esp entity

-Room: the name of the room the thermostat will be installed. This text
will be exposed on the top part of the thermostat screen

\- **Climate entity** in HA you want to associate with the thermostat

\- **Heater switch** to activate with the thermostat.

        *Notice that in the climate entity, there is another piece of information you'll need: heater switch entity.*
        *After the installation, if you are using the internal temperature sensor in the NSPAnel you'll need to change*
        *the temperature sensor entity in the YAML code for the climate entity associated in your HA climate section.*

-   *HOTWATER recirculation pump switch.*

-   *HOTWATER boolean switch entity.*

-   *Outdoor Temperature Sensor entity*

-   *IP you want to assign the the thermostat*

-   *Temperature sensor entity of main heating system entity*

-   *Temperature sensor entity for HOTWATER return*

**In your SECRETS in ESPHOME:**

-   *wifi_password*

-   *wifi_ssid*

-   *opta_password*

**Finally:**

*The password you want to use for the thermostat web server*

Installation:

1.- Download **esphome_mikasa.yaml** and change all CHANGEME texts in
the code.

2.- Create a new esphome entity in HA (use the name you want to use in
device_name.

3.- copy Encryption key (don't worry is a temporal issue)

4.- If you have decided the fixed IP you want to use, skip to step 6

5.- install the code in NSP using the regular procedure. (Plug into This
Computer section)

-wait until "Download Project" finishes, download the project

\- Open Esphome Web and upload the firmware to the NSPanel

6.- Power the NSP (remember, 5v) and check the log in EspHome console
for this device. Take note of the IP assigned. At this point, **do not
add the device to the HA**, even if it has been discovered.

7.- edit the code of your device in ESPHOME by removing ALL the code and
substituting it with the modified code you have prepared on point 1.
Update it with the fixed IP you want to use.

8.- upload the new firmware using the same procedure as in point 5

9.- Power on the device. The NSP will show the original sonoff screen
BUT you'll heard the start-up melody in the buzzer. Now you have to add
the device to the Home Assistant Installation. If you want, you can
check the logs. All switches and sensors will be listed.

10.- if the HA has discovered the device, add it to the ESPhome
integration. If Not, do it manually by adding an ESP device and using
the IP you know for the device. The new device won't ask for any
encryption key.

11.- check the device in the ESPHOME integration by clicking on DEVICE
and go to Update TFT display. Switch on it once and the NSP screen will
start the download firmware for the screen configuration. It takes some
minutes. DO NOT POWER OFF the device at this point or you'll brick the
device.

12.- After the screen (actually is a Nextion screen) firmware has been
download, the NSP will restart and connect to your wifi and to your HA.
Check again the ESP integration for this device and take note of the
entity for the temperature sensor. It will be somethig like
"sensor.DEVICE_NAME_temperature".

Change the your climate settings for this thermostat in the
"target_sensor" section and update climates in your HA configuration.

That's all!
