> Audience:
> This is targeted at folks who have used python but have never made or uploaded any packages to pypi and are not familiar with [Ana]conda.
> It is also targeted at folks who have been using [Ana]conda but have not actually built any packages for it.
> I would like it to be targeted at folks who *have* built pypi packages, but I don't know what assumptions they'll be making.



You are going to create your first conda package. It will contain a single
python module that prints "Hello World!" and will be installable on any Windows, Linux, or OSx platform.

Part 0: Installing Conda and setting up a sandbox conda environment
-------------------------------------------------------------------
If you have not already installed the [Anaconda](http://docs.continuum.io/anaconda/install.html) distribution of python,
then install [miniconda](http://conda.pydata.org/miniconda.html). This includes the package management tool `conda` which you will
be creating packages for. Conda also enables you to create sandboxed environments similar to virtualenv. Before we begin, create a
new environment with `conda create --name hello-test python=3.4` and then activate it with `source activate hello-test`.

TODO: talk more about what conda actually is for someone who has never encountered it.
TODO: have them install the utility `tree`, because it is super userful for checking their work. Does something similar exist on windows?

Part I: distutils and setup.py
==============================
Before we create a conda package, we must first create a basic python package.
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

If you run `tree .`, you should see
├── hello
│   ├── __init__.py
│   └── helloworld.py
└── setup.py

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
> Before we go on, make sure you are have activated a conda environment. Check that the result of running `echo $CONDA_DEFAULT_ENV` is 'hello-test'. If it isn't, run `conda create --name hello-test python=3.4; source activate hello-test`.

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
Right now your setup.py includes only metadata.
Run `python setup.py --name`, `python setup.py --author`, or `python setup.py --version`. to see it.
Note that the name given to setup() need not relate to the name of any module within it. This metadata might be useful for an index like PyPI or binstar.org, but does not help the user install anything.

Add `scripts=['hello/helloworld.py']` to the arguments, then run `python setup.py build`. Your directory tree should look like

├── build
│   └── scripts-3.4       #This will be scripts-2.7 if you run python2.7
│       └── helloworld.py
├── hello
│   ├── __init__.py
│   └── helloworld.py
└── setup.py

You can run `./build/scripts-3.4/helloworld.py` and see that script now has execute permissions. Now, clean that up with `rm -rf ./build` and install the script with `python setup.py install`.
You'll see that helloworld.py has now been put as an executable in /miniconda/envs/helloworld-test/bin/ (or /anaconda/envs/helloworld-test/bin/). Run it directly with `helloworld.py`. Congratulations! You've successfully built your first installable python package.

Sections to write:
- About the 'scripts' and 'packages' arguments.
- The effect of `python setup.py build`.
- About how to find scripts and how to find modules to demonstrate what `python setup.py install` did.


Conda NoArch
============
We'll write this section for building a conda package as a noarch package.

Binstar Upload
==============
I don't think binstar upload functionality exists yet for conda-noarch.
