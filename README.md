# Ender 5 Plus

I purchased a second hand 2021 Ender 5 Plus that was working "so-so" with the extruder motor installed on top of the hotend

**Current Ender 5 Plus mods:**
1. Installed Klipper via an external RPI zero 2
2. Replaced the original V2.2 board with a Creality 1.1.5 Silent Board.
  Made adapters for the dual Z-axis and fans
  The BL-Touch control pin is connected to ISCP interface with Vcc, MOSI (command signal of the BL-Touch), GND. The signal pin and GND have been inverted and connected to the Z-end.
3. Installed a Sprite Extruder Pro.
  Used the adapter from https://www.printables.com/model/329742-ender-5-plate-sprite-pro
  Reused the BL-Touch from the original extruder setup
4. Enabled original touchscreen with https://github.com/Desuuuu/DGUS-reloaded-Klipper as described here https://www.reddit.com/r/ender5plus/comments/kx9hsy/klipper_screen_on_ender_5_plus/
  And this video for the connections https://www.youtube.com/watch?v=-pZmeRf-XNs
  RxD_LCD -> PD2, TxD_LCD -> PD3

Current printer.cfg

**Future mods:**
4a. Finalise configuration for the original touschscreen with diplaying the Print Status https://github.com/Desuuuu/DGUS-reloaded-Klipper/wiki/Print-status

5. Install ADXL345 with connections to the RPI, twisted cables: GND+MISO, 3.3V+MOSI, SCLK+CS and setup input shaping
6. Control of a smart power socket via moonraker and tinytuya (https://github.com/jasonacox/tinytuya) or https://github.com/teejo75/mtghs -> that should enable to get rid of octoprint on my ender3v2 and further install Klipper on this one
7. Install a ZeroPointModule (https://github.com/pkElectronics/ZeroPointModule) in order to have the RPI zero 2 inside the printer box with the 24V power supply from the printer. Maybe using this method for the serial connection: https://www.youtube.com/watch?v=QNxE_v5G_bg
8. Command the always ON fan of the extruder and the always ON fan from the printer box via the PWMs of the ZeroPointModule
9. Move the BL-Touch to have no Y offset
10. Make a small PCB for the original touchscreen, the filament sensor and the BL-Touch on the original Creality 1.1.5 Board
   VCC                        GND
   N/A                        N/A
   N/A                        RxD_LCD -> PD2
   N/A                        TxD_LCD -> PD3
   Filament Sense -> PC0      BL-Touch Control -> PA4

11. New clips for the bed like https://www.amazon.com.be/gp/product/B09HQX1JGH/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1
12. Install a camera connected to the RPI zero 2+LED lights
13. Install corners reinforcements for the square chassis, like such ones https://www.thingiverse.com/thing:4890331
14. 450mm MG12 Linear rails for Y: https://cults3d.com/en/3d-model/tool/ender-5-plus-linear-rail-mod-remix
15. MG9 Linear rails for X with a lighter Gantry like this one: https://www.aliexpress.com/item/1005004910125155.html?spm=a2g0o.productlist.main.17.25957cabHzZwE8&algo_pvid=9e22712c-21bd-42ea-b19b-f8ce81c6447f&algo_exp_id=9e22712c-21bd-42ea-b19b-f8ce81c6447f-8&pdp_npi=3%40dis%21EUR%2169.47%2142.37%21%21%2175.58%21%21%400b0a558a16901350300074452d0733%2112000030986649526%21sea%21BE%214310898249&curPageLogUid=8zFS2bfiPk8L
16. CoreXY like ZeroG or the following one: https://drive.google.com/drive/folders/1-1tjyXcxYlQ97HP_JLZ4AQB9xGDrp68Q
  Some infos https://www.3docity.com.au/mercury-zerog-ender-5-mod-build-info-klipper-slicer-profiles/
  https://www.fabreeko.com/collections/mods/products/mercury-one-kit?variant=43506009538815
17. Enclosure like https://www.thingiverse.com/thing:5111093
18. 220V bed like this one: https://www.aliexpress.com/item/1005005657153057.html?spm=a2g0o.productlist.main.41.25957cabHzZwE8&algo_pvid=9e22712c-21bd-42ea-b19b-f8ce81c6447f&algo_exp_id=9e22712c-21bd-42ea-b19b-f8ce81c6447f-20&pdp_npi=3%40dis%21EUR%2175.39%2175.39%21%21%2182.03%21%21%400b0a558a16901350300074452d0733%2112000033912707130%21sea%21BE%214310898249&curPageLogUid=R9eD0Ap9gOdx
19. Install an ERCF https://www.aliexpress.com/item/1005004537312582.html?spm=a2g0o.productlist.main.67.4861630f9qWtfo&algo_pvid=00f3bf77-b45e-4930-aff9-60a1b7c5a0a2&algo_exp_id=00f3bf77-b45e-4930-aff9-60a1b7c5a0a2-33&pdp_npi=3%40dis%21EUR%21178.43%21132.04%21%21%21194.14%21%21%40211be10916901353988465274d0746%2112000029518182151%21sea%21BE%214310898249&curPageLogUid=1caYjVaTd2w6



**Some further usefull pages**
https://github.com/Identity-Unkn0wn/Ender-5-Plus-Upgrades#klipper--cfgs
