
=========================================
 Highlight python class and method names
=========================================

:date: 2016-06-24
:tags: emacs, python

Recently I began working on a personal python-based project. Having
worked with python in the past, it was a welcoming experience. I
wasn't really used to a indent-sensitive language. And I figured I
could use some visual aids to quickly tell class and method
definitions apart when scanning source files.

In my Emacs set-up I use the `leuven theme`_. It's quite a minimal
theme, which seems especially geared towards the use of org-mode. For
non-emacs converts, one of the benefits of the Emacs display system is
that you can have different font faces in a single document. For
instance, the leuven theme uses a bigger font size for level 1
headings, and gives each level a different background color.

I figured I wanted something like that for class and method
definitions. After some fiddeling around, I'm satisfied with the
following snippet:

.. code-block:: elisp

    (font-lock-add-keywords 'python-mode
     '(("^\s*\\(def\s*\\)\\(.*\\)\\((.*):.*\xa\\)" ; Highlight "def my_func(param):"
	(1 '(:inherit font-lock-keyword-face :background "#F3F3F3"))
	(2 '(:inherit font-lock-function-name-face :background "#F3F3F3" :weight bold))
	(3 '(:background "#F3F3F3"))
	)
       ("^\s*\\(class\s*\\)\\(.*\\)\\((.*):.*\xa\\)" ; Highlight "class MyClass(Base):"
	(1 '(:inherit font-lock-keyword-face :background "#EEEEEE" :height 1.4))
	(2 '(:inherit font-lock-function-name-face :background "#EEEEEE" :height 1.4 :weight bold))
	(3 '(:background "#EEEEEE" :height 1.4))
	)
       ("^\s*\\(class\s*\\)\\(.*\\)\\(:.*\xa\\)"  ; Highlight "class MyClass:"
	(1 '(:inherit font-lock-keyword-face :background "#EEEEEE" :height 1.4))
	(2 '(:inherit font-lock-function-name-face :background "#EEEEEE" :height 1.4 :weight bold))
	(3 '(:background "#EEEEEE" :height 1.4))
	)
       ))

With some more work I could probably reduce this to a single regex. Oh
well. Anyway, here's a screenshot with the result:

.. image:: {attach}/images/007-highlight-class-method-defenitions.png
	   :alt: Highlight python source code
	   :width: 851
	   :height: 700

I opened an issue_ on the Leuven Theme github repo, to see if others
like this as well.

.. _`leuven theme`: https://github.com/fniessen/emacs-leuven-theme
.. _issue: https://github.com/fniessen/emacs-leuven-theme/issues/29



