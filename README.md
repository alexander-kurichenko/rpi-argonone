# rpi-argonone
Fan and power control for Argon One Raspberry Pi case
---

**Installation:**



- Install i2c-tools package:
	
     RaspberryPi OS / Debian / Ubuntu:	`sudo apt install i2c-tools`
    
     Arch:               `sudo pacman -Sy i2c-tools`
    
     Fedora:	`sudo dnf install i2c-tools`
	
    
  &nbsp;




- Update /boot/config.txt:

 
 ```
# Enable i2c
dtparam=i2c_arm=on

# Argon One poweroff button (triggered by double-click)   
dtoverlay=gpio-key,gpio=4,active_low=1,gpio_pull=down,keycode=116
        
 ```
  _Note for Ubuntu users: you can find this file in /boot/firmware_
  
  &nbsp;

 
 - And copy these files to specified location in your system:

   - **/usr/local/bin/fanctrl**
   
	    _Simple script to control fan speed depending on measured CPU temperature and options in /etc/default/fanctrl_
        
        

   - **/etc/default/fanctrl**

	    _Main configuration file_
        
        

   - **/etc/systemd/system/hw-shutdown.service**

	    _Sends poweroff command at shutdown_
        


   - **/etc/systemd/system/fanctrl.service**

	    _Starts /usr/local/bin/fanctrl._
	   

Reboot and enjoy :)

___
    

  &nbsp;
Manual control:
```$ fanctrl  
Usage: fanctrl [-D] [on|off] [0-4]
```
on/off - starts/stops fan (1st speed)

0/1/2/4 - set fan speed. _More values were not implemented because of noisy fan_

-D - this option is used to start it by systemd

-----
**NOTE:**
If fan was turned off or set to lower speed manually, it will be automatically started when temperature exceeds configured values
