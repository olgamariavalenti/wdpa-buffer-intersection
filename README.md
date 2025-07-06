# 🐸 wdpa-intersection
This project examines whether certain locations are situated within 10 km of any globally protected area, utilizing the World Database on Protected Areas (WDPA). This is especially useful for evaluating environmental risks and opportunities related to conservation policies, sustainable development, or impact assessments.

We'll explore spatial relationships between point locations (e.g., power stations or fuel facilities) and protected areas, leveraging Python, GeoPandas, and geospatial data science practices.

## 📖 Introduction to Key Concepts
### 🌍 World Database on Protected Areas (WDPA)
The [WDPA](https://www.protectedplanet.net/en) is a global dataset maintained by UNEP-WCMC that contains information about protected areas worldwide. Protected areas may be marine or terrestrial, and they are tracked with various metadata including designation status, year, and ISO3 country codes. It contains global spatial data on protected areas — parks, reserves, and marine zones — classified into:

Marine areas (e.g., ocean reserves)
Terrestrial areas (e.g., national parks)
Mixed (partially marine)

The MARINE column encodes this:
0 – Terrestrial
1 – Both
2 – Marine

We use three shapefiles because WDPA distributes large volumes of data in three split layers (0, 1, 2) due to file size limits. We combine all three into one GeoDataFrame for analysis.

### 📌 Coordinate Reference Systems (CRS)
A CRS defines how the two-dimensional, projected map in your computer relates to real places on the earth. You cannot calculate distances accurately in degrees (EPSG:4326). To perform buffering (e.g. 10 km radius), you must first project your data into meters using a CRS like EPSG:3857.
* EPSG:4326 is a geographic coordinate system using latitude and longitude.
* EPSG:3857 is a projected system (Web Mercator) using meters, which is ideal for spatial operations like buffering.

### 📚 🐼 pandas vs geopandas
* pandas is used for standard data manipulation.
* geopandas extends pandas with spatial operations, geometry types, and spatial joins.

## ⚙️ Steps

### 1️⃣  Load Point Locations: power_locations
We define a sample dataset of five power-related locations (e.g., hydrogen, electric, LNG) across the Netherlands with lat/lon coordinates.

### 2️⃣ Intersecting with WDPA: Do These Facilities Touch Protected Areas?
To identify which power locations intersect protected zones:

We reproject both power_locations and WDPA to EPSG:3857.
Perform a spatial join using .sjoin(..., predicate='intersects').
Separate intersecting from non-intersecting points.
Visualize using .explore() with color coding:

* 🔴 Red = intersects protected area
* 🟣 Purple = does not intersect

This step gives actionable insight into which energy facilities are located near sensitive conservation zones.
