---
layout: post
title: "Fedora 20 on VirtualBox. No Wayland for you!"
category: posts
---

Today I tried to install Fedora 20 on VirtualBox. I'm writing to guide voyagers on what NOT to do if you really want to try it on VirtualBox.

## Don't install Guest Additions

After installing on VirtualBox VM, I've updated all the packages prior to installing Guest Additions. Fired up Terminal and:

	sudo yum upgrade && sudo reboot

To get VirtualBox integration working I had to install some software,

	sudo yum install kernel-headers kernel-devel gcc make bzip2 dkms  
	
setup an environment variable pointing to the where the kernel headers are installed:

	KERN_DIR=/usr/src/kernels/`uname -r`
	
mounted Guest Additions image into VM (Host+D), navigated to it, and ran installer:

	cd /var/run/media/YOUR_USERNAME/
	cd VBOXADDITIONS_X.Y.ZZ_RRRRR
	sudo ./VBoxLinuxAdditions.run
	
where X.Y.ZZ_RRRRR was my VirtualBox version.

After rebooting the system things got really scary, I got a very buggy and slow piece of software. Seems like Guest Additions just screwed up video. 

### Conclusions

To get it kind of usable you should disable 2D/3D acceleration on VirtualBox and forget about Guest Additions on Fedora 20. It renders system unusable.

## [X11 sucks](http://www.youtube.com/watch?v=RIctzAQOe44), what about Wayland?

The latest packages support running GNOME 3.10 over Wayland, but it's still not the default session. You must switch to a VT (Ctrl+Alt+F2) and start the session manually:

	gnome-session --session gnome-wayland

On VirtualBox the command blinks screen and then returns to VT without any error. 

I can't tell this exactly, as things evolves really fast with Wayland, but as far as I know at this moment Wayland works only on Intel graphic cards. So, still no VirtualBox fun for you!

---

_Hey, this is my first post here_