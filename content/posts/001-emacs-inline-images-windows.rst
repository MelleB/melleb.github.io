
===========================================
 Showing inline images in Emacs on Windows
===========================================

:date: 2016-01-05
:tags: emacs, org-mode, note-to-self

For me `M-x` `org-display-inline-images` didn't work on windows.
The error I get is: `"No images to display inline"`

Googling gave me this_, but that didn't really help...

Eventually the README_ in the Emacs downloads folder was more helpful: 

::

  Emacs can also support some other image formats with appropriate
  libraries.  These libraries are all available on the following sites:

  1. http://sourceforge.net/projects/ezwinports/files/
     -- leaner, more up-to-date builds, only for 32-bit Emacs
  2. http://www.gtk.org/download/win32.php
     http://www.gtk.org/download/win64.php
     -- the GTK project site; offers much fatter builds, but includes
        64-bit DLLs (from the 2nd URL)
  3. GnuWin32 project -- very old builds, not recommended


So in order to view inline images you should get the ezwinports of
libpng_, giflib_, jpeg_ and librsvg_

Unzip these files and add the directories to PATH.
After this, `org-display-inline-images` seemd to work for me.

Tested with Emacs 24.5, org-mode 8.3.3 on windows 7.

Hope this saves somebody some time.

..  _this:    https://www.gnu.org/software/emacs/manual/html_node/efaq-w32/Image-support.html#Image-support
.. _readme:  http://ftp.snt.utwente.nl/pub/software/gnu/emacs/windows/README
.. _libpng:  http://sourceforge.net/projects/ezwinports/files/libpng-1.6.12-w32-bin.zip/download
.. _giflib:  http://sourceforge.net/projects/ezwinports/files/giflib-5.1.0-w32-bin.zip/download
.. _jpeg:    http://sourceforge.net/projects/ezwinports/files/jpeg-v9a-w32-bin.zip/download
.. _librsvg: http://sourceforge.net/projects/ezwinports/files/librsvg-2.40.1-2-w32-bin.zip/download 

