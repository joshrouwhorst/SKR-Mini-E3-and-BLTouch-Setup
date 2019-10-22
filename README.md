# SKR Mini E3 and BLTouch Setup
How I setup SKR Mini E3 and BLTouch on my Ender 3 Pro

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

When I did that, it worked except the hotend was printing a few millimeters too high. So I downloaded gazcbm's [source code](https://github.com/gazcbm/Marlin-2.0.x-SKR-Mini-E3-v1.2). The Teaching Tech video above describes a little about how to configure the firmware to know where the BLTouch is in relation to the hotend. Using a caliper it wasn't hard to get the distance from the hotend to the BLTouch but I had to just do trial and error to figure out the depth. 

In order to compile the source code I followed this guide to [install VSCode and PlatformIO](http://marlinfw.org/docs/basics/install_platformio_vscode.html). When I made my changes to configure the BLTouch location, I went to the PlatformIO tab and clicked "Build". Once it finished it put a firmware.bin file in the project folder under .pio/build/STM32F103R_bigtree. I copied that to my SD card and loaded it back up. 
