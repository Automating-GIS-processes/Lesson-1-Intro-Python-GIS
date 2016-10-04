---
anaconda-cloud: {}
---

# Geometric Objects - Spatial Data Model

<img src="http://www.helsinki.fi/science/accessibility/maintenance/Kuvia/SpatialDataModel.PNG">
*Fundamental geometric objects that can be used in Python with __<a href="http://toblerity.org/shapely/manual.html">Shapely</a> __ module*


The most fundamental geometric objects are __Points__, __Lines__ and __Polygons__ which are the basic ingredients when working with spatial data in vector format. Python has a specific module called **Shapely** that can be used to create and work with *Geometric Objects*. There are many useful functionalities that you can do with Shapely such as:

  - Create __Line__(s) or __Polygon__(s) from a __*Collection*__ of __Point__ geometries
  - Calculate areas/length/bounds etc. of input geometries
  - Make geometric operations based on the input geometries such as __Union__, __Difference__, __Distance__ etc.
  - Make spatial queries between geometries such __Intersects__, __Touches__, __Crosses__, __Within__ etc.
  
__Geometric Objects consist of coordinate tuples where:__

  - *__Point__* object consists of a single coordinate-tuple ( examplePoint = Point(x-coord, y-coord) )
  - *__LineString__* object (i.e. a line) consists of a list of at least two coordinate tuples ( exampleLine = LineString([(x1, y1), (x2, y2)]) )
  - *__Polygon__* object consists of a list of at least three coordinate tuples that forms the outerior ring ( examplePoly = Polygon([(x1, y1), (x2, y2), (x3,y3)]) ) and a (possible) list of hole polygons. 
  
__It is also possible to have collections of geometric objects (e.g. Polygons with multiple parts):__
  
  - *__MultiPoint__* object consists of a list of coordinate-tuples ( examplePoints = MultiPoint([(-2.2, 24.5), (12.9, -43.7)]) )
  - *__MultiLineString__* object consists of a list of line-like sequences ( exampleLines = MultiLineString([((0, 0), (1, 1)), ((-1, 0), (1, 0))]) )
  - *__MultiPolygon__* object consists of a list of polygon-like sequences that construct from exterior ring and (possible) hole list tuples ( [((a1, ..., aM), [(b1, ..., bN), ...]), ...] )