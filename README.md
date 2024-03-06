# neurodesign

This package allows the optimisation of an experimental design for fMRI studies.

## Documentation

The documentation of neurodesign is available at [ReadTheDocs](http://neurodesign.readthedocs.io/en/latest/).

## File description

```
├── docs                    Contains the source code to generate the documentation with sphinx.
├── examples                Contains scripts to perform a design optimalisation.
└── neurodesign             Folder with the source code of the python package
    └── media               Folder contains the logo of neurodesign, which is used in the reports.
```
## Notes (as of 6/03/2024)
- Neurodesign website linked above is completely empty (only installation command is there)
- Installation via pip install neurodesign downloads something which is possibly not the most up to date version of the package


### Installation and usability issues (as of 6/03/2024)
**Issue 1**
```
ImportError: cannot import name 'design' from partially initialized module 'neurodesign' (most likely due to a circular import) (/Users/mkachlicka/anaconda3/lib/python3.11/site-packages/neurodesign/__init__.py)
```

Solved by updating __init__.py to the following:
```
# Import design and experiment directly from neurodesign module
from .neurodesign import design, experiment, optimisation 

# Expose necessary symbols at the module level
__all__ = ['design', 'experiment', 'optimisation', '__version__', '__author__', '__license__', '__email__', '__status__', '__url__', '__packagename__']

# Import information from info module
from .info import (
    __version__,
    __author__,
    __license__,
    __email__,
    __status__,
    __url__,
    __packagename__,
)

```

**Issue 2**
Dependencies not mentioned in the install guide
```
pip install reportlab
pip install pdfrw
import io # Replace all instances of import cStringIO or import StringIO
pip install progressbar2
```

**Issue 3**
```
NameError: name 'xrange' is not defined
```

There is no such function in Python 3. Replace all instances with range

**Issue 4**

```
AttributeError: module 'sys' has no attribute 'exc_clear'

```

The sys module in Python 3.11 does not have the attribute exc_clear() anymore. This method was used to clear the exception information from the current thread of control, but it's been removed in Python 3.11. You should remove the line sys.exc_clear() from the neurodesign.py file or update it to handle exceptions differently ( I just removed them)

**Issue 5**

```
UserWarning: Matplotlib is currently using agg, which is a non-GUI backend, so cannot show the figure.
```

It seems that Matplotlib is currently using a non-GUI backend (agg), which means it cannot display the figure directly. This commonly happens when you're running code in an environment without a graphical user interface, such as certain IDEs or when running code in a terminal without GUI support.

```
plt.savefig('plot.png')
```