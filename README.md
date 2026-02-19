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
**Interpreting GIS IO in Practice**

In PostGIS, geometry is stored as a spatial data type within a database. It is saved in a format that allows indexing and SQL-based queries suitable for storage and retrieval. In GeoPandas, geometry is represented as Shapely objects inside a GeoDataFrame in Python. This allows spatial operations such as area calculation and overlays to be performed. Overall, PostGIS is for storing and efficiently querying spatial data, while GeoPandas is for manipulating and analyzing spatial data.

This step is considered Input (IO) rather than analysis because we did not perform any spatial computation or algorithm. The SQL query used (e.g. SELECT parcel_pin, geom FROM public.parcel) merely retrieved existing geometry and attributes from the database. We also only converted the storage format (database geometry) into a computational format (GeoDataFrame with Shapely objects). Thus, this was data retrieval, not spatial analysis.

At this point in the laboratory exercise, we are still in the Input phase because we only retrieved data from the database and translated it into a computational structure. The purpose of this is to prepare the spatial data so that algorithms can operate on them in the next phase—Process.

**Spatial Process and Classification**

CRS transformation is necessary before area computation because it ensures the geometry is in a measurement-appropriate coordinate system before calculations. Take EPSG: 4326 for example, this is a geographic coordinate system where coordinates are stored in degrees. But degrees are not uniform units of distance, so area calculations in square degrees are not reliable. That's why we had to convert our data to EPSG:3395, a projected coordinate system where area is computed in square meters.

Building on this, CRS choice directly affects area accuracy because different projected coordinate systems preserve different properties, such as shape, distance, or area. Since our analysis depends on accurate area measurements, it is important to select a CRS that minimizes area distortion since it directly influences our numerical results and final classification.

Once the geometries are in the correct CRS and areas are computed properly, the next step is the overlay operation. The overlay created new spatial units that did not previously exist. Before the overlay, each parcel was represented as a single feature with its attributes. After overlay, one parcel could become multiple fragments. These fragments did not exist before and are newly constructed created by the intersection algorithm.

Then, we proceeded to classification. Classification is part of the analysis (Process) stage because it applies rule-based decision logic to computed values. Unlike before, we are no longer retrieving or formatting data. Instead, we are assigning categories based on calculated results. Therefore, classification belongs to the Process stage rather than Input or Output.

However, it is also important to note that classification is sensitive to sliver geometries or topology errors. Overlay can introduce very small sliver polygons or slight overlaps. Even small geometric errors can change which land use is largest and thus alter final classification.

Essentially, because classification depends on defined rules, changing the dominance threshold would significantly alter spatial patterns. Changing the threshold could mean more or less parcels would qualify depending on the threshold set. Changing it alters the spatial distribution of “dominant residential” parcels.

**QGIS Spatial Classification Interpretation**

When our output was exported as GeoJSON, the data changed from something stored inside Python into a format that other GIS programs can read. In QGIS, we were able to visualize dominant_residential.geojson where the results of the analysis became more concrete. What began as Input (retrieving parcels and land use data from PostGIS) and moved through Process (area computation, overlay, classification) ultimately materialized as Output which is a map of parcels classified as dominant residential.

Upon closer inspection, the output revealed small sliver geometries along some parcel boundaries. These likely resulted from minor topology inconsistencies in the land use or parcel data. This shows that map output depend not only on the rules we apply, but also on how clean and accurate the original data is.

Overall, the exercise demonstrates how structured computational steps transform spatial data into geographic patterns we can visualize and interpret.

**Challenge Analysis Reflection**

For my challenge analysis, I chose Option 1 — Dominant Non-Residential Parcels, which asks: Which parcels are dominantly non-residential, with at least 50% of their area occupied by that land use?

Following the Input–Process–Output structure, I mainly followed the workflow from the laboratory exercise: retrieving data from the database, reprojecting the CRS, calculating parcel areas, performing the overlay, and applying classification. The main difference in my approach was the classification step. Instead of identifying parcels with dominant residential land use, I edited the script to focus on non-residential parcels. I used logical operators, != and &, to exclude residential zones and ensure only parcels with at least 50% non-residential coverage were selected I then reprojected the results back to EPSG:4326 and exported them as a GeoJSON file.

Compared to the guided example, which used a 60% threshold to find dominant residential parcels, the challenge I selected shifted the spatial question to non-residential dominance and adjusted the threshold to 50%, resulting in a different spatial pattern and interpretation.