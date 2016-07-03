
======================================================
 Connecting my HK Esquire bluetooth speaker on Ubuntu
======================================================

:date: 2016-06-27
:tags: ubuntu, note-to-self

Some time ago I got a `HK Esquire Bluetooth Speaker`_ which is
actually a really nice, solid speaker. Pairing and connecting is easy
under Windows and Mac OS, but I couldn't get it to work on Ubuntu.

First, `I had some trouble getting my bluetooth adapter to work
<{filename}/posts/005-install-bluetooth-adapter-on-ubuntu.rst>`_,
after that the pairing worked, but I couldn't get the sound to work.
After trying several solutions metioned on different fora, the
solution was much simpler that I anticipated.

Part of the solution was to install the bluetooth module for
PulseAudio using

.. code-block:: sh

   sudo apt-get install pulseaudio-module-bluetooth

But that alone didn't fix the issue. After connecting to the speaker,
you need to kill/reset the pulseaudio deamon using

.. code-block:: sh

   pulseaudio -k

For some reason this makes the speaker show up in PulseAudio Volume
Control. My guess is that it resets the list of output devices. But I
might be wrong.

I got to choose between two audio profiles: `High Fidelity Playback
(A2DP Sink)` and `High Fidelity Headset (HSP/HFP)`. The sound output
of the High Fidelity Heaset profile was crap, which might be expected.
So I tried using the A2DP sink. It didn't work the first time, but
after trying it a week later it worked. Yay.

**Update 2016-07-04**: It turned out the problem of the A2DP sink not working was
structural. After rebooting, I could only connect to my high fidelity headset.
I came across `this post`_ on ArchLinux's forum, suggesting it might have something to do with the bluetooth discovery module being loaded before X11.
The solution was to load the bluetooth discovery module after X11 was initialized.

1. Comment out the following lines in ``/etc/pulse/default.pa`` (add a ``#``)

   .. code-block:: sh

      .ifexists module-bluetooth-discover.so
      load-module module-bluetooth-discover
      .endif

2. Modify ``/usr/bin/start-pulseaudio-x11`` and include a line to load the module after X11 has been started:

   .. code-block:: sh

      if [ x"$SESSION_MANAGER" != x ] ; then
        /usr/bin/pactl load-module module-x11-xsmp "display=$DISPLAY session_manager=$SESSION_MANAGER" > /dev/null

	# Add this single line
	/usr/bin/pactl load-module module-bluetooth-discover
      fi

3. Reboot.

After booting I'm able to connect to the A2DP sink staight away!


.. _`HK Esquire Bluetooth Speaker`: http://www.harmankardon.com/bluetooth-speakers/ESQUIRE.html
.. _`this post`: https://bbs.archlinux.org/viewtopic.php?pid=1526534#p1526534
