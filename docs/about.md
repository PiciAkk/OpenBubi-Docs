# <p align="center">About</p>

#### Known issues

1. We assume that Budapest is a small city

Budapest is a "small" city, but with a potentially larger city (or even a country), the algorithm wouldn't work, because it doesn't account with the curvature of the Earth. So for OpenBubi to work on larger cities, it needs to switch to the Haversine-formula instead of the Pythagorean-theorem.

But the Haversine-formula isn't perfect either, because it doesn't account with the Earth being a geoid, not sphere.

I think I'll use 3rd party libraries, like [geopy](https://pypi.org/project/geopy/).

---

#### Thanks for the help in the reverse engineering, [Brúnó Salomon](https://github.com/bru02)
