Instructions for the Banana PI M64 / Pine64+ Camera Module
***********************************************************

Basic instructions to activate and use the Pine64+ Camera module.

git clone https://github.com/avafinger/pine64_camera

Known issues:
 - Controls not working yet
 - HW encoding not used, no video saving

Requires:
 - kernel 3.10.102 (or latest) - Debian / Ubuntu (Desktop)
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
	sudo /sbin/modprobe -r -f s5k4ec 

Now load the new driver after you update it:

	sudo /sbin/modprobe s5k4ec 
	sudo /sbin/modprobe vfe_v4l2


Now you should have /dev/video0:

	ls /dev/video0 

Or edit /etc/modules and add the two lines and reboot:

	s5k4ec 
	vfe_v4l2

**** This is a WiP - use at your own risk ****


Now use the modified Guvcview to see your camera working
========================================================

Install dependencies:

	sudo apt-get install libmp3lame-dev libx264-dev libpulse-dev libv4l-dev libsdl1.2-dev libgtk-3-dev portaudio19-dev libpng12-dev libavcodec-dev libavutil-dev libudev-dev libusb-1.0-0-dev libpulse-dev libgsl0-dev libv4l2rds0


Install the deb packages in Ubuntu Xenial 16.04 (Desktop)

Run:

	sudo dpkg -i libguvcview-1.1-1_2.0.2+debian-3_arm64.deb 
	sudo dpkg -i guvcview_2.0.2+debian-3_arm64.deb


Run:

	guvcview (from command line) or use the menu

or

	guvcview -d /dev/video0 -x 640x480 -r sdl -f nv12


History
-------

* Initial commit
* Fix for Gtk3 Gui to start correctly on any win size, you are know able to switch Resolutions
* additional instructions and updated deb



