I purchased a very cheap 2021 Ender 5 Plus that was working "so-so" with the extruder motor installed on top of the hotend

**Current Ender 5 Plus mods:**

1. Installed Klipper via an external RPI zero 2W
   
2. Installed a Sprite Extruder Pro. Used the adapter from https://www.printables.com/model/329742-ender-5-plate-sprite-pro Reused the BL-Touch from the original extruder setup
  
3. Replaced the original Creality V2.2 board with a BTT SKR Mini E3 V3.0
   
4. Installed a 4 inches LCD screen https://www.waveshare.com/wiki/4inch_RPi_LCD_(C) for klipperscreen and connected the RPI zero 2W to the SKR Mini according to this manual: https://github.com/ploucandco/Ender_5_Plus_KlipperScreen/blob/main/Install%20Klipper%2BKlipperScreen%20Ender%205%20Plus.pdf

5. Installed ADXL345 with connections ICSP port of the SKR Mini. Used V2 mount from https://cults3d.com/en/3d-model/tool/creality-sprite-adxl345-mount
  
6. Control of a Tuya smart power socket tinytuya (https://github.com/jasonacox/tinytuya) and gcode_shell_command from kiuah (https://github.com/dw-0/kiauh/tree/master)
   
7. Installed 400mm linear rails on Y axis with this mod: https://www.thingiverse.com/thing:3960105

8. Installed a RPI Camera Module 3 with the following case: https://www.thingiverse.com/thing:6277496

9. Install ASA printed corners reinforcements for the chassis (125mmx125mm version): https://www.thingiverse.com/thing:4196635

**Future mods:**

10. Find the source of noise when moving fast on the Y gantry

11. MGN9 or MGN12 Linear rails for X with lighter gantry
    
12. CAN bus toolhead maybe with sensorless homing

13. ZeroG CoreXY or the following one: https://drive.google.com/drive/folders/1-1tjyXcxYlQ97HP_JLZ4AQB9xGDrp68Q
  Some infos https://www.3docity.com.au/mercury-zerog-ender-5-mod-build-info-klipper-slicer-profiles/
  
14. Enclosure like https://www.thingiverse.com/thing:5111093
 
15. 220V bed like this one: https://www.aliexpress.com/item/1005005657153057.html?spm=a2g0o.productlist.main.41.25957cabHzZwE8&algo_pvid=9e22712c-21bd-42ea-b19b-f8ce81c6447f&algo_exp_id=9e22712c-21bd-42ea-b19b-f8ce81c6447f-20&pdp_npi=3%40dis%21EUR%2175.39%2175.39%21%21%2182.03%21%21%400b0a558a16901350300074452d0733%2112000033912707130%21sea%21BE%214310898249&curPageLogUid=R9eD0Ap9gOdx

16. Install an ERCF https://www.aliexpress.com/item/1005004537312582.html?spm=a2g0o.productlist.main.67.4861630f9qWtfo&algo_pvid=00f3bf77-b45e-4930-aff9-60a1b7c5a0a2&algo_exp_id=00f3bf77-b45e-4930-aff9-60a1b7c5a0a2-33&pdp_npi=3%40dis%21EUR%21178.43%21132.04%21%21%21194.14%21%21%40211be10916901353988465274d0746%2112000029518182151%21sea%21BE%214310898249&curPageLogUid=1caYjVaTd2w6

**Some further usefull pages**
https://github.com/Identity-Unkn0wn/Ender-5-Plus-Upgrades#klipper--cfgs
