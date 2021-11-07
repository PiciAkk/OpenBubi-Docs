# <p align="center">Making a news reader</p>

## What are we going to do?

We are going to make a Tkinter-based GUI program that lists the MOL Bubi news.

## Dependencies

The only (not preinstalled) dependency for this project is `tkhtmlview`. If you want to install it with pip, type the following command:

```bash
pip install tkhtmlview
```

## Write the program

First of all, make a new Python script in the cloned folder

```bash
mkdir bubinews && touch bubinews/bubinews.py
```

Then import all the necessary modules in the newly created program/script

```python
import sys # for manipulating the path
sys.path.append("../") # add the folder of openbubi.py to the path
import openbubi
from tkinter import * # for making the GUI
import json # for converting the output of openbubi to a dictionary
import datetime # for converting epoch time to datetime
from tkhtmlview import HTMLLabel # for displaying HTML elements in tkinter
```
