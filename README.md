# Vector---geopandas-shapely


# Save geodataframe to file (if there is a problem with geometry)

```python
from geopandas import GeoSeries, GeoDataFrame
from shapely.geometry.polygon import Polygon
from shapely.geometry.multipolygon import MultiPolygon
from geopandas import GeoSeries, GeoDataFrame

shp_fn = 'segura/Crop_Classification_Delivery.shp' 
parcels = gpd.read_file(shp_fn)
gdf = gpd.GeoDataFrame(parcels, crs="EPSG:4326", geometry='geometry')
gdf["geometry"] = [MultiPolygon([feature]) if isinstance(feature, Polygon) \
    else feature for feature in gdf["geometry"]]

gdf.to_file('segura/Crop_Classification_Delivery_class.geojson' , driver="GeoJSON") 

```
