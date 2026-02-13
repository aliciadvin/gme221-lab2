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

Questions:
- What is the difference between storing geometry in PostGIS and representing it in GeoPandas?
- Why is this step considered Input (IO) rather than analysis?
- How does this relate to the “Input / Process / Output” structure of GIS algorithms discussed in Lecture 3?