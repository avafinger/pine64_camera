Instructions for Pine64+ Camera Module
**************************************

Basic instructions to activate and use the Pine64+ Camera module.

Update: Guvcview 2.0.3

git clone https://github.com/avafinger/pine64_camera

Known issues:
 - Controls not working yet
 - HW encoding not used, no video saving

Requires:
 - kernel 3.10.102 (or latest) - Debian / Ubuntu (Desktop)
 - camera module s5k4ec 
 - DTB with s5k4ec enabled

If you have installed any previous version, please remove it with something like this:

	sudo apt-get remove --purge guvcview
	sudo apt-get remove --purge libguvcview-1.1-1

Steps:
 - Connect you camera module
 - rename in SD card:  [sdcard]/BOOT/pine64/sun50i-a64-pine64-plus.dtb to [sdcard]/BOOT/pine64/sun50i-a64-pine64-plus.dtb_no_camera
 - copy the sun50i-a64-pine64-plus.dtb [sdcard]/BOOT/pine64/


Final steps
===========
Run in the command line:

	sudo /sbin/modprobe -r -f vfe_v4l2
	sudo /sbin/modprobe -r -f s5k4ec 

or in Ubuntu:

	sudo modprobe -r -f vfe_v4l2
	sudo modprobe -r -f s5k4ec 


Now load the new driver after you update it:

	sudo /sbin/modprobe s5k4ec 
	sudo /sbin/modprobe vfe_v4l2

or the Ubuntu way:

	sudo modprobe s5k4ec 
	sudo modprobe vfe_v4l2


Now you should have /dev/video0 and check the sensor:

	ls /dev/video0 

and

	dmesg | grep OK



Or edit /etc/modules and add the two lines and reboot:

	s5k4ec 
	vfe_v4l2


**** This is a WiP - use at your own risk ****


Now use the modified Guvcview to see your camera working
========================================================

Install dependencies from command line:

	sudo apt-get install libmp3lame-dev libx264-dev libpulse-dev libv4l-dev libsdl1.2-dev libgtk-3-dev portaudio19-dev libpng12-dev libavcodec-dev libavutil-dev libudev-dev libusb-1.0-0-dev libpulse-dev libgsl0-dev libv4l-dev


Install the deb packages in Ubuntu Xenial 16.04 (Desktop)

Run from command line (version 2.0.2):

	sudo dpkg -i libguvcview-1.1-1_2.0.2+debian-3_arm64.deb 
	sudo dpkg -i guvcview_2.0.2+debian-3_arm64.deb

or

Run from command line (version 2.0.3):

	sudo dpkg -i libguvcview-1.2-1_2.0.3+debian-1_arm64.deb 
	sudo dpkg -i guvcview_2.0.3+debian-1_arm64.deb


Run:

	guvcview (from command line) or use the menu

or

	guvcview -d /dev/video0 -x 640x480 -r sdl -f yu12
	guvcview -d /dev/video0 -x 640x480 -r sdl -f nv12


History
-------

* Initial commit
* Fix for Gtk3 Gui to start correctly on any win size, you are now able to switch Resolutions
* additional instructions and updated deb
* Bumped version to 2.0.3 to prevent conflit with Debian Package and prepare to HW Encoder experiments


