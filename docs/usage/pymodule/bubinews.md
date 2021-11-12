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

Then initialize a Tkinter window with the name `root`, and title `BubiNews`

```python
root = Tk()
root.title("BubiNews")
```

Then make a label with the text `BubiNews`. This is going to be the title

```python
Label(root, text="BubiNews", font=("Helvetica", 20)).pack()
```

Then

1. Initialize a new instance of the `BubiHelpers` class

2. Get the news in JSON format

3. Convert the news (from JSON) to dictionary format

```python
helpers = openbubi.BubiHelpers()
news = json.loads(helpers.getNewsFormatted())
```

Then iterate through the news, and make a paragraph for each

```python
for i in news:
    currentTitle = i["title"]
    # set the `currentTitle` variable to the title of the current article
    currentDate = i["created_time"]
    # set the `currentDate` variable to the created_time of the current article (it is an epoch time)
    currentURL = i["url_webview"]
    currentDate = datetime.datetime.fromtimestamp(currentDate).strftime('%Y-%m-%d %H:%M:%S')
    headerLabel = HTMLLabel(root, html=f"<a style='font-size: 12px' href='{currentURL}'><p style='text-align: center'>{currentTitle}</p></a>", width=100, height=1.5)
    dateLabel = Label(root, text=f"({currentDate})", font=("Helvetica", 10))
    headerLabel.pack()
    dateLabel.pack()
```

Then
