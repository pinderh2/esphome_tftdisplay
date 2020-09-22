# esphome_tftdisplay
Add an Adafruit 160x128 TFT color display to ESPHome.

Many displays have been added to ESPHome before, but not this one. There is a
project that is very similar (https://github.com/airy10/esphome-m5stickC), and
mine is based on that work, but I did change some things because my display is
similar but not exactly the same.

This work is based on the current /dev branch of ESPHome, which meant updating
a few minor things like SPI interface and Color.
Since this uses the /dev branch, builds are done on my laptop, not using ESPHome plugin
for Home Assistant. 

A sample config file is provided (garage_display.yaml), showing how I use this to make
a status display for my two garage doors. Also included, for reference, is the config file 
(garage_doors.yaml) for the garage door controller that creates some of the text
elements shown on this display.

To use this display, add the project files to the folder holding the .yaml config file.
Then create your yaml file with the 'display' element in it, using the one from
garage_display.yaml as an example.

To get my config file to work, you will need to fetch the font file and put it in 
that same folder, since I didn't post the font file to github.

Some things I learned along the way:

1) To work with the latest /dev branch of esphome:
   ```
   - git clone https://github.com/esphome/esphome.git
   - pip install ./esphome
   ```
2) My display uses BGR instead of RGB, but luckily Color supports this via to_bgr_565() 
   method.
3) My display does not require color inversion.
4) The display works with a ESP32, but not ESP8266, because of RAM issues. The ESP8266
   doesn't have enough RAM for the display buffer, and everything else it needs to do.
5) The essential purpose of my project was to display status about a Home Assistant element. At first
   I tried getting my display code to monitor states of HA elements, and try to figure out what
   was going on and why. Later, I realized it was better for the element that controls a device to 
   create the status text itself, since it has better knowledge of what's going on. Specifically,
   the status text for the garage doors (last operating time, and source of last open/close command)
   is created in garage_doors.yaml, and sent to Home Assistant, rather than the garage_display
   element trying to figure that out on its own. The garage_display.yaml is more of a dumb display now.
