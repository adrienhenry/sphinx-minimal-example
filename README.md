# Documenting with Sphinx #
# ![](https://upload.wikimedia.org/wikipedia/en/d/dc/Sphinx_Python_Documentation_Logo.png)
###### [http://www.sphinx-doc.org/](http://www.sphinx-doc.org/)



### Project ###

```bash
+-- Project/
|   +-- main.py
|   +-- MyClass/
|   |   +-- __init__.py
|   |   +-- function.py
```
- main.py
```python
import MyClass
MyClass.hello_world("Spam")
```
- [\_\_init\_\_.py]()
```
from .function import hello_world
```



- function.py
```python
def hello_world(name):
    """ Function that says hello to someone

    Args:
        name(string): Name of the person to greet
    Returns:
        None	
    """
    print("Hello "+name)
    return None

```

### Install Sphinx ###
```bash
sudo pip3 install sphinx
```
```bash
sudo conda install sphinx
```
 
## Configure sphinx for  _Project_ ##
Go to the _Project/_ directory an run:
```bash
.../Project$ sphinx-quickstart
## The utily allows to set a lot of parameters
## Some important ones are:
> Root path for the documentation [.]: doc/
> autodoc: automatically insert docstrings[...] (y/n): y
> Create Makefile? (y/n): y
```
It adds a _doc/_ directory in the root of the project. The _doc/_ contains a templates from wich to generate the documentation. For now the documentation is empty.



## Tell Sphinx were is the root of the project ##

In the file _Project/doc/source/config.py_, uncomment and edit the three lines as follows:
```python
import os
import sys
sys.path.insert(0, os.path.abspath('../../'))
```

Then from _doc/_, run:
```bash
sphinx-apidoc -f -o source/ ../MyClass
```



The former command explored the module looking for docstring and genrated a document file (rst format by default).

Modify the _doc/source/index.rst_ to add the module to the index:
```rst
Contents:

.. toctree::
   :maxdepth: 2
   modules
   MyClass
```



## Generate the documentation ... finaly ##

In _doc/_:
```bash
make html # or pdf or epub or ...
```

The newly generated doc is in _doc/build/html/