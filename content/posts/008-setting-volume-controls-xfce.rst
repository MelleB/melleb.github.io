
==================================
 Fixing volume buttons under XFCE
==================================

:date: 2016-06-28
:tags: ubuntu, xfce, note-to-self

Under XFCE my keyboard's volume buttons didn't work.
The start/pause, stop, forward and backward buttons were controlling
Rhythmbox correctly, but the volume buttons weren't configured.

You have to add the shortcuts manually in keyboard application shortcuts
(Settings Manager > Keyboard > Application Shortcuts). 

+-----------------------+-------------------------+
|Shortcut               |Command                  |
+=======================+=========================+
|XF86AudioLowerVolume   |amixer set Master 5%+    |
+-----------------------+-------------------------+
|XF86AudioRaiseVolume   |amixer set Master 5%-    |
+-----------------------+-------------------------+
|XF86AudioMute          |amixer set Master toggle |
+-----------------------+-------------------------+

