***** The "Octopus" (previously Weeping Willow) affordable Rasp Pi SD Cloner / Writer *****

We (Naturebytes) had to come up with our own in-house method of mass SD card cloning / duplication to write the 300+ Kickstarter kit SD cards needed for the Wildlife Cam Kit.  

To copy a vast number of SD images we would have needed to invest in a professional SD card duplicator, but even a 1-31 machine can cost shy of £2,400, so we decided to use the humble Raspberry Pi and individual USB writers as a network, ending up with what appeared to originally look like a weeping willow SD card writer, only later to become more of an octopus – which fits into the Naturebytes family quite well we thought.

This repo is a how-to guide so you can build your own device if you ever feel the burning need to clone many hundreds of SD cards on the cheap.

*****

![The original Weeping Willow prototype](http://naturebytes.org/wp-content/uploads/2015/12/SD_writer1.jpg? "The original Weeping Willow prototype")

***** How to guide *****

* Hardware needed:

   * Raspberry Pi (cheapest with embedded ethernet - we use the Pi Model B)
   * Cat5 cables (as many pieces as you have Pis and one for your host laptop / desktop)
   * Micro USB cables (for the Rasp Pis)
   * Host SD cards large enough to fit your image and SD cards that you intend to write it to
   * USB SD card writer (linux compatible, i.e Pluggable variety)
   * Anker USB multi-port charger (i.e PowerPort 40W)
   * Switch (as many ports as you need, we used a 16 port Netgear Prosafe but the 5 port TP-Link is incredibly cheap if you only need to write 4 SDs at the same time)
   * Host machine (laptop, another Pi, whatever you enjoy that has ethernet)
   
Once you've got the hardware in place, attach each Rasp Pi to the switch via the Cat5 cables and attach a USB writer to each Pi in turn. Load each writer with a formatted SD card that you indend to write to. Ensure the capacity of the card is large enough to fit the image that you are going to write to it.

Next, we need to create the host SD card that will contain the image file and an OS to boot the Pi. Download Raspbian Jessie Lite (or just Raspbian if you want, but the Lite version is fine). Write this to the host SD card. If you are burning an 7.4GB image you're going to want a card larger than 8GB to do the job, do get a 16GB to be safe for example. Write the OS to is using WinDiskImage32 if on Windows (download it and search for a guide showing you how to write an image), or the standard way if doing it in Linux. Run this from your SSH command line once the USB writer is attached is so:

sudo dd bs=4M if=path_to_your_img.img of=/dev/sdb

Be sure to change /dev/sdb to your path. Check the path by typing "df" in the command line and check what it is.

Once you have written the OS we're going to want to copy the image you intend to write to each of the cards to it so you can access it when we login and tell each Rasp Pi to begin writing. Copy it to a folder (such as /home) on the host SD card. If on Windows, write the image to one of your SD cards and we'll read it using a Rasp Pi and save it to the host that way, but before we go, read the next section.

**** Setting up the hostname for each Rasp Pi writer ****

We're going to make life easy and use mDNS (Bonjour / Avahi) to connect to each Rasp Pi. This means we don't need a DHCP server and that each Rasp Pi will be discoverable and connectable on the same network. Avahi is pre-installed with Jessie, but if you are connecting from a Windows PC you will want to install Bonjour so yu can discover mDNS devices. Macs already have it by default as it's used by iTunes.

Once done, connect the Rasp Pi to your switch, and your PC to the switch too. Download a program called PuTTy that allows us to connect to the command line of the Rasp Pi if on Windows. The default hostname of a Rasp Pi using Jessie is raspberrypi. We can connect to it by selecting SSH in PuTTy. Change the port to 22 and enter raspberrypi.local as the host.

raspberrypi.local

Click open and a command line will load. You should see "Login as:"

Enter: raspberry
Password: pi


   