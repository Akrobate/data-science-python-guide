# Data manipulation GeoData

## Cartopy module

### Night France map view

```python
import matplotlib.pyplot as plt
import cartopy.crs as ccrs

url = 'https://map1c.vis.earthdata.nasa.gov/wmts-geo/wmts.cgi'
layer = 'VIIRS_CityLights_2012'

fig = plt.figure(figsize=[10,8])
ax = fig.add_subplot(1, 1, 1, projection=ccrs.PlateCarree())
ax.add_wmts(url, layer)
ax.set_extent([-5, 9, 51, 42], crs=ccrs.PlateCarree())

# Paris marker
plt.plot(2.21, 48.85,  markersize=10, marker='o', color='red')

ax.set_title('France map night April/October 2012')
plt.show()
```

### Stamen France map view

```python
import matplotlib.pyplot as plt
import cartopy.crs as ccrs
import cartopy.io.img_tiles as cimgt
import cartopy.feature as cfeature

# Create a Stamen terrain background instance.
stamen_terrain = cimgt.Stamen('terrain-background')

fig = plt.figure(figsize=[10,8])

# Create a GeoAxes in the tile's projection.
ax = fig.add_subplot(1, 1, 1, projection=stamen_terrain.crs)
ax.set_extent([-5, 9, 51, 42], crs=ccrs.Geodetic())

# Add the Stamen data at zoom level 8.
ax.add_image(stamen_terrain, 8)
ax.add_feature(cfeature.COASTLINE)
ax.add_feature(cfeature.BORDERS, color='red')

# Paris marker
plt.plot(2.21, 48.85,  markersize=10, marker='o', color='red', transform=ccrs.Geodetic())

plt.show()
```