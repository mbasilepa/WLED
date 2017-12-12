## Welcome to my project WLED!

WLED is a basic, fast and (relatively) secure implementation of a ESP8266 webserver to control Neopixel (WS2812B) leds

Uses ESP Arduino core version 2.3.0 (latest as of December 2017).

### Features: (V0.4)
- RGB, HSB, and brightness sliders
- Settings page - configuration over network
- Access Point and station mode - automatic failsafe AP
- WS2812FX library integrated for over 50 special effects!
- Secondary color support lets you use even more effect combinations
- Support for RGBW strips
- 25 user presets! Save your favorite colors and effects and apply them easily!
- Nightlight function (gradually dims down)
- Notifier function (multiple ESPs sync color via UDP broadcast)
- Support for power pushbutton
- Custom Theater Chase
- Full OTA software update capability
- Password protected OTA page for added security (OTA lock)
- Alexa smart home device server
- (unstable) NTP and experimental analog clock function
- client HTML controlled
- Edit page. Change html and other files via OTA. (needs to be enabled in source)

### Compile settings:
- Board: WeMos D1 mini (untested with other HW, should work though)
- CPU frequency: 80 MHz
- Flash size : 4MB (3MB SPIFFS)
- Upload speed: 921600

### Quick start guide:

- If you do not plan to change the software, you can use the supplied binary files instead-
Just flash a [basic HTTP OTA updater](https://github.com/Aircoookie/ESP8266MinimalHTTPUpdater) sketch and upload the bin!

1. Connect a  WS2812B RGB led strip to GPIO2. Optionally connect a NO-pushbutton to GPIO0 (internal pull-up) and ground.

2. Follow a guide to setup your Arduino client (I am using version 1.8.1) with the ESP8266 libraries.
For current compiles I use version 2.3.0.

3. In file "wled00.ino", you should change the access point and OTA update passphrases for added security (you can change them later, this is just the "factory default"). Flash the sketch.
You will need to install the NeoPixelBus library by Makuna. All other dependencies are included with WLED for convenience.

5. Connect to automatically started WiFi access point "WLED-AP" using default passwort "wled1234". Go to the IP "192.168.4.1".

6. Click on the cog icon to edit settings like connecting the module to your home WiFi.

7. Have fun with the software!

### Advanced module control via HTTP requests API:

See the [wiki](https://github.com/Aircoookie/WLED/wiki/HTTP-request-API)!

### Other

Licensed under the MIT license 
Uses libraries: 
ESP8266 Arduino Core
NeoPixelBus by Makuna
[WS2812FX](https://github.com/kitesurfer1404/WS2812FX) by kitesurfer1404 (Aircoookie fork)
Time library
Timezone library by JChristensen
arduino-esp8266-alexa-multiple-wemo-switch by kakopappa

Uses Linearicons by Perxis! (link in settings page)

#### This information will be moved to the wiki soon:

Software update procedure:

Method 1: Reflash the new update source via USB.

Method 2: The software has an integrated OTA software update capability.
First you have to enable it by typing in the correct OTA passphrase (default: "wledota") in the settings menu.
Remove the tick in the checkbox "OTA locked". Then save settings and reboot the ESP.
Now you can go to "<moduleip>/update" to update binary firmware.
After you are done, it is recommended to lock the OTA function again.
To do so, tick the checkbox again (you can change the passphrase by typing in a new one now). Reboot.
If you try to access the update page now, you should see the message "OTA lock active".


The software now supports audio-reactive-led-strip!

1. Download [audio-reactive-led-strip](https://github.com/scottlawsonbc/audio-reactive-led-strip) and follow its installation instruction. Use python 3!
2. Insert the following code in led.py after line 66:
    m.append(1);
    m.append(2);
3. In config.py set your led amount, ESP IP and WLED UDP notifier port. For FPS, a setting between 15-30 is recommended.
4. Run visualization.py! If you have a low amount of LEDS (e.g. 10) try lowering the sigma values in line 129-131.
5. If you have multiple WLED devices, you can sync them all with music.
Use the led count of your largest device and set the IP to X.X.X.255 (UDP broadcast).
You can adjust the position of the amplitude with the WARLS offset setting.
Note that there is currently an issue preventing you from accessing the control web page while the script is running. HTTP requests work.






