# APSystems inverters monitoring

![housing](https://user-images.githubusercontent.com/12282915/150977290-19a81da7-0c82-4eb8-9522-89a74197bcea.jpg)

A software for a Raspberry pi Zero and other Raspberry models to read the production of APS inverters yc600 and qs1. I should mention that the basics (the zigbee communication) has been reverse engineered by others who shared their results here: https://github.com/Koenkk/zigbee2mqtt/issues/4221<br>
A very important detail is the software running on the zigbee module, developped by @kadzsol.  

## WARNING
People keep asking for the ssh login for obvious reasons. Its 'root' and 'mies'. Please be aware that this is known to the whole world now.
So never put the ssh port open ttw unless you have a very strong password.

## PURPOSE
This project is intended for reading APS Systems inverters. The program can pair and poll YC600 and QS1 inverters, up to 9 pieces. The read values are: 
- displayed on a web page  
- sent via mosquitto in a Json format
- saved in a database for charts and statistics. 

## DOWNLOADS
2022-02-15 The new version RPI-ECU-v2_0 is available. This has to be installed by burning the disk image to an sdcard. Be sure you upgraded to version RPI-ECU-v1_5 if you want to reliable backup your settings and databases. Please follow the steps in **installation via the sd-card immge** , in particular it is important that you expand the filesystem first, before restoring your backup!!. <br><br>You can download the package here:
https://1drv.ms/u/s!AkMG5FvUwhedixPTuIXzbsG3cnrZ?e=PV8bUQ<br><br>
**instructions** You can burn the image on a new sd-card at any time. The backup of the old system however, and starting up / restore the new system should be done in the period after sunset and before midnight. This way we have a smooth migration. Follow the steps in * installation of a new
<br><br>**version 1:**<br>
Only the upgrade to 1_5 matters for the backup procedure. Than you can migrate to version 2. 

If you are currently using version **RPI-ECU-v1-4** (check the infopage) you can upgrade to version RPI-ECU-v1_5 .<br>Download the tarball here
https://1drv.ms/u/s!AkMG5FvUwhedixKJflkO_z8JjhBo?e=IAtQ8y <br>
This update is important as soon a new version 2 will be available. This version can only be installed by burning a new sd image.<br>Likely you want to backup your settings and databases first. This upgrade contains a new more reliable backup procedure.

upgrade to version RPI-ECU-v1_4: https://1drv.ms/u/s!AkMG5FvUwhedixBZv4dx-B7tFCWp?e=dt1FHK <br>
upgrade to version RPI-ECU-v1_3: https://1drv.ms/u/s!AkMG5FvUwhediwqRzRVIn_FmXms0?e=R16Nb7 <br>
 
Please see 'CHANGELOG'
<br><br>
If you are currently using version **RPI-ECU-v1_1** (check the infopage) you now can upgrade to version RPI-ECU-v1_2.<br>
Download the tarball here https://1drv.ms/u/s!AkMG5FvUwhediwMEziqX7Kv8eWEC?e=K5FKcC <br>
In the menu 'system' you'l find the option 'update'. Click this and choose the downloaded file.
If you get an error about the filename, try to rename it to ecu_swupdate.tar. <br>
Please see 'CHANGELOG'

dowload RPI_ECU-v1_4 04-02-2022 https://1drv.ms/u/s!AkMG5FvUwhediw8uRyYhBFCXikJ0?e=VbwwfO <br>

See it in action on youtube: https://youtu.be/oF-QE4GUGy8
<br><br>
In case someone wants to print the housing: https://1drv.ms/u/s!AkMG5FvUwhediwaPqGYXa7vMkXp8?e=kzkdHQ<br><br>
**Some webpages:**<br>
![pages_rpiecu](https://user-images.githubusercontent.com/12282915/147755570-db00c49e-3033-42b2-bb68-8bbb9a003e33.jpg)
<br><br>
## FEATURES:
- all inverter information such as temperature, dc voltage etc available
- energy production per solar panel displayed
- Easy wifi config portal
- Easy add, delete and pair inverters
- There are 3 different json formats, a special one for domoticz
- a very smart console to send zigbee commands and debug
- polled values are stored in a database
- charts of the production at multiple days are available
- There is a page with some statistic data 
- The menu is only accessible from local network with login
- software can be updated by uploading and installing a tar achive

## (RE) INSTALLATION INSTRUCTIONS
**installation via the sd-card immge**<br>
**step 1** Download the package, unzip and burn the image on an sd card. I you are new user of this software please continue with stap 3.
**step 2** You already are using this software then you can make a backup of your system and databases first. You should do this after sunset. Then complete the next steps before midnight in order to get a smooth migration..
**step 3**
<br>Boot up with the new sd-card. Open the wifi settings on your computer/tablet/phone. 
After a while you will see an accesspoint **RadioAP**. Connect to it with the paswd 'rpiradio'.
<br>Now browse to http://192.168.4.1 and enter your wifi credentials as well as a userename/password
for the security of your webpages. Click save and wait for the reboot button to appear. Click it.
**note:** The security credentials are needed to get access to the settings of your ECU. 

<br>Next the Raspberry reboots and tries to connect to your wifi. This may take a while!
You can find your Raspberry's ip address by browsing to http://rpiecu.local.
Or open your router's webpage to see the connected devices to find the ip address.
Or use a wifi analizer tool on your phone/tablet.
**step 4**
The first thing to do now is to expand the filesystem. Go to the menu 'system' and click the button 'expand'.
After the reboot you can restore your system backup.
**step 5**
If you restored a systembackup you can check the settings otherwise you should do some other configuration first. See the chapter 'SETTINGS'.
In particular the setting of the geographic coordinates is important.

**upgrade an existing installation**
If you already use this software you can do 2 things: Install a new image or simply update the software.
If you want to install a newer released image, you best do this after sunset. You can backup your databases first, and restore
them after you installed the new version. (menu databases->backup).<br>

## SOFTWARE UPDATES
If the software needs updates, they are provided as a file ecu_swupdate_date.tar that you can download.
This file can be uploaded to your system. When this succeeded you'l get a button<br>
'install' and when pressed a script is running that unpacks the archive and replaces<br>
the relative files. You can follow the process in the outputframe. In the chapter 'CHANGELOG' you can see
what has been changed.

## FACTORY RESET
When i make an image of the system there are settings and data present that belong to my inverters. 
You should edit inverter 0 with your own name and serialnr. Now go to the menu 'databases' and wipe all data for inv0 in both databases.
If you restore a backup, the existing databases are removed and replaced by those in the backup.

## SETTINGS AFTER INSTALL A NEW IMAGE
<br>In the menuitem 'settings' you have to enter the coordinates of your location. Now your system can determine
sunset and sunrise. <br>Also enter the id nr for the zigbee coordinator, this must be a 12 character string, like D6B3011B9780<br>
<br>Enter an offset to sunrise and sunset were the polling should start. On a bright day, the inverter may startup before sunrise. <br>
I have an offset of -5 so i start 5 minutes before sunrise with the polling.  

## START THE ZIGBEE SYSTEM
Check first the hardware, than go to "console" and try to start the zigbee coordinator. With the healthcheck you can see if this succeeded.
If success you can configure an inverter, go to the menu 'inverters' and fill up / save the form. **Attention** you should provide a numeric value in the field DOM.IDX like 123, do not leave it empty or put a non-numeric value. !!! 
Now you can try to pair this inverter, but only during daylight, the inverter will not answer when it's not working.  
If success, this inverter will be polled automatically every 5 minutes. The data is displayed in the frontpage and charts,
and is send via Mosquitto. At reboot all processed will be started automatically. 

## HARDWARE
What you need for this project is:
- a Raspberry zero 1.3 W (yes the W means wifi) ~11Euro or a goodold model 1 will work too.
- micro sd-card class 10, 8 or 16 gB (like in your phone)
- a cc2530 module, see photo
- a 5V dc 3A powersupply see photo

estimates costs some 25 Euro.
The zigbeemodule should be flashed with a firmware that can be found here https://github.com/Koenkk/zigbee2mqtt/issues/4221.  

## WIRING ZIGBEE MODULES
you need 5 dupont cables.

**cc2530**<br>
p2 -> gpio14 ( pin 8 )<br>
p3 -> gpio15 ( pin 10 )<br>
rst -> gpio18 ( pin 12 )<br>
vcc -> 3.3V<br>
gnd -> g<br>
<br>
**cc2531** (not tested by me!)<br>
dd -> gpio14 ( pin 8 )<br>
dc -> gpio15 ( pin 10 )<br>
rst -> gpio18 ( pin 12 )<br>
vcc -> 3.3V<br>
gnd -> g<br>
if this doesn't work try to swap dd and dc<br>
<br>
![RPI-ECU_WIRING](https://user-images.githubusercontent.com/12282915/148555017-c3e7a36f-6595-415f-95c7-0eb32400f2bb.jpg)

hardware:<br>
![rpi_minhw](https://user-images.githubusercontent.com/12282915/147755635-156ec891-1dfd-4ff3-a59e-979653e1f47a.jpg)
![pwrsup](https://user-images.githubusercontent.com/12282915/148765236-f1662888-5d44-43d7-a09e-abe379e6e89d.jpg)

![stats](https://user-images.githubusercontent.com/12282915/148557056-7ca1aa16-36bb-4352-a0fb-ba7e8e3b5ee5.jpg)
<br>

## TROUBLE SHOOTING
**You forgot your admin password.** 
If you type http://your_ecu_ip/recovery/recover.php you will enter a secret page where you
can drop your wifi credentials. At reboot the accesspoint **RadioAP** is started. 

## CHANGELOG
**version RPI-ECU-v2_0**  Only installable as sd-image.
- changed the process of gathering the total energy values. 
- ruled out the effect of disturbances (eclips, inverter resets, zigbee disturbances)
- added a tool to upload and show a photo of your powerplant.

**version RPI-ECU-v1_5**  11 feb 2022
- improved the backup process as this was not working as it should.

**version RPI-ECU-v1_4**  04 feb 2022
- added a tool for statistic research over an adjustable period.
- removed a small bug in the mosquitto sending and settings.
- added a chart for average power
- added currency setting
- improved some beauty flaws

**version RPI-ECU-v1_3**  28 jan 2022
- added a quick analysis tool for statistic research.
- removed a bug in the pairing process that malformed the inverterProprties files.
- added a workaround for qs1's not returning values for freq and acv

**version RPI-ECU-v1_2**  24 jan 2022
- changed the chart 'last 30 days' to a selectable month.
- made the programm suitable for old Raspberry 1 model.
  
**version RPI-ECU-v1_1**  19 jan 2022
- added means of backup of settings and databases
- added means to upload/install software upgrade package
- added some new features to the charts and statistics
- removed a hard-coded inverternumber in midNight.cpp
- changed the security strategy, only local access to settings pages.
- changed the retention policy of invEnergy to 3 years
