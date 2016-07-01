
Installation of blog dev env
============================

Create a separate virtual environment for the blog, e.g.
``pyenv virtualenv 3.5.1 pelican-3.5.1``

Switch to new environnment
``pyenv local pelican-3.5.1``

Install pelican
``pip install pelican when-changed``

Automatic rebuild on changes
``./watch.sh``

Serve local
``cd output && python3 -m http.server``
