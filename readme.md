Instructions for the Pine64+ Camera Module
******************************************

Basic instructions to activate and use the Pine64+ Camera module.

git clone https://github.com/avafinger/pine64_camera

Known issues:
 - Some Artifacts on streaming
 - Controls not working yet


Requires:
 - kernel 3.10.102 (or latest) - Debian / Ubuntu
 - camera module s5k4ec
 - DTB with s5k4ec enabled

Steps:
 - Connect you camera module
 - rename in SD card:  [sdcard]/BOOT/pine64/sun50i-a64-pine64-plus.dtb to [sdcard]/BOOT/pine64/sun50i-a64-pine64-plus.dtb_no_camera
 - copy the sun50i-a64-pine64-plus.dtb [sdcard]/BOOT/pine64/


Final steps
===========
Run in the command line:

sudo /sbin/modprobe -r -f vfe_v4l2

sleep 1

sudo /sbin/modprobe s5k4ec 

sudo /sbin/modprobe vfe_v4l2

Now you should have /dev/video0:

ls /dev/video0 


**** This is a WIP - use at your own risk ****

Now use the modified Guvcview to see your camera working
========================================================

You need to compile Guvcview in order to use your camera, or install the deb packages or try motion.

Install the deb packages in Ubuntu Xenial 16.04
Run:
sudo dpkg -i *.deb

Run:
guvcview -d /dev/video0 -x 640x480 -r sdl -f yu12





