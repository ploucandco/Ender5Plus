# Ender 5 Plus

I purchased a second hand 2021 Ender 5 Plus that was working "so-so" with the extruder motor installed on top of the hotend

**Current Ender 5 Plus mods:**
1. Installed Klipper via an external RPI zero 2
2. Replaced the original V2.2 board with a Creality 1.1.5 Silent Board
  Made adapters for the dual Z-axis and fans
  The BL-Touch control pin is connected to ISCP interface with Vcc, MOSI (command signal of the BL-Touch), GND. The signal pin and GND have been inverted and connected to the Z-end.
4. Installed a Sprite Extruder Pro
  Used the adapter from https://www.printables.com/model/329742-ender-5-plate-sprite-pro
  Reused the BL-Touch from the original extruder setup

Current printer.cfg

**Future mods:**
5. Re-enable the filament sensor and original touch screen
6. Control of a smart power socket via moonraker
7. Get the original touch screen working with Klipper with https://github.com/Desuuuu/DGUS-reloaded-Klipper as described here https://www.reddit.com/r/ender5plus/comments/kx9hsy/klipper_screen_on_ender_5_plus/
Maybe also check what's here https://github.com/bustedlogic/DWIN_T5UIC1_LCD and https://github.com/GalvanicGlaze/DWIN_T5UIC1_LCD/wiki and https://www.reddit.com/r/ender3v2/comments/oa8qwx/klipper_using_ender_3_v2_display_check_first_post/
And this video for the connections https://www.youtube.com/watch?v=-pZmeRf-XNs
8. Displace the BL-Touch as overheating and have a support for the ADXL345
9. Install a Buck Converter from 24V->5V and install the RPI zero 2 inside the printer electronic cover, maybe using this method for the serial connection: https://www.youtube.com/watch?v=QNxE_v5G_bg
10. Install a camera connected to the RPI zero 2+LED lights
11. Install reinforcements for the square chassis, like such ones https://www.thingiverse.com/thing:4890331
12. 450mm MG12 Linear rails for Y: https://cults3d.com/en/3d-model/tool/ender-5-plus-linear-rail-mod-remix
13. MG9 Linear rails for X with a lighther Gantry
14. CoreXY like ZeroG or the following one: https://drive.google.com/drive/folders/1-1tjyXcxYlQ97HP_JLZ4AQB9xGDrp68Q 
15. Enclosure like https://www.thingiverse.com/thing:5111093
