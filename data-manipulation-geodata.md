# Data manipulation GeoData

## Cartopy module

### Night France Map view

```python
import matplotlib.pyplot as plt
import cartopy.crs as ccrs

url = 'https://map1c.vis.earthdata.nasa.gov/wmts-geo/wmts.cgi'
layer = 'VIIRS_CityLights_2012'

fig = plt.figure(figsize=[10,8])
ax = fig.add_subplot(1, 1, 1, projection=ccrs.PlateCarree())
ax.add_wmts(url, layer)
ax.set_extent([-5, 9, 51, 42], crs=ccrs.PlateCarree())

plt.plot(2.21, 48.85,  markersize=10, marker='o', color='red')

ax.set_title('France map night April/October 2012')
plt.show()
```
