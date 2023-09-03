# Ender 5 Plus

I purchased a very cheap second hand 2021 Ender 5 Plus that was working "so-so" with the extruder motor installed on top of the hotend

**Current Ender 5 Plus mods:**
1. Installed Klipper via an external RPI zero 2W

2. Replaced the original Creality V2.1 board with a Creality 1.1.5 Silent Board.
  Made adapters for the dual Z-axis and fans
  The BL-Touch control pin is connected to ISCP interface with Vcc, MOSI (command signal of the BL-Touch), GND. The signal pin and GND have been inverted and connected to the Z-end.

3. Installed a Sprite Extruder Pro.
  Used the adapter from https://www.printables.com/model/329742-ender-5-plate-sprite-pro
  Reused the BL-Touch from the original extruder setup

4. Enabled original touchscreen with https://github.com/Desuuuu/DGUS-reloaded-Klipper as described here https://www.reddit.com/r/ender5plus/comments/kx9hsy/klipper_screen_on_ender_5_plus/ and as reference
  https://github.com/Thinkersbluff/DGUS-Reloaded_for_CR6-DWIN-SET_Component/tree/Refactored_For_CR6_T5L_DWIN_Display
  And this video for the connections https://www.youtube.com/watch?v=-pZmeRf-XNs
  RxD_LCD -> PD2, TxD_LCD -> PD3
  Updated CURA configuration in order to display the Print Status https://github.com/Desuuuu/DGUS-reloaded-Klipper/wiki/Print-status
  Enabled the 2 post-processing scripts "Display Progress on LCD" and "Display Filename and Layer on LCD"

5. Installed ADXL345 with connections to the RPI, twisted cables: GND+MISO, 3.3V+MOSI, SCLK+CS and setup input shaping
  Used V2 mount from https://cults3d.com/en/3d-model/tool/creality-sprite-adxl345-mount
  Got some issues: there was no https://github.com/Klipper3d/klipper/blob/master/scripts/klipper-mcu.service in the ~/klipper/scripts directory
  and enabling [mcu rpi] was not working with this tutorial (https://www.klipper3d.org/RPi_microcontroller.html).  I solved that with section 2.6 and beyond of this tutorial (https://www.lpomykal.cz/klipper-raspberry-as-a-second-mcu-installation/) and checked systemctl 
  status klipper-mcu

6. Installed an ESP32-CAM with URL Stream http://192.168.1.5:81/stream and Service MJPEG-Streamer. Adapted the default resolution in CameraWebServer.ino to VGA. Remixed an enclosure towards https://www.thingiverse.com/thing:6200417

7. Installed new clips for the bed https://www.amazon.com.be/gp/product/B09HQX1JGH/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1

8. Created my own repository of klipper https://github.com/ploucandco/klipper with DGUS-reloaded-Klipper. That gave me an up-to-date klipper/mainsail/moonraker and no issues for the ADXL345.
  Added klipper/klippy/extras/t5uid1/, added klipper/src/avr/t5uid1/ and modified Kconfig and Makefile in klipper/src/avr/, added klipper/src/tm32/t5uid1/ and modified Kconfig and Makefile in klipper/src/stm32/
  So only both avr and STM32 are supported.
  Installed by using kiauh (https://github.com/dw-0/kiauh) and added the line https://github.com/ploucandco/klipper in klipper_repos.txt

9. Installed the RPI Zero 2W on a ZeroPointModule (https://github.com/pkElectronics/ZeroPointModule) and connected with the 24V power supply from the printer.
  That broke the ADXL345 connection as SPI0 of the RPI is now used by the CANbus interface. On top of that, SPI1 of the RPI doesn't support the needed mode for the ADXL345!
  I got the ADXL345 working on the creality V2.1 board by connecting to the SPI port and CS-> PB0, SCK-> PB1, MOSI -> PB2, MISO -> PB3 (used the commands: ACCELEROMETER_QUERY and MEASURE_AXES_NOISE to validate the worrking state).
  The connections with the creality V1.1.5 board will be challenging as the SPI port is on CS->PB4, MOSI->PB5, MISO->PB6 and SCK->PB7 and PB4 is used to command the fans!
  Another opportunity is to use Software SPI, but the noise is clearly higher when using on the V2.1 board: cs_pin: rpi:gpio18, spi_software_sclk_pin = rpi:gpio21, spi_software_mosi_pin = rpi:gpio20, spi_software_miso_pin = rpi:gpio19
   
Current printer.cfg

**Future mods:**

9a. Power the ESP32-CAM via the +5V output of the ZeroPointModule 
9b. Further enable PWM for the hotend fan and electronics box fan with the RPI MCU (https://github.com/Klipper3d/klipper/blob/master/docs/RPi_microcontroller.md) by using the ZeroPoint Module.
9c. Reenable the ADXL345. I will potentially need to replace the Creality V1.1.5 board by a Creality E3 free (https://github.com/CrealityOfficial/E3-Free-runs-Silent-Motherboard) that I got for very cheap. I already figured out that I need to select the STM32F401
with a "64KiB bootloader" and serial (on USART1 PA10/PA9) communication. Also flash the firmware by copying "out/klipper.bin" to a SD card at [STM32F4_UPDATE] folder at root
 
10. 400mm MG12H Linear rails for Y: https://www.thingiverse.com/thing:3960105 or remix: https://www.thingiverse.com/thing:5380428
  with such end-stops: https://www.thingiverse.com/thing:3449917

11. Control of a smart power socket via moonraker and tinytuya (https://github.com/jasonacox/tinytuya) or https://github.com/teejo75/mtghs -> that should enable to get rid of octoprint on my ender3v2 and further install Klipper on this one

12. Make a small PCB for the original touchscreen, the filament sensor and the BL-Touch on the original Creality 1.1.5 Board
   VCC                        GND
   N/A                        N/A
   N/A                        RxD_LCD -> PD2
   N/A                        TxD_LCD -> PD3
   Filament Sense -> PC0      BL-Touch Control -> PA4

12. Install corners reinforcements for the square chassis, like such ones https://www.thingiverse.com/thing:4890331 or https://www.thingiverse.com/thing:4196635

15. MG9 Linear rails for X with a lighter Gantry like this one: https://www.aliexpress.com/item/1005004910125155.html?spm=a2g0o.productlist.main.17.25957cabHzZwE8&algo_pvid=9e22712c-21bd-42ea-b19b-f8ce81c6447f&algo_exp_id=9e22712c-21bd-42ea-b19b-f8ce81c6447f-8&pdp_npi=3%40dis%21EUR%2169.47%2142.37%21%21%2175.58%21%21%400b0a558a16901350300074452d0733%2112000030986649526%21sea%21BE%214310898249&curPageLogUid=8zFS2bfiPk8L

16. CoreXY like ZeroG or the following one: https://drive.google.com/drive/folders/1-1tjyXcxYlQ97HP_JLZ4AQB9xGDrp68Q
  Some infos https://www.3docity.com.au/mercury-zerog-ender-5-mod-build-info-klipper-slicer-profiles/
  https://www.fabreeko.com/collections/mods/products/mercury-one-kit?variant=43506009538815

17. Enclosure like https://www.thingiverse.com/thing:5111093

18. 220V bed like this one: https://www.aliexpress.com/item/1005005657153057.html?spm=a2g0o.productlist.main.41.25957cabHzZwE8&algo_pvid=9e22712c-21bd-42ea-b19b-f8ce81c6447f&algo_exp_id=9e22712c-21bd-42ea-b19b-f8ce81c6447f-20&pdp_npi=3%40dis%21EUR%2175.39%2175.39%21%21%2182.03%21%21%400b0a558a16901350300074452d0733%2112000033912707130%21sea%21BE%214310898249&curPageLogUid=R9eD0Ap9gOdx

19. Install an ERCF https://www.aliexpress.com/item/1005004537312582.html?spm=a2g0o.productlist.main.67.4861630f9qWtfo&algo_pvid=00f3bf77-b45e-4930-aff9-60a1b7c5a0a2&algo_exp_id=00f3bf77-b45e-4930-aff9-60a1b7c5a0a2-33&pdp_npi=3%40dis%21EUR%21178.43%21132.04%21%21%21194.14%21%21%40211be10916901353988465274d0746%2112000029518182151%21sea%21BE%214310898249&curPageLogUid=1caYjVaTd2w6



**Some further usefull pages**
https://github.com/Identity-Unkn0wn/Ender-5-Plus-Upgrades#klipper--cfgs
