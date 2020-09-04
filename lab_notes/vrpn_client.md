---
title: VRPN Client for Python3.X
layout: template
filename: vrpn_client.md
--- 

### How to install a vrpn client in Python3.X

#### From system interpreter (Linux)

First of all, it is useful to have Python3.X installed under `/usr/local/lib` or somewhere under `/usr/`. If you know the version of python you'd like to use for `vrpn` go to the command terminal and check out `which python3.X` and locate that folder, whithin that folder,  it is important that you know the absolute path of where `dist-packages` is under library and the `include` path under that folder. In my case it is: 

```
/usr/local/include.python3.X
/usr/local/lib/python3.X/dist-packages
```

Then, clone the `vrpn` repository anywhere in your computer. 

```
$ git clone https://github.com/vrpn/vrpn
```

```
$ cd vrpn
$ edit python_vrpn/Makefile.python
```

Here you are going to make the following changes: 

> include ../Makefile</br>

> PYTHON_VER := ~~$(shell /usr/bin/python -V 2>&1 | sed 's/^[^0-9]*\([0-9]\+.[0-9]\+\)[^0-9].*/\1/')~~ **3.X** </br>
> VRPN_ROOT_DIR := ..</br>
> OBJECT_DIR := $(VRPN_ROOT_DIR)/$(OBJECT_DIR)</br>
> PYTHON_INCLUDE_DIR := ~~/usr/include/python$(PYTHON_VER)~~ **/usr/local/include/python3.X**</br>
> PYTHON_LIB := python$(PYTHON_VER)</br>
> PYTHON_PACKAGES_DIR := ~~$(LIB_DIR)/python$(PYTHON_VER)/dist-packages~~ **/usr/local/lib/python3.X/dist-packages**</br>
> QUAT_INCLUDE_DIR := $(VRPN_ROOT_DIR)/quat</br>
> QUAT_LIB_DIR := $(QUAT_INCLUDE_DIR)</br>
> QUAT_LIB := quat</br>
> </br>
> [...]</br>

After you save that file then build the vrpn project. 

```
$ cd .. && mkdir build && cd build
$ cmake ..
$ make vrpn-python
$ sudo make install vrpn-python
```

##### Possible issue: 

**`vrpn` module appears to be installed because `python3.X -c "import vrpn"` doesn't lead to any errors, however, when we check out the arguments that exist in the package by `python -c "import vrpn; print(dir(vrpn))"` only shows `['__doc__', '__file__', '__loader__', '__name__', '__package__', '__path__', '__spec__']` instead of `['__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', 'error', 'quaternion', 'receiver', 'sender']
`**  

This occurs because `vrpn.so` is not under `/usr/local/lib/python3.X/dist-packages/`. All you have to do is go to where you built the vrpn python client and find a file called `vrpn.so` then `sudo cp vrpn.so /usr/local/lib/python3.x/dist-packages/`.

#### For `conda` environmnents:

