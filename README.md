# kicad_projects
Respository of personal KiCad projects that I have developed for home use. I am a Software Engineer by professional choice. Due to my professional commitments, like a lot of us, I am required to learn something new every few months. After recovering from the craziness and disruption created by COVID, I felt like I needed to learn something new. I felt like I needed to pick something other than software to learn. Golf feels like a pointless exercise in personal vanity, so here I am. I have been learning PCB schematic and layout design for fun since 2023.  I am sharing these with the world so we can all learn together.

These are actual working schematics as I have had them manufactured by [PCB Way](https://www.pcbway.com/). I have a few boards already printed and soldered them myself. I am willing to sell them for a mutually acceptable price. However, there are no implied guarantees and warrantees. Their usage will be at your own risk as this is a personal hobby project. I only need some time to solder all the components on to the board.

I can share working videos as needed.

# Project List

## Blind Controller
This project uses an ESP32-C3 to control a [DRV8874 H-bridge motor driver](https://www.ti.com/product/DRV8874) for controlling blinds. I have an outdoor blind which is quite hard to roll up and down. So the specs for the motor needed to be pretty high. I ended up using a [12v 40RPM motor](https://a.co/d/eGuKaqe) with a rated torque of 40kgcm.

I came up with the torque numbers by tying a bucket with a paracord to the blind cord. I slowly added water to the bucket until the blind rotated. Weighing the bucket and water gave me minimum weight needed to move the blind, which I then converted to force/torque. I do not remember the actual numbers but this gave me enough to buy this motor with enough buffer. IIRC, I think I went with double the calculated value.

In the previous iterations of this design I had an AC/DC converter on the board. The output current ratings for these converters was not enough for my needs. I needed at least 5A max current to prevent motor stall. And they were really bulky to mount on the board. So I decided to use an external 12v/6A power supply with barrel jack plug. The 12v is converted to 3.3v using [AP62250WU](https://www.diodes.com/assets/Datasheets/AP62250.pdf) buck converter to power the ESP32-C3.

This ESP32-C3 chip is then flashed with [ESPHome](https://esphome.io/) and integrated with [Home Assistant](https://www.home-assistant.io/). Or it is ready for your programming desires.

### Warnings:
1. Even though the components are rated for 5A, the track from the motor driver to the barrel jack connector is the default width (~9mils). My google search seems to show that ~10mils is good for ~2A. So it is probably not a good idea to run sustained loads of high amperage through this track.