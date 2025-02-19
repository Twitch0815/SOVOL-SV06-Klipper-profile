# SOVOL SV06 Klipper firmware & profile
Complete Klipper profile with all config files and macros to tune the Sovol SV06 (stock)

What's included :

- Klipper profile, already tuned with :

        - 3 printing mode
        - display config
        - ADXL settings (2 options : with the RPI or over a RPI-Pico)
        - Macros :
                  -  print start / end
                  -  load / unload filament
                  -  bed mesh (called in start print macro)
                  -  gantry calibration (allign the gantry at the top of the frame)
                  -  Z-offset
                  -  input shapper (resonnance compensation using ADXL module)
                  -  screws adjust (tilt bed screws)
                  
- Slicers Start/End macros config :

https://github.com/Pr20100/SOVOL-SV06-Klipper-profile/blob/main/Slicer%20START-END%20PRINT


How to use :

You'll need a raspberry pi with it's own SD card, micro-usb cable to connect to the printer mainboard and another SD card to flash the printer

1- First you have to instal Mainsail Klipper, link to download : https://docs.mainsail.xyz/setup/mainsail-os


2- Once installed in your raspberry, follow the steps to make the config : https://www.klipper3d.org/Installation.html

   -> during "make menuconfig" select the STM32F103 with a "28KiB bootloader", serial (on USART1 PA10/PA9) communication and Disable "SWD at startup"
  
   -> run "make" and wait...


3- put the firmware.bin included here in your SD card to flash the printer (or the one generated by the previons config steps, you can find it in /home/pi/klipper/out/klipper.bin)

   -> The SD card should be formated in FAT32 with 4096 blocks to make your flash successfull
  
  
4- Turn off your printer, insert the flash SD card, turn on the printer and wait 1mn before turning it off and removing the SD card


5- Connect your printer by USB to the raspberry and go to your raspberry IP adress


6- Download .zip bundle file attached and Upload the configuration files in your raspberry :

 -> PRINTER.CFG in /home/pi/printer_data/config directory, to have /home/pi/printer_data/config/printer.cfg
  
 -> CONFIG folder WITH ALL IT'S CONTENT in the same directory, respecting the path, with all the files and folders in it :
   - using web interface you will have to create folders yourself (case sensitive be carrefull)
   - using an FTP client like FILEZILA https://filezilla-project.org/
  
  
7- You should be able to connect klipper to the printer, if not you probably have a flash problem OR an USB cable issue :
- Try others USB cable lying aroud (from me it was the third tested who worked
        Still not working
- Check if the SD card is correctly formated (see 3rd step) and change the name of your .bin (cause the printer don't flash if she receive the same name file twice)
  
  
8- Things to do before printing

   -> Run PID TUNE for heater and bed https://www.klipper3d.org/G-Codes.html?h=pid#pid_calibrate_1
  
   -> Run these included macros : 
  
   1- GANTRY CALIBRATION to align the gantry with the top frame,
        
   2- BED MESH to make a 25 points bed mesh,
        
   3- Z OFFSET to calibrate your Z offset.
        
   -> Be sure you have in mainsail.cfg :
  
         [virtual_sdcard]
         path: /home/pi/printer_data/gcodes
                                            
   -> See available optionnal printing profiles in printer.cfg and options under /config/options.cfg
  
  For presure advance tuning, you can use this wonderfull tool : https://ellis3dp.com/Pressure_Linear_Advance_Tool/
  
 Happy printing ;)
