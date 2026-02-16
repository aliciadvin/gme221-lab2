# GmE 221 – Laboratory Exercise 2 

## Overview 
This laboratory performs a parcel–landuse overlay analysis using Python (GeoPandas). 
Spatial data are retrieved from PostGIS using minimal SQL. 
Overlay, area computation, percentage calculation, and classification are executed in Python. 
The final output is exported as a GeoJSON file for visualization in QGIS. 

--- 

## Environment Setup 
- Python 3.x 
- PostgreSQL with PostGIS 
- GeoPandas, SQLAlchemy, psycopg2 

--- 

## How to Run 
1. Activate the virtual environment 
2. Run `analysis.py` to execute the overlay and classification 
3. Load the generated GeoJSON file in QGIS 

--- 

## Outputs 
- GeoJSON file: `output/dominant_residential.geojson`
- Visualization in QGIS

## Reflection
Interpreting GIS IO in Practice

In PostGIS, geometry is stored as a spatial data type within a database. It is saved in a format that allows indexing and SQL-based queries suitable for storage and retrieval. In GeoPandas, geometry is represented as Shapely objects inside a GeoDataFrame in Python. This allows spatial operations such as area calculation and overlays to be performed. Overall, PostGIS is for storing and efficiently querying spatial data, while GeoPandas is for manipulating and analyzing spatial data.

This step is considered Input (IO) rather than analysis because we did not perform any spatial computation or algorithm. The SQL query used (e.g. SELECT parcel_pin, geom FROM public.parcel) merely retrieved existing geometry and attributes from the database. We also only converted the storage format (database geometry) into a computational format (GeoDataFrame with Shapely objects). Thus, this was data retrieval, not spatial analysis.

At this point in the laboratory exercise, we are still in the Input phase because we only retrieved data from the database and translated it into a computational structure. The purpose of this is to prepare the spatial data so that algorithms can operate on them in the next phase—Process.

Spatial Process and Classification

insert reflection here

Questions:
- Why is CRS transformation necessary before area computation?
- How does CRS choice affect area accuracy?
- Does the overlay create new spatial units that did not previously exist?
- Why is classification considered part of the analysis process?
- Is classification sensitive to sliver geometries or topology errors?
- Would changing the dominance threshold alter spatial patterns?

QGIS Spatial Classification Interpretation

insert reflection here

Challenge Analysis Reflection

insert reflection here

- What spatial question did you choose?
- What algorithmic steps did you design?
- How does your logic differ from the guided example?