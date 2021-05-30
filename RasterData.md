
## Read shape file with geopanda

```python
import geopandas as gpd
import matplotlib.pyplot as plt

gdf = gpd.read_file('C:/Users/liu34/OneDrive/OSU/Working Papers/5 Guyana and Suriname/Data/Geographic files/Surinam_files/sur_admbnda_adm1_2017.shp') 
# 使用文件所在路径

print(gdf.shape)
print(gdf.head)

gdf.plot()
plt.show()
```

## Show a preview of graph
*(Ref: https://towardsdatascience.com/reading-and-visualizing-geotiff-images-with-python-8dcca7a74510)*


```python
from rasterio.plot import show

fp = r'GeoTiff_Image.tif'
img = rasterio.open(fp)
show(img)
```


# References

使用Raster读取栅格数据: https://theonegis.github.io/geos/%E4%BD%BF%E7%94%A8Rasterio%E8%AF%BB%E5%8F%96%E6%A0%85%E6%A0%BC%E6%95%B0%E6%8D%AE/index.html

Rasterio Guide: https://rasterio.readthedocs.io/en/latest/index.html

知乎专栏--地理信息及图像处理: https://www.zhihu.com/column/c_1253474882190192640

tifffile -- read and write tiff files: https://github.com/cgohlke/tifffile

遥感数据处理: https://blog.csdn.net/z704630835/article/details/83349551
