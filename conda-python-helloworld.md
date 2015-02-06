You are going ot create your first conda package. It will contain a single
python module that prints "Hello World!"

Part I: distutils and setup.py
==============================
A package itself is nothing more than a directory tree with some files in it.
For others to use it, they need to know some a few things that directory tree.

* `packages`: What are the modules that other code can import?

* `scripts`: What are the files a command-line shell can execute?

* `metadata`: Who wrote the code? What it is named? What version it is? .. and everything else.

In python, the place to put this is a file called setup.py and so your first step is to create a small directory tree
and write setup.py.

Creating a minimal package directory tree
-----------------------------------------

                                                                 | Linux/OSX                            |  Windows
-----------------------------------------------------------------|--------------------------------------|-----------
Create a directory which will hold the entire project            | `mkdir helloworld`                   | TODO
Enter that directory                                             | `cd helloworld`                      | TODO
Within that, create a directory which will hold your actual code | `mkdir hello`                        | TODO
Make the code directory a python module by adding __init__.py    | `touch hello/__init__.py`            | TODO
Within the code directory, start a file to hold your code        | `touch hello/helloworld.py`          | TODO
Within the project directory, start a file to hold package info  | `touch setup.py`                     | TODO

In helloworld.py write the following
```python
#!/usr/bin/env python
def hello():
  print("Hello World!")

if __name__ == '__main__':
  hello()
```
This is both a script that you can run on the command line and a module that you can import from a python shell or another python module.
Check that it works as by calling on the command line `$ python hello/helloworld.py`. It should of course print out "hello world!".
Then run `python -c 'import hello.helloworld; hello.helloworld.hello()'

Writing setup.py
----------------
You're now ready to actually write setup.py. Begin with the following.
```python
from distutils.core import setup

setup(
  name='shrubbery',
  author='Sir Galahad',
  version='0.0.1',
  description='Prints a friendly greeting.',
  url='https://github.com/amfarrell/conda-walkthrough/blob/master/conda-python-helloworld.md',
)
```
Right now your package only has metadata. Note that the name given to setup() need not relate to the name of any module within it.
This metadata does not let the package do anything in particular and running `python setup.py build`
