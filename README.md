# Ender 5 Plus

I purchased a very cheap 2021 Ender 5 Plus that was working "so-so" with the extruder motor installed on top of the hotend

**Current Ender 5 Plus mods:**
1. Installed Klipper via an external RPI zero 2W

2. Replaced the original Creality V2.2 board with a Creality 1.1.5 Silent Board.
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

6. Installed an ESP32-CAM with URL Stream: http://192.168.1.5:81/stream and Service: MJPEG-Streamer. Adapted the default resolution in CameraWebServer.ino to VGA. Remixed an enclosure towards https://www.thingiverse.com/thing:6200417

7. Installed new clips for the bed https://www.amazon.com.be/gp/product/B09HQX1JGH/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1

8. Created my own repository of klipper https://github.com/ploucandco/klipper with DGUS-reloaded-Klipper. That gave me an up-to-date klipper/mainsail/moonraker and no issues anymore for the ADXL345.
  Added klipper/klippy/extras/t5uid1/, added klipper/src/avr/t5uid1/ and modified Kconfig and Makefile in klipper/src/avr/, added klipper/src/tm32/t5uid1/ and modified Kconfig and Makefile in klipper/src/stm32/
  So, only both avr and STM32 are supported in my version.
  Installed by using kiauh (https://github.com/dw-0/kiauh) and added the line https://github.com/ploucandco/klipper in klipper_repos.txt

9. Installed the RPI Zero 2W on a ZeroPointModule (https://github.com/pkElectronics/ZeroPointModule) and connected with the 24V power supply from the printer.
  The power of the ESP32-CAM is now also coming from the +5V output of the ZeroPointModule.
  The ZeroPointModule broke the ADXL345 connection as SPI0 of the RPI is now used by the CANbus interface. On top of that, SPI1 of the RPI doesn't support the needed mode for the ADXL345!
  I got the ADXL345 working on the creality V2.2 board by connecting to the SPI port and CS-> PB0, SCK-> PB1, MOSI -> PB2, MISO -> PB3 (used the commands: ACCELEROMETER_QUERY and MEASURE_AXES_NOISE to validate the worrking state).
  The connections with the creality V1.1.5 board will be challenging as the SPI port is on CS->PB4, MOSI->PB5, MISO->PB6 and SCK->PB7 and PB4 is used to command the fans!
  Another opportunity is to use Software SPI, but the noise is clearly higher when using on the V2.2 board: cs_pin: rpi:gpio18, spi_software_sclk_pin = rpi:gpio21, spi_software_mosi_pin = rpi:gpio20, spi_software_miso_pin = rpi:gpio19

10. Control of a Tuya smart power socket tinytuya (https://github.com/jasonacox/tinytuya) and gcode_shell_command from kiuah (https://github.com/dw-0/kiauh/tree/master).
  I found MGTHS (https://github.com/teejo75/mtghs) way way too complex to install. 
   
Current printer.cfg
