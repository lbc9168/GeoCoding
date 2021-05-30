
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

## Splitting raster data
*(Ref: https://www.youtube.com/watch?v=p_BsFdV_LUk&list=PL4aUQR9L9RFp7kuu38hInDE-9ByueEMES&index=1)*

```python
# splitting raster data

from osgeo import gdal
import matplotlib.pyplot as plt

dem = gdal.Open("C:/Users/liu34/OneDrive/OSU/Working Papers/5 Guyana and Suriname/Data/TMF_data/AnnualChange/JRC_TMF_AnnualChange_v1_1990_SAM_ID49_N10_W60.tif")
gt = dem.GetGeoTransform()

xmin = gt[0]
ymax = gt[3]
res = gt[1]

xlen = res * dem.RasterXSize     # 0.000269 decimal degrees = 30m
ylen = res * dem.RasterYSize

# seprate by 5*5
div = 5

xsize = xlen/div
ysize = ylen/div

xsteps = [xmin + xsize * i for i in range(div+1)]
ysteps = [ymax - ysize * i for i in range(div+1)]

for i in range(div):
    for j in range(div):
        xmin = xsteps[i]
        xmax = xsteps[i+1]
        ymax = ysteps[j]
        ymin = ysteps[j+1]
        
        print(i,", ",j)
        print("xmin: "+str(xmin))
        print("xmax: "+str(xmax))
        print("ymin: "+str(ymin))
        print("ymax: "+str(ymax))
        print("\n")

        gdal.Warp("dem"+str(i)+str(j)+".tif", dem, 
                  outputBounds = (xmin, ymin, xmax, ymax), dstNodata = -9999)


ds = gdal.Open("dem01.tif")
band = ds.GetRasterBand(1)
array = band.ReadAsArray()

plt.figure()
plt.imshow(array)

ds1 = gdal.Open("dem00.tif")
band1 = ds1.GetRasterBand(1)
array1 = band1.ReadAsArray()

plt.figure()
plt.imshow(array1)
```


# References

使用Raster读取栅格数据: https://theonegis.github.io/geos/%E4%BD%BF%E7%94%A8Rasterio%E8%AF%BB%E5%8F%96%E6%A0%85%E6%A0%BC%E6%95%B0%E6%8D%AE/index.html

Rasterio Guide: https://rasterio.readthedocs.io/en/latest/index.html

知乎专栏--地理信息及图像处理: https://www.zhihu.com/column/c_1253474882190192640

tifffile -- read and write tiff files: https://github.com/cgohlke/tifffile

遥感数据处理: https://blog.csdn.net/z704630835/article/details/83349551
