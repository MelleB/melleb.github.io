
=============================================
 Speeding up Emacs start-up and file loading
=============================================
:tags: emacs, note-to-self
:date: 2016-02-01

In this post I describe the steps I undertook to speed-up my Emacs under Windows 7.

Improving start-up time
-----------------------
       
My initial experience of Emacs' start-up time on Windows wasn't great.
After installing a couple of packages I noticed things became a bit slower.
I was using John Wiegley's use-package_ plugin for managing packages, this
kept everything nice and modular, however being an novice whom only recently
converted to the church of Emacs, I knew little about the things actually
happening at start-up time.

To analyse where time is spent during Emacs' start-up, I installed the
`Emacs Start Up Profiler`_ (esup) from Melpa using

.. code-block:: elisp
		
   (use-package esup
    :defer t
    :ensure t)

You can check you current start-up time and extra info by running the `esup` (``M-x esup``)
command provided by the package. This opens a new Emacs window and measures start-up time of
both the window and it's packages. You get a nice report in your current Emacs window.

After running these I noticed several most of the packges were loaded during
Emacs start-up, which wasn't really necessary. By adding the ``:defer t`` option
to my ``use-package`` statements, package loading was deferred until the packages
were actually required. Already I noticed quite a speed-up. Running the `esup` command again
confirmed this.

Another trick I used was the increase of the threshold for garbage collection.

.. code-block:: elisp
		
   (setq gc-cons-threshold 100000000)

Finally I used the `auto-compile` to - wait for it - auto compile `.el` files on save.

.. code-block:: elisp
		
   (use-package auto-compile
    :ensure t
    :config
    (auto-compile-on-save-mode))

Improving file-load time
------------------------
Another thing that bothered me was the time it took to navigate and
load a file. File loading under windows took way too much time.
Being used to vim, this was actually pretty frustrating.

You can use `C-h v find-file-hook` to describe the list of file hooks used when opening files.
It seemd git was the culprit here, and after some digging, I eventually found `this answer`_
which points to `a question`_ on StackOverflow with more info.

I'm not using git via Emacs, so the fix was pretty easy.

.. code-block:: elisp
		
   (when (eq system-type 'windows-nt)
    (progn
      (remove-hook 'find-file-hooks 'vc-find-file-hook)
      (setq vc-handled-backends nil)
      ))

I hope this saves someone (or the future me) some time.

      
.. _use-package: https://github.com/jwiegley/use-package
.. _`Emacs Start Up Profiler`: https://github.com/jschaf/esup
.. _`this answer`: http://stackoverflow.com/a/13256456/1293385 
.. _`a question`: http://stackoverflow.com/q/6724471/1293385
