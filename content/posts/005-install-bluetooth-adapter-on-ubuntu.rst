
=========================================================
 Enable internal bluetooth BCM2046(B1) adapter on Ubuntu
=========================================================

:date: 2016-06-19
:tags: ubuntu
       
For some reason I couldn't get my bluetooth to work in ubuntu 16.04 on
my old Dell Vostro 3700. These are the steps I took in order to make
it work. A note to my future self.

``lsusb`` shows that there is indeed a Bluetooth device:

    Bus 001 Device 003: ID 0a5c:4500 Broadcom Corp. BCM2046B1 USB 2.0
    Hub (part of BCM2046 Bluetooth)

First diagnosis: ``sudo service bluetooth status`` showed a failed
process. After running ``sudo modprobe -r btusb; sudo modprobe
btusb``, I could start the bluetooth service without failure. Now the
bluetooth service was enabled, but no adapters were found.

I remembered disabling the bluetooth adapter under windows when I got
the laptop. I figured I didn't need it back then. This seemed to
be essential, and something the linux drivers didn't support.
According to linux, everyting was enabled.

Several fora mention extraction of linux drivers from their Windows
counterparts. I couldn't get this to work, because I couldn't
determine which driver to use.

I thought about installing windows side-by-side with Ubuntu for a
while in order to enable the bluetooth driver again. But messing
around with partitions, volumes and bootloaders seemed way too much
work just to enable bluetooth. I figured I could try running a Windows
VM, and enable the adapter in there. A long shot, but it worked!

I performed the following steps:

1. Install the bluetooth module for PulseAudio: ``sudo apt-get install
   pulseaudio-module-bluetooth``.
   
2. Install virtualbox and load a windows VM Installing virtual box is
   as simple as ``sudo apt-get install virtualbox``. You also need to
   download/install the `virtualbox extension pack`_ for USB 2.0
   support.
   
   Windows VM's are easy to come by these days, since Microsoft makes
   them publicly available for testing web development efforts against
   older MSIE versions. I got the `IE8 on Win7`_ version. Load the VM.
   
3. Next, add yourself to the ``vboxusers`` group ``sudo usermod -a -G
   vboxusers $USER``. Don't forget to logout and login again.
      
4. Add all your USB devices to the VirtualBox Go to settings > USB.
   Enable usb 2.0 and add all devices. In my case I wasn't sure which
   device was the bluetooth device, but I read on the `LinuxMint
   forum`_ that changing the mode of the wireless adapter made the
   bluetooth adapter show up. So I had a hunch where to look.
   
5. Start the VM, download the bluetooth drivers Download the drivers
   for the bluetooth dongle. In my case I entered my laptop serial
   number on the dell website and I got the *wireless* driver for
   windows 7. Make sure you download the right platform, which for me
   was 32-bit.
   
6. Install the drivers in the new VM.

After this my bluetooth adapter works. I might still need to enable
the bluetooth service using modprobe as described above. But at least
my bluetooth adapter is recognized.

.. _`virtualbox extension pack`: https://www.virtualbox.org/wiki/Downloads
.. _`IE8 on Win7`: https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/linux/
.. _`LinuxMint forum`: https://forums.linuxmint.com/viewtopic.php?t=56621
