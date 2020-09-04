### How to install a vrpn client in Python3.X

#### From system interpreter (Linux)

First of all, it is useful to have Python3.X installed under `/usr/bin

##### Possible issue: 

**`vrpn` module appears to be installed because `python3.X -c "import vrpn"` doesn't lead to any errors, however, when we check out the arguments that exist in the package by `python -c "import vrpn; print(dir(vrpn))"` only shows `['__doc__', '__file__', '__loader__', '__name__', '__package__', '__path__', '__spec__']` instead of `['__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', 'error', 'quaternion', 'receiver', 'sender']
`**  


#### From `conda` environment

