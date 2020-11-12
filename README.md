# gis-apps

Coding session on intro to web architure of GIS apps.

## Objectives

1. Explain the basics software architecture of web-based GIS applications and how do they compare with more generic web-based applications.
2. Describe how the Server-Client model is use in web-based GIS applications and common toolschains.
3. Implement a basic client to consume Geo-Web services (MWS, WMTS, and WFS) using Jupyter notebooks.
4. Do some geeky things while playing Python.


## Tool Chain

### Server Side

* [Geoserver](http://geoserver.org/): a server used for geospatial data. Java based.
* [PostgreSQL](https://www.postgresql.org/) + [PostGIS](https://postgis.net/): A relational database with goespatial capabilites.


### Client Side

* Python
* Jupyter Notebooks via [Anaconda](https://www.anaconda.com/), and the following packages:
    * **ipywidgets**, enables widgets in jupyter notebook for dynamic content
    * **ipyleaflet**, enables the display of maps on jupyter notebooks based on the JavaScript library [leaflet](https://leafletjs.com/)



