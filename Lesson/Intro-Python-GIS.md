# Automating GIS-processes - Lesson 1: Python GIS

## What we have learned this far - Where to find help?

At this point we have learned the basics of Python programming and used Python to automate processes in ArcGIS using arcpy module. If you have ArcGIS installation available (as we have at the University of Helsinki) it is quite straightforward to continue working with arcpy module and start building scripts that automatize and solve your own GIS-tasks/problems. ArcGIS has good [documentation](http://resources.arcgis.com/en/help/main/10.2/) and fairly active [user community](https://geonet.esri.com/community/discussions-lobby) that can help you achieving your goals. You can also search answers for your problems just by 'Googling' it. Highly active user community for coders is [StackOverFlow](http://stackoverflow.com/) from where you most probably find answers/help to different problems or errors that you might get while writing your own codes. Also [gis.StackExchange](http://gis.stackexchange.com/) is a user community that is focused ecpecially on GIS stuff, thus it can be really useful site to visit.

In addition to the online materials, there are various books that can help you going especially in the beginning of your "programming career":

- [Python Scripting for ArcGIS](http://www.amazon.com/Python-Scripting-ArcGIS-Paul-Zandbergen/dp/1589482824/ref=pd_bxgy_14_img_2/175-2574462-6134540?ie=UTF8&refRID=0HZHB9BQQWD4SKA1017A) (also [available in HELKA](https://helka.linneanet.fi/cgi-bin/Pwebrecon.cgi?BBID=2632928))
- [Learning Geospatial Analysis with Python](http://www.amazon.com/Learning-Geospatial-Analysis-Python-Lawhead/dp/1783281138)
- [Python Geospatial Development](http://www.amazon.com/Python-Geospatial-Development-Second-Edition/dp/178216152X)
- [Python for Data Analysis: Data wrangling with Pandas, NumPy and iPython](http://www.amazon.com/Python-Data-Analysis-Wrangling-IPython/dp/1449319793)

## GIS with 'pure' Python

### Why not to use specific GIS software for GIS programming?

Using a specific GIS software such as ArcGIS can be a nice way to start programming different GIS/geoprocessing functionalities with Python since all the functionalities are gathered under a single module, i.e. arcpy. However there are different reasons why you could want to move away from using e.g. ArcGIS:

- you don't have the lisence to use ArcGIS (which is fairly expensive)
- you are not happy with some of the functionalities that ArcGIS has (yes, there are bugs in the software and some functionalities such as working with attribute-tables are extremely slow in ArcGIS)
- you would like to support open source softwares/codes and open science that makes all of your work reproducible for everyone
- you would like to more easily plug-in and chain all sorts of third-party softwares that makes it possible to build e.g. as fancy web-GIS applications as you want (using e.g. [GeoDjango](https://docs.djangoproject.com/en/1.8/ref/contrib/gis/) with [PostGIS](http://postgis.net/) as a back-end)
- you would like to LEARN and UNDERSTAND much more deeply how different geoprocessing operations work

## Introduction to Python GIS

When starting to do GIS analyses/operations using pure Python we move away slightly from the *world of scripting*. When you are *scripting* it means that you are programming using only a single software or framework such as arcpy or R (statistical software). In *"real"* programming it is fairly common that you are using multiple different libraries/modules/softwares/frameworks that have been developed independently by different companies, communities, groups of people or just individual persons.

Thus, when doing data analysis or GIS with Python there are various modules that can help you get going:

- **Data analysis & visualization:**
    - [numpy](http://www.numpy.org/) --> Fundamental package for scientific computing with Python
    - [pandas](http://pandas.pydata.org/) --> High-performance, easy-to-use data structures and data analysis tools
    - [scipy](http://www.scipy.org/about.html) --> A collection of numerical algorithms and domain-specific toolboxes, including signal processing, optimization and statistics
    - [matplotlib](http://matplotlib.org/) --> Basic plotting library for Python 
    - [bokeh](http://bokeh.pydata.org/en/latest/) --> Interactive visualizations (also maps) for the web
- **GIS:**
    - [gdal](http://www.gdal.org/) --> Fundamental package for processing vector and raster data formats (many modules below depend on this)
    - [geopandas](http://geopandas.org/#description) --> Working with geospatial data in Python made easier, combines the capabilities of pandas and shapely. 
    - [shapely](http://toblerity.org/shapely/manual.html) --> Python package for manipulation and analysis of planar geometric objects (based on widely deployed [GEOS](https://trac.osgeo.org/geos/))
    - [fiona](https://pypi.python.org/pypi/Fiona) --> Reading and writing spatial data (alternative for geopandas)
    - [pyproj](https://pypi.python.org/pypi/pyproj?)  --> Performs cartographic transformations and geodetic computations (based on [PROJ.4](http://trac.osgeo.org/proj))
    - [pysal](https://pysal.readthedocs.org/en/latest/) --> Library of spatial analysis functions written in Python
    - [cartopy](http://scitools.org.uk/cartopy/docs/latest/index.html) --> Make drawing maps for data analysis and visualisation as easy as possible
    - [scipy.spatial](http://docs.scipy.org/doc/scipy/reference/spatial.html) --> Spatial algorithms and data structures
    - [rtree](http://toblerity.org/rtree/) --> Spatial indexing for Python for quick spatial lookups
    - [rasterio](https://github.com/mapbox/rasterio) --> Clean and fast and geospatial raster I/O for Python
    - [RSGISLib](http://www.rsgislib.org/index.html#python-documentation) --> Remote Sensing and GIS Software Library for Python
