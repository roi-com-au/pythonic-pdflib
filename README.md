# PythonicPdflib

PythonicPdflib is an attempt to create a more "pythonic" API for PDFlib.

## Input Attributes

Many methods within PDFlib require "odd" or un-pythonic input attributes for their default values.

PythonicPdflib behaves how you would expect a Python API to behave - that is, sensible defaults and options are a dict, not a string of space separated values.

## Color Data Type

Rather than define RBG as a float between 0-1 you can define as an integer between 0-255, as follows:

```python
from pythonic_pdflib import RGBColor

fillcolor = RGBColor(255, 255, 255)
tf = p.add_textflow(title, options={'fillcolor': fillcolor})
```

Note this behaviour needs to be implemented for CMYK, grey and the other color data types. Feel free to fork and submit a pull request.

## Context Managers

There are a lot of `begin_*` methods which each require their associated `end_*` method to be called once you've finished using them.

PythonicPdflib provides context managers which allow you to use the `with` statement to manage the relevant calls to `begin_*`/`end_*`.

All `begin_*`/`end_*` and some `open_*`/`close_*` methods have a corresponding context manager simple titled as the last part of the method. For example, instead of using `begin_font`/`end_font` simply use `font`.

For example:

```python
p = PythonicPDFlib({'license': 'my-license'})
with p.document('/path/to/my.pdf'):
    # do stuff
```

vs.

```python
p = PDFlib()
p.set_option('license=my-license')
p.begin_document('/path/to/my.pdf', '')
# do stuff...
p.end_document('')
```

## Version

PythonicPdflib is currently considered alpha - the API will likely change as it's in active development.

## Author

Alex Hayes <alex@alution.com>

## Thanks

Thanks to [roi.com.au](http://roi.com.au) for allowing this code to be released open source.