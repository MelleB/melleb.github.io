=======================================
 Org-mode show TODO keywords at bottom
=======================================

:date: 2016-04-02
:tags: emacs, org-mode, note-to-self

In org-mode you can quickly toggle todo states when you define shortcuts.
For instance, my `init.el` contains the following TODO keywords:

.. code-block:: elisp

   (setq org-todo-keywords
	  '((sequence "TODO(t)" "NEXT(n)" "IN-PROGRESS(p)" "WAITING(w)"
		      "|" "DEFERED(f)" "DONE(d)" "CANCELLED(c@)")))

This allows me to tap e.g. ``C-t n`` on a heading to change its status to
NEXT or ``C-t c`` to set it's status to CANCELLED and enter a reason. 
For more info, see `Fast access to TODO states`_ in the org-mode manual.

By default these pop-up in the other window, in my case this is often a
document which I have open in a  vertical split.
I wanted these top pop-up at the bottom of the screen.
By using the popwin_ package I was able to pull this off by adding the following lines to my config.

.. code-block:: elisp

   (require 'popwin)
   (setq display-buffer-function 'popwin:display-buffer)
   (add-to-list 'popwin:special-display-config '(" *Org todo*"))
   (popwin-mode 1)

The trick was to set the display-buffer-function to use the popwin implementation.

Hopefully this saves someone a bit of time.

.. _`Fast access to TODO states`: http://orgmode.org/manual/Fast-access-to-TODO-states.html
.. _popwin: https://github.com/m2ym/popwin-el
