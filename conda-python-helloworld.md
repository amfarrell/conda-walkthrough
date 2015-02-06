You are going ot create your first conda package. It will contain a single
python module that prints "Hello World!"

Part I: distutils and setup.py
==============================
A package itself is nothing more than a directory tree with some files in it.
For others to use it, they need to know some a few things that directory tree.

0) `packages`: What are the modules that other code can import?

1) `scripts`: What are the files a command-line shell can execute?

2) `metadata`: Who wrote the code? What it is named? What version it is? .. and everything else.

In python, the place to put this is a file called setup.py and so your first step is to create a small directory tree
and write setup.py.

Creating a minimal package directory tree
-----------------------------------------

                                                                 | Linux/OSX                            |  Windows
-----------------------------------------------------------------|--------------------------------------|-----------
Create a directory which will hold the entire project            | `mkdir helloworld`                   | TODO
Within that, create a directory which will hold your actual code | `mkdir helloworld/hello`             | TODO
