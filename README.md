# ZeroAPS
Use a Raspberry Pi Zero an a few other products to build your compact close loop with [OpenAPS](https://openaps.org)

## What you will need
*(Everything in [ ] is only used for the initial setup)*
* 1x Raspberry Pi Zero *(Get a starter pack [here](https://www.adafruit.com/products/2817))*
  * 1x Micro SD Card 8GB
  * [Some way to connect your Raspberry Pi Zero to the internet]
    * *I used an Raspberry Pi 2 I had laying around (I basically set up Raspbian and downloaded everything following on the Raspberry Pi 2 and then transfair the micro SD card to the Raspberry Pi Zero*
    * *You also can use a WiFi USB dongle*
  * [1x Micro HDMI to HDMI adapter]
  * [1x USB OTG to USB adapter]
  * [Keyboard]
* 1x [Power management](https://www.adafruit.com/products/2465) (Powersuply + Battery charger)
* 1x [Battery](https://www.adafruit.com/products/354)
* 1x [Radio Module](https://www.wirelessthings.net/srf-wireless-rf-radio-surface-mount)
  * 1x [CC-Debugger](http://www.aliexpress.com/item/CC-Debugger-CCxxxx-Bluetooth-ZIGBEE-Wireless-Emulator-Programmer-for-RF-System-on-Chips/32417465960.html?spm=2114.13010608.0.55.1gfz18) to flash the chip with a custom software
* Some soldering skills + soldering equipment
* A steady hand
* Tools (tweezers, side cutters, double sided tape...)
* And of course an [OpenAPS compatible pump](http://openaps.readthedocs.io/en/master/docs/walkthrough/phase-0/hardware.html)

## What you will get
You will get a small portable Raspberry Pi based device with a decent battery life and a much better and stabile communication to your pump. Because we won't use that overpriced trashy CareLink stick.

## What you won't get
You won't get a finished product, that you can clip on like your insulin pump. Its basically just 3 PCBs glued together and bundled with a big battery. I am still working on a clip on option, but I still have had the right idea. Feel free to share yours:)

# Lets start with the software
1. You need to setup Raspbian, it is the operating system we use for the Raspberry Pi Zero
  * Download [here](https://www.raspberrypi.org/downloads/raspbian/). I am usin Jessie Light because we don't need the fully fledged Raspbian
  * Once downloaded you need to burn the files to the SD card, follow [this](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) instructions and you are good to go
2. Setup [OpenAPS](https://openaps.readthedocs.io/en/latest/index.html)
  * The best source is the webpage it self, it is worth reading through the documentation
3. Prepare your radio module
  * Follow this tutorial to flash the radio module, below you will find the color codes matching the colors used in the tutorial ![SRF Footprint](https://raw.githubusercontent.com/idoodler/ZeroAPS/master/srf%20footprint%20flash.png?token=AGgkwdv6VsdTywUvk8v7RYhet1swmNqRks5XgXlbwA%3D%3D)
4. Setup [MMowlink](https://github.com/oskarpearson/mmeowlink/wiki/Installing-MMeowlink) (used to allow OpenAPS communicate with the radio module) if you have not already

**Now swap your micro SD card in your Raspberry Pi Zero if you have not already**

* If you want to debug your Raspberry Pi Zero via USB there is an option for that:)
  * The Raspberry Pi Zero is capable of emulating USB devices with the USB OTG port, so we can simulate an Eathernet adapter. If you connect your Raspberry Pi Zero with your PC the Raspberry will create its own network. This allows you to directly ssh you into your Raspberry Pi Zero. Please keep in mind, that if you enable this you won't be able to use a USB device on your Raspberry Pi Zero anymore.
* If you want to extend the battery live of your close loop you can disable the HDMI components and the ACK LED
  * Disable HDMI
    * `sudo nano /etc/rc.local`
    * add `/usr/bin/tvservice -o` before `exit 0;`
  * Disable ACK legend
    * Follow [this](http://www.jeffgeerling.com/blogs/jeff-geerling/controlling-pwr-act-leds-raspberry-pi) instructions

**Congratulations, the software part is done** 👍

# Start with the hardware part
