# Geometric Objects - Spatial Data Model

**Contents:**

1. [Overview of geometric objects and Shapely -modules](#1-overview-of-geometric-objects-and-shapely--module)
2. [Point](#2-point)
  - [Creating a Point -object](#2-point)
  - [Point attributes and functions](#point-attributes-and-functions)
3. [LineString (i.e. a line)](#3-linestring)
  - [Creating a LineString -object](#3-linestring)
  - [LineString attributes and functions](#linestring-attributes-and-functions)
4. [Polygon](#4-polygon)
  - [Creating a Polygon -object](#4-polygon)
  - [Polygon attributes and functions](#polygon-attributes-and-functions)
5. [Pro -tips](#5-pro--tips-optional)
  - [Geometry collections](#geometry-collections)
  - [Useful Shapely functions](#useful-shapely-functions)

## 1. Overview of geometric objects and Shapely -module  

<img src="http://www.helsinki.fi/science/accessibility/maintenance/Kuvia/SpatialDataModel.PNG">
*Fundamental geometric objects that can be used in Python with <a href="http://toblerity.org/shapely/manual.html"><strong>Shapely</strong></a> module*


The most fundamental geometric objects are **Points**, **Lines** and **Polygons** which are the basic ingredients when working with spatial data in vector format. 
Python has a specific module called **[Shapely](http://toblerity.org/shapely/manual.html#)** that can be used to create and work with *Geometric Objects*. 
There are many useful functionalities that you can do with Shapely such as:

  - Create **Line**(s) or **Polygon**(s) from a _**Collection**_ of **Point** geometries
  - Calculate areas/length/bounds etc. of input geometries
  - Make geometric operations based on the input geometries such as **Union**, **Difference**, **Distance** etc.
  - Make spatial queries between geometries such **Intersects**, **Touches**, **Crosses**, **Within** etc.
  
**Geometric Objects consist of coordinate tuples where:**

  - **Point** -object represents a single point in space. Points can be either two-dimensional (x, y) or three dimensional (x, y, z). 
  - **LineString** -object (i.e. a line) represents a sequence of points joined together to form a line. Hence, a line consist of a list of at least two coordinate tuples 
  - **Polygon** -object represents a filled area that consists of a list of at least three coordinate tuples that forms the outerior ring and a (possible) list of hole polygons. 
  
**It is also possible to have a collection of geometric objects (e.g. Polygons with multiple parts):**
  
  - **MultiPoint** -object represents a collection of points and consists of a list of coordinate-tuples 
  - **MultiLineString** -object represents a collection of lines and consists of a list of line-like sequences 
  - **MultiPolygon** -object represents a collection of polygons that consists of a list of polygon-like sequences that construct from exterior ring and (possible) hole list tuples 

## 2. Point 

- Creating point is easy, you pass x and y coordinates into Point() -object (+ possibly also z -coordinate) :

```python
>>> # Import necessary geometric objects from shapely module
... from shapely.geometry import Point, LineString, Polygon
...
>>> # Create Point geometric object(s) with coordinates
... point1 = Point(2.2, 4.2)
>>> point2 = Point(7.2, -25.1)
>>> point3 = Point(9.26, -2.456)
>>> point3D = Point(9.26, -2.456, 0.57)
...
>>> # Let's see what the variables look like
... print(point1)
>>> print(point3D)
...
>>> # What is the type of the point?
... type(point1)
...
>>> # Outputs:
POINT (2.2 4.2)
POINT Z (9.26 -2.456 0.57)
shapely.geometry.point.Point
```

We can see that the type of the point is shapely's Point which is represented in a specific format that is based on [GEOS](https://trac.osgeo.org/geos/) C++ library that is one of the standard libraries in GIS. It runs under the hood e.g. in [Quantum GIS](http://www.qgis.org/en/site/). 3D-point can be recognized from the capital Z -letter in front of the coordinates. 

### Point attributes and functions 

Point -object has some built-in attributes that can be accessed and also some useful functionalities. One of the most useful ones are the ability to extract the coordinates of a Point and calculate the Euclidian distance between points.

- Extracting the coordinates of a Point can be done in a couple of different ways

```python
>>> # Get the coordinates
... point_coords = point1.coords
...
>>> # What is the type of this?
... type(point_coords)
shapely.coords.CoordinateSequence
```

Ok, we can see that the output is a Shapely CoordinateSequence. Let's see how we can get out the actual coordinates:

```python
>>> # Get x and y coordinates
... xy = point_coords.xy
...
>>> # Get only x coordinates of Point1
... x = point1.x
...
>>> # Whatabout y coordinate?
... y = point1.y
...
>>> # What is inside?
... print(xy)
>>> print(x)
>>> print(y)
(array('d', [2.2]), array('d', [4.2]))
2.2
4.2
```

Okey, so we can see that the our xy variable contains a tuple where x and y are stored inside of a numpy arrays. However, our x and y variables are plain decimal numbers. 

- It is also possible to calculate the distance between points which can be useful in many applications
  - the returned distance is based on the projection of the points (degrees in WGS84, meters in UTM)

```python
>>> # Calculate the distance between point1 and point2
... point_dist = point1.distance(point2)
>>> print("Distance between the points is {0:.2f} decimal degrees".format(point_dist))
Distance between the points is 29.72 decimal degrees
```

## 3. LineString 

- Creating a LineString -object is fairly similar to how Point is created. Now instead using a single coordinate-tuple we can construct the line using either a list of shapely Point -objects or pass coordinate-tuples:

```python
>>> # Create a LineString from our Point objects
... line = LineString([point1, point2, point3])
...
>>> # It is also possible to use coordinate tuples having the same outcome
... line2 = LineString([(2.2, 4.2), (7.2, -25.1), (9.26, -2.456)])
...
>>> # Let's see how our LineString looks like
... print(line)
>>> print(line2)
>>> type(line)
LINESTRING (2.2 4.2, 7.2 -25.1, 9.26 -2.456)
LINESTRING (2.2 4.2, 7.2 -25.1, 9.26 -2.456)
shapely.geometry.linestring.LineString
```

Ok, now we can see that variable line constitutes of multiple coordinate-pairs and the type of the data is shapely LineString.

### LineString attributes and functions  

LineString -object has many useful built-in attributes and functionalities. It is for instance possible to extract the coordinates or the length of a LineString (line), calculate the centroid of the line, create points along the line at specific distance, calculate the closest distance from a line to specified Point and simplify the geometry. See full list of functionalities from [Shapely documentation](http://toblerity.org/shapely/manual.html#). Here, we go through a few of them.

- We can extract the coordinates of a LineString similarly as with Point

```python
>>> # Get x and y coordinates of the line
... lxy = line.xy
>>> print(lxy)
(array('d', [2.2, 7.2, 9.26]), array('d', [4.2, -25.1, -2.456]))
```

Okey, we can see that the coordinates are again stored as a numpy arrays where first array includes all x-coordinates and the second all the y-coordinates respectively. 

- We can extract only x or y coordinates by referring to those arrays as follows

```python
>>> # Extract x coordinates
... line_x = lxy[0]
...
>>> # Extract y coordinates straight from the LineObject by referring to a array at index 1
... line_y = line.xy[1]
...
>>> print(line_x)
>>> print(line_y)
array('d', [2.2, 7.2, 9.26])
array('d', [4.2, -25.1, -2.456])
```

- We can get specific attributes such as lenght of the line and center of the line (centroid) straight from the LineString object itself

```python
>>> # Get the lenght of the line
... l_length = line.length
...
>>> # Get the centroid of the line
... l_centroid = line.centroid
...
>>> print("Length of our line: {0:.2f}".format(l_length))
>>> print("Centroid of our line: ", l_centroid)
...
>>> # What type is the centroid?
... type(l_centroid)
Length of our line: 52.46
Centroid of our line:  POINT (6.229961354035622 -11.89241115757239)
shapely.geometry.point.Point
```

Okey, so these are already fairly useful information for many different GIS tasks, and we didn't even calculate anything yet! These attributes are built-in in every LineString object that is created. Notice that the centroid that is returned is Point -object that has its own functions as was described earlier.

## 4. Polygon  

- Creating a Polygon -object continues the same logic of how Point and LineString were created but Polygon object only accepts coordinate-tuples as input. Polygon needs at least three coordinate-tuples:

```python
>>> # Create a Polygon from the coordinates
... poly = Polygon([(2.2, 4.2), (7.2, -25.1), (9.26, -2.456)])
...
>>> # We can also use our previously created Point objects (same outcome)
... # --> notice that Polygon object requires x,y coordinates as input
... poly2 = Polygon([[p.x, p.y] for p in [point1, point2, point3]])
...
>>> # Let's see how our Polygon looks like
... print(poly)
>>> print(poly2)
>>> type(poly)
POLYGON ((2.2 4.2, 7.2 -25.1, 9.26 -2.456, 2.2 4.2))
POLYGON ((2.2 4.2, 7.2 -25.1, 9.26 -2.456, 2.2 4.2))
shapely.geometry.polygon.Polygon
```

Notice that Polygon has double parentheses around the coordinates. This is because Polygon can also have holes inside of it. As the help of Polygon -object tells, a Polygon can be constructed using exterior coordinates and interior coordinates (optional) where the interior coordinates creates a hole inside the Polygon:

 ```python
 Help on Polygon in module shapely.geometry.polygon object:
 class Polygon(shapely.geometry.base.BaseGeometry)
  |  A two-dimensional figure bounded by a linear ring
  |  
  |  A polygon has a non-zero area. It may have one or more negative-space
  |  "holes" which are also bounded by linear rings. If any rings cross each
  |  other, the feature is invalid and operations on it may fail.
  |  
  |  Attributes
  |  ----------
  |  exterior : LinearRing
  |      The ring which bounds the positive space of the polygon.
  |  interiors : sequence
  |      A sequence of rings which bound all existing holes.
 ```

- Let's create a Polygon with a hole inside

```python
>>> # Let's create a bounding box of the world and make a whole in it
...
... # First we define our exterior
... world_exterior = [(-180, 90), (-180, -90), (180, -90), (180, 90)]
...
>>> # Let's create a single big hole where we leave ten decimal degrees at the boundaries of the world
... # Notice: there could be multiple holes, thus we need to provide a list of holes
... hole = [[(-170, 80), (-170, -80), (170, -80), (170, 80)]]
...
>>> # World without a hole
... world = Polygon(shell=world_exterior)
...
>>> # Now we can construct our Polygon with the hole inside
... world_has_a_hole = Polygon(shell=world_exterior, holes=hole)
...
>>> print(world)
>>> print(world_has_a_hole)
>>> type(world_has_a_hole)
POLYGON ((-180 90, -180 -90, 180 -90, 180 90, -180 90))
POLYGON ((-180 90, -180 -90, 180 -90, 180 90, -180 90), (-170 80, -170 -80, 170 -80, 170 80, -170 80))
shapely.geometry.polygon.Polygon
```

Now we can see that the polygon has two different tuples of coordinates. The first one represents the outerior and the second one represents the hole inside of the Polygon.

### Polygon attributes and functions  

- We can again access different attributes that are really useful such as area, centroid, bounding box, exterior, and exterior-length of the Polygon

```python
>>> # Get the centroid of the Polygon
... world_centroid = world.centroid
...
>>> # Get the area of the Polygon
... world_area = world.area
...
>>> # Get the bounds of the Polygon (i.e. bounding box)
... world_bbox = world.bounds
...
>>> # Get the exterior of the Polygon
... world_ext = world.exterior
...
>>> # Get the length of the exterior
... world_ext_length = world_ext.length
...
>>> print("Poly centroid: ", world_centroid)
>>> print("Poly Area: ", world_area)
>>> print("Poly Bounding Box: ", world_bbox)
>>> print("Poly Exterior: ", world_ext)
>>> print("Poly Exterior Length: ", world_ext_length)
Poly centroid:  POINT (-0 -0)
Poly Area:  64800.0
Poly Bounding Box:  (-180.0, -90.0, 180.0, 90.0)
Poly Exterior:  LINEARRING (-180 90, -180 -90, 180 -90, 180 90, -180 90)
Poly Exterior Length:  1080.0
```

## Next steps ..

Now you know all of the basic geometrical objects that are used when doing GIS using vector data. 

Next, you can **continue with the [Exercise 1]()** or read [Pro -tips materials]() where there is still some extra material concerning geometry collections and some useful functions that can be used when dealing with geometric objects in Python using Shapely -module. 

# 5. Pro -tips (optional)  

This part is not obligatory but it contains some really useful information related to a slightly more complicated GIS-related functions and processes that can be done using Shapely -module. 

## Geometry collections  

## Useful Shapely functions  

- We can also simplify our geometry (applies to line and polygon geometries which can be useful in some occasions using specific ([Douglas-Peucker algorithm](https://en.wikipedia.org/wiki/Ramer%E2%80%93Douglas%E2%80%93Peucker_algorithm))
