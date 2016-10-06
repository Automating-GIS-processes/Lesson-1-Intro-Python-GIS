# Introduction to Python GIS

## General overview of the latter part of the course

Now as we know the basics we are ready to advance and apply those skills to different GIS related tasks. During the next seven weeks we will learn how to deal with
spatial data and analyze it using "pure" Python.
 
At the end of the course you should be able to:

 - Read / write spatial data from/to different file formats
 - Deal with different projections
 - Do different geometric operations and geocoding
 - Do spatial queries
 - Do simple spatial analyses
 - Visualize data and create (interactive) maps, such as (click to open in interactive mode):
 
<a href="http://www.helsinki.fi/science/accessibility/opetus/autogis/texas_unemployment.html" target="_blank"><img src="https://github.com/Automating-GIS-processes/Lesson-1-Intro-Python-GIS/blob/master/img/Texas_map.PNG" width="400"/></a>
 
## What sort of tools are available for doing GIS in pure Python?

Python is extremely useful language to learn in terms of GIS since most of the different GIS Software packages (such
as ArcGIS, QGIS, PostGIS etc.) provide an interface to do analysis using Python scripting. During this course, we will mostly focus on doing GIS without any third
party softwares such as ArcGIS. _**Why?**_ There are several reasons for doing GIS using only Python without any additional software such as:
  
  - Everything is free: you don't need to buy and expensive license for ArcGIS (for example) 
  - You will **learn and understand** much more deeply how different geoprocessing operations work
  - Supports open source softwares/codes and open science by making it possible for everyone to reproduce your work, free-of-charge.
  - Plug-in and chain all sorts of third-party softwares to build e.g. a fancy web-GIS applications as you want (using e.g. [GeoDjango](https://docs.djangoproject.com/en/1.8/ref/contrib/gis/) with [PostGIS](http://postgis.net/) as a back-end)

Thus, when doing data analysis or GIS with Python there are various modules that can help you get going:

- **Data analysis & visualization:**
    - [numpy](http://www.numpy.org/) --> Fundamental package for scientific computing with Python
    - [pandas](http://pandas.pydata.org/) --> High-performance, easy-to-use data structures and data analysis tools
    - [scipy](http://www.scipy.org/about.html) --> A collection of numerical algorithms and domain-specific toolboxes, including signal processing, optimization and statistics
    - [matplotlib](http://matplotlib.org/) --> Basic plotting library for Python 
    - [bokeh](http://bokeh.pydata.org/en/latest/) --> Interactive visualizations (also maps) for the web
    
- **GIS:**
    - [gdal](http://www.gdal.org/) --> Fundamental package for processing vector and raster data formats (many modules below depend on this). Used for raster processing.
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




