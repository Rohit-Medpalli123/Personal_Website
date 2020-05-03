---
layout: post
section-type: post
title: How to use Virtualenv in Python to Install Packages Locally
category: Installation
tags: [ 'Python', 'Venv' ]
---

There are two philosophies when it comes to package installation, global first and local first. Global meaning all applications that rely on a certain package have access to the same copy of the library that was installed once. Local means that each project has its own folder of dependencies installed specifically for this project and each library is installed many times. NPM, for example, uses local first strategy. Pip in Python uses global first strategy by default.

Both approaches have their benefits and drawbacks. In this post I wanted to show how to use a Python library called virtualenv to created isolated (local) python environments.

virtualenv is used to manage Python packages for different projects. Using virtualenv allows you to avoid installing Python packages globally which could break system tools or other projects. You can install virtualenv using pip.

#### Installing virtualenv:
As usual, it’s as simple as:

On macOS and Linux:

```
python3 -m pip install --user virtualenv
```

On Windows:

```
py -m pip install --user virtualenv
```

### Create a new virtual environment:
Navigate to the folder where you want the project set up and run:

```
On macOS and Linux:

python3 -m venv env

On Windows:

py -m venv env
or
virtualenv any_name_you_want
```

The second argument is the location to create the virtual environment. Generally, you can just create this in your project and call it env.

venv will create a virtual Python installation in the env folder.

*_Note_* You should exclude your virtual environment directory from your version control system using .gitignore or similar.
This will set up Python as well as pip that you can use locally.

#### Activating Virtual Environment:
At this point we are still running Python in usual mode and running pip install will install a package globally.

We need to “switch” into the virtual environment by running the activation command:

```
On macOS and Linux:

source env/bin/activate

On Windows:

.\env\Scripts\activate
```

You can confirm you’re in the virtual environment by checking the location of your Python interpreter, it should point to the env directory.

```
(venv) $ which python
/someproject/venv/bin/python

(venv) $ which pip
/someproject/venv/bin/pip
```
which will show that both Python and Pip are running locally.

As long as your virtual environment is activated pip will install packages into that specific environment and you’ll be able to import and use packages in your Python application.

Using the Virtual Environment
This is really it. You can now do your work in the virtual environment and anything installed with pip install will show up in your local venv folder.

For example let’s install Pandas.

```
(venv) $ pip install pandas
# ... pip magic

(venv) $ ls /someproject/venv/lib/python3.6/site-packages/ | grep pandas
pandas
pandas-0.23.4.dist-info
```

Deactivating the Virtual Environment
When you are done with local environment, simply run deactivate in your shell to go back to the regular Python flow.

```
(venv) $ which python
/someproject/venv/bin/python

(venv) $ deactivate

$ which python
/usr/local/bin/python
```

To record project dependancies we just have to redirect result of pip freeze into a txt file.

```
pip freeze > requirements.txt
```

Checking this file in, will make sure that the next person using this project will have the same dependencies as we did.

In any case, now that our dependancies are installed, we are ready to run the repo. Once we are done, we can de-activate it or simply exit this shell session.

```
deactivate
```
That’s really it. In true spirit of Python – using virtualenv is very simple and effective.



#### References:
[Python official docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

[Article](https://www.alexkras.com/how-to-use-virtualenv-in-python-to-install-packages-locally/)


