# esphome_tftdisplay
Add Adafruit 160x128 TFT color display to esphome

This is based on some work found here: https://github.com/airy10/esphome-m5stickC

I made it work with the 160x128 display from Adafruit, using the current /dev branch of
esphome, which meant updating a few minor things like SPI interface and Color.
Since this uses the /dev branch, builds are done on my laptop, not using ESPHome plugin
for Home Assistant. 

A sample config file is provided, showing how I use this to make a status display
for my two garage doors.

To use, add the project files to the folder holding the .yaml config file.

You will need to fetch the font file and put it in that same folder.

Some things I learned along the way:

1) To work with the latest /dev branch of esphome:
   ```
   - git clone https://github.com/esphome/esphome.git
   - pip install ./esphome
   ```
2) My display uses BRG instead of RGB, but luckily Color supports this via to_bgr_565() 
   method.
3) My display does not require color inversion.
4) The project works on a ESP32, but not ESP8266, because of RAM issues.
