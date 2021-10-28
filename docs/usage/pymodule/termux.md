# <p align="center">For Termux users</p>

I'm a big fan of [Termux](https://termux.com/) (a terminal emulator and Linux environment app for Android), so I made an example program for Termux users (based on the `termux-location` command).


## A few words about `termux-location`

`termux-location` is a Termux command, that takes advantage of one of the most important features of smartphones: GPS.

`termux-location` returns the exact coordinates of the user in JSON format.

Example output:

```bash
$ termux-location

{
  "latitude": 123456.0,
  "longitude": 123456.0,
  "altitude": 123456.0,
  "accuracy": 123456.0,
  "vertical_accuracy": 123456.0,
  "bearing": 123456.0,
  "speed": 123456.0,
  "elapsedMs": 123456,
  "provider": "gps"
}
```

## What are we going to do with `termux-location`?

We are going to:

- run `termux-location` from our Python script
- parse the output JSON data of `termux-location`
- determine the user's exact location
- provide the location to OpenBubi
- make a command-line MOL Bubi detector :D

## Write the program

First of all, make a new Python script in the cloned folder

```bash
mkdir bubidetector && touch bubidetector/bubidetector.py
```

Then import all the necessary modules in the newly created program/script

```python
import sys # for path manipulation
sys.path.append("../") # add openbubi.py's folder to the current path
import openbubi
import json # for converting the command-line output to dictionary
import os # for running termux-location
import urllib.parse # for parsing urls
```

Then initialize a new instance of `BubiMap` as Budapest

```python
Budapest = openbubi.BubiMap()
```

Then run `termux-location`, and parse the output

```python
currentLocation = os.popen("termux-location").read() # read the current location

currentLocationDict = json.loads(currentLocation) # convert it to a dictionary

lat = currentLocationDict["latitude"]; lon = currentLocationDict["longitude"] # parse it
```

Then find the nearest station, and print out some information about it

```python
nearestStation = Budapest.getNearestStation(lat, lon) # call getNearestStation(), and provide lat, lon
# this will return the nearest station's name

nearestStationInfo = {
  "name": nearestStation,
  "bikesOnStation": Budapest.countBikesOnStation(nearestStation), # count the bikes on that station
  "coordinates": json.loads(Budapest.getCoordinateOfStation(nearestStation)) # get the coordinates of that station, and convert it to a dictionary
}

startingPoint = urllib.parse.quote(f"{lat},{lon}")
# make a starting point in a url-friendly format (based on the current coordinates)
destinationPoint = urllib.parse.quote(f"{nearestStationInfo['coordinates']['lat']},{nearestStationInfo['coordinates']['lon']}")
# make an ending point in a url-friendly format (based on the station's coordinates)
googlemapsurl = f"https://www.google.com/maps?f=d&saddr={startingPoint}&daddr={destinationPoint}&dirflg=d"
# generate the Google Maps URL

# ^
# |
# calculate a Google Maps route to the station

print(
 f"""
 Station found...

 Informations:

 - Station name: {nearestStationInfo["name"]}
 - Bikes on station: {nearestStationInfo["bikesOnStation"]}
 - Coordinates of station: {nearestStationInfo["coordinates"]}
 - Google Maps route to the station: {googlemapsurl}
 """
)
# printing out
```

And the final code is:

```python
import sys # for path manipulation
sys.path.append("../") # add openbubi.py's folder to the current path
import openbubi
import json # for converting the command-line output to dictionary
import os # for running termux-location
import urllib.parse # for parsing urls

Budapest = openbubi.BubiMap()

currentLocation = os.popen("termux-location").read() # read the current location

currentLocationDict = json.loads(currentLocation) # convert it to a dictionary

lat = currentLocationDict["latitude"]; lon = currentLocationDict["longitude"] # parse it

nearestStation = Budapest.getNearestStation(lat, lon) # call getNearestStation(), and provide lat, lon
# this will return the nearest station's name

nearestStationInfo = {
  "name": nearestStation,
  "bikesOnStation": Budapest.countBikesOnStation(nearestStation), # count the bikes on that station
  "coordinates": json.loads(Budapest.getCoordinateOfStation(nearestStation)) # get the coordinates of that station, and convert it to a dictionary
}

startingPoint = urllib.parse.quote(f"{lat},{lon}")
# make a starting point in a url-friendly format (based on the current coordinates)
destinationPoint = urllib.parse.quote(f"{nearestStationInfo['coordinates']['lat']},{nearestStationInfo['coordinates']['lon']}")
# make an ending point in a url-friendly format (based on the station's coordinates)
googlemapsurl = f"https://www.google.com/maps?f=d&saddr={startingPoint}&daddr={destinationPoint}&dirflg=d"
# generate the Google Maps URL

# ^
# |
# calculate a Google Maps route to the station

print(
 f"""
 Station found...

 Informations:

 - Station name: {nearestStationInfo["name"]}
 - Bikes on station: {nearestStationInfo["bikesOnStation"]}
 - Coordinates of station: {nearestStationInfo["coordinates"]}
 - Google Maps route to the station: {googlemapsurl}
 """
)
# printing out
```

## Usage

Go to the program's directory

```bash
cd bubidetector
```

Run the program

```bash
python bubidetector.py
```

Example output:

```bash
Station found...

Informations:

- Station name: Lorem Ipsum tér
- Bikes on station: 123
- Coordinates of station: {'lat': 123456.0, 'lon': 123456.0}
- Google Maps route to the station: https://www.google.com/?maps?f=d&saddr=123456.0%2C123456.0&daddr=123456.0%2C123456.0&dirflg=d
```

## Source code

I uploaded the source code of this program to [GitHub](https://github.com/PiciAkk/OpenBubi/blob/main/bubidetector/bubidetector.py)
