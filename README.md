# SKR Mini E3 and BLTouch Setup
Dec 22, 2019

This documents what I had to do to get my SKR Mini E3 and BLTouch installed and working. One thing I learned is that guides like this one have a short lifespan before the info in them is irrelevant. So good luck to you! If you're finding this a year down the road maybe some of it will still be useful, but keep in mind you might need to do some more digging.

## Hardware

### Installing the BLTouch
I used a mount that came with the BLTouch. But there are many printable mounts on Thingiverse.
[Insert image of mount]

### Installing the SKR Mini Board
[Teaching Tech video](https://www.youtube.com/watch?v=-XUQKQnUNig)

When I first got the printer started up, the display and the BLTouch wouldn't turn on. I had to switch the blue and red wires on my BLTouch in order to get it to work. Apparently there's no standard to wire colors so maybe see if it works first and if not try switching them. You can use something sharp to carefully pull up the little plastic flaps on the connector to the board to pull out the wires and switch them.

[Insert images of wiring]

## Firmware

I couldn't figure out how to get the firmware updated from Teaching Tech's videos. I don't know if it's true but from what I was seeing the new SKR Mini E3 boards can't be updated using the Ardunio IDE like he was using in there. So here's what I did instead.

I started working on the firmware based on this [reddit post](https://www.reddit.com/r/ender3/comments/dfw5ox/skr_mini_e3_v12_board_with_tmc2209_bltouch_link/). So if you want to just get going and see if the hardware works (which isn't a bad idea) you can download his [firmware.bin](https://github.com/gazcbm/Marlin-2.0.x-SKR-Mini-E3-v1.2/blob/master/CompiledFirmWare/firmware.bin) file, copy it to an SD card and start up the printer with the SD card installed.

When I did that, it worked except the hotend was printing a few millimeters too high. In order to properly work, the firmware needs to know where the BLTouch sensor is in relation to the hotend. What I didn't realize at the time was that you can easily set how high the BLTouch is by turning on the printer and going to Configuration > Z Probe Offset. But since I didn't know that, I downloaded gazcbm's [source code](https://github.com/gazcbm/Marlin-2.0.x-SKR-Mini-E3-v1.2). The Teaching Tech video above describes a little about how to configure the firmware for the BLTouch position. Using a caliper it wasn't hard to get the distance from the hotend to the BLTouch and the setting already in the firmware was close enough, but I had to just do trial and error to figure out the height. 

While I was at it, I wanted to change the number of touch points the probe would hit when calibrating. Out of the box the firmware is set to do a 7x7 grid which takes a while to get through. I found this [Stack Exchange post](https://3dprinting.stackexchange.com/questions/8497/how-to-increase-the-amount-of-probing-points-for-a-bltouch-sensor-in-marlin-firm) which explains you just have to change the `GRID_MAX_POINTS_X` setting in the configuration.h file. I set it to 3 while I was tinkering and set it to 5 later when I had it all running smooth for better accuracy.

### Editing and Compiling
In order to compile the source code into a firmware.bin file, I followed this guide to [install VSCode and PlatformIO](http://marlinfw.org/docs/basics/install_platformio_vscode.html). After I made my changes to configure the BLTouch location and the grid settings I went to the PlatformIO tab and clicked "Build". Once it finished it put a firmware.bin file in the project folder under .pio/build/STM32F103R_bigtree. I copied that to my SD card and loaded it back up. 
