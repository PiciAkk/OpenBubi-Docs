# <p align="center">Built-in functions of the Dart package</p>

## `BubiUser(phoneNumber, pin)` (*phoneNumber, and pin needs to be a string*)

- `info()` (async) - returns user information in JSON (not map) format -> if you want it in map format, `import json`, and use `json.decode(info())`
- `getScreenName()` (async) - grabs the screen name from `info()`, and returns it
- `getLoginKey()` (async) - grabs the login key from `info()`, and returns it
- `callOtherEndpoint(relativeURL, data)` (async) - (*relativeURL needs to be a string, and data needs to be a map*) calls the specified `endpoint` with the specified `data` (plus `loginkey`, `domain`, `apikey`, `show_errors`), and returns the output. (*you can find endpoints [here](https://github.com/h0chi/nextbike-api-reverse-engineering)*)
- `rentBike(bikeNumber)` (async) - (*bikeNumber needs to be an integer*) rents a bike, and returns the output
- `getRentals()` (async) - returns information about the user's rentals
- `getClosedRentals()` (async) - returns closed rentals from `getRentals()`
- `getActiveRentals()` (async) - returns active rentals
- `getPaymentLinks()` (async) - returns information about payment links
- `getSubscriptionInfo()` (async) - returns the end of the subscription, and the type of the subscription
- `getSubScriptionType()` (async) - returns the type of the subscription based on `getSubscriptionInfo()` (monthly, or annual)
- `getEndOfSubscription()` (async) - returns the end of the subscription based on `getSubscriptionInfo()` (date)
- `moreInfo()` (async) - returns a LOT of information about the user
- `getRentalDetails()` (async) - returns information about the current rental

## `BubiMap()`

- `listAllStations()` (async) - returns a JSON object containing all stations
- `listAllBikes()` (async) - returns a JSON object containing all bikes
- `listAllBikesFormatted()` (async) - returns a JSON object containing all bikes (without the unnecessary parts)
- `listAllStationsFormatted()` (async) - returns a JSON object containing all stations (without the unnecessary parts)
- `getNearestStations(lat, lon)` (async) - (*lat, and lon needs to be a float*) returns a JSON object containing all stations, sorted by proximity to `lat`, and `lon`. Distance is counted in geographical degrees. (calculated using the Pythagorean theorem)
- `getNearestStation(lat, lon)` (async) - (*lat, and lon needs to be a float*) returns the nearest station's name by latitude, and longitude (based on the first key of `getNearestStations`)
- `getNearestStationByAddress(address)` (async) - returns the nearest station's name by address (using `getNearestStation()`, and OpenStreetMap API)
- `listAllBikesOnStations(stationName)` (async) - returns all the bikes on a station (and the number of these bikes, and information about these bikes)
- `countBikesOnStation(stationName)` (async) - counts all the bikes on a station (using `listAllBikesOnStation()`), and returns the counter
- `getCoordinatesOfStation(stationName)` (async) - returns the coordinates of a station (latitude, longitude)

## `BubiHelpers()`

- `register()` - *Work in progress...*
- `pinReset(mobile)` - *Work in progress...*
- `getNews()` (async) - Returns all the news in a JSON format
- `getNewsFormatted()` (async) - Returns all the news from the mobile app without the unnecessary parts (based on `getNews()`)
- `readNew(uid)` (async) - Returns the HTML page of a specific new article with the given uid (based on `getNewsFormatted()`) (*uid needs to be an integer*)
