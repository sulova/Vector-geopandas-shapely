# Vector---geopandas-shapely


Problems: *GeometryTypeValidationError: Record's geometry type does not match collection schema's geometry type: 'MultiPolygon' != 'Polygon'*


- Save geodataframe to file (if there is a problem with geometry)

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

- change values based on condition

```python
gdf_stat_merge.Class = np.where(((gdf_stat_merge.C21_M05.eq('LAC')) & (gdf_stat_merge.Class_name.eq('Olivos'))),'OV_LAC', gdf_stat_merge.Class)
gdf_stat_merge.Class = np.where(((gdf_stat_merge.C21_M05.eq('LBC')) & (gdf_stat_merge.Class_name.eq('Olivos'))),'OV_LBC', gdf_stat_merge.Class)
gdf_stat_merge.Class_num = np.where((gdf_stat_merge.Class.eq('OV_LBC')),'5', gdf_stat_merge.Class_num)
gdf_stat_merge.Class_name = np.where((gdf_stat_merge.Class.eq('OV_LBC')),'Olivos LBC', gdf_stat_merge.Class_name)
gdf_stat_merge.Class_name = np.where((gdf_stat_merge.Class.eq('OV_LAC')),'Olivos LAC', gdf_stat_merge.Class_name)     
```
