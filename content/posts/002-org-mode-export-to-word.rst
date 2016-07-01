

=================================================
 Exporting Emacs Org documents to Microsoft Word
=================================================

:date: 2016-01-10
:tags: emacs, org-mode, note-to-self

In order to export org-mode documents to Microsoft Word I took the following steps:

1. Install Cygwin, and specifically the `unzip` executable.
   (I read Info-Zip_ seems to work, but haven't tried it myself.)
2. Set the preferred output format to `docx` :

   .. code-block:: elisp
		   
      (require 'ox-odt)
      (setq org-odt-preferred-output-format "docx")

      ;; Add cygwin to the execpath on windows to be able to export to ODF
      (when (eq system-type 'windows-nt)
        (add-to-list 'exec-path "C:\\cygwin64\\bin"))

3. Org-mode requires `soffice` executable for document conversion, which is
   part of LibreOffice. I installed the `portable version`_ of LibreOffice.
   Be sure to add the `App\\libreoffice\\program` directory to your `PATH`

4. Finally, restart Emacs.

.. _Info-Zip: http://permalink.gmane.org/gmane.emacs.orgmode/69882
.. _`portable version`: https://www.libreoffice.org/download/portable-versions/
