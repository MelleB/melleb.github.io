
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

.. _`HK Esquire Bluetooth Speaker`: http://www.harmankardon.com/bluetooth-speakers/ESQUIRE.html
