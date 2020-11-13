# Geo Web Apps

A coding session about an intro to web architecture of web apps for geographic data: this session demonstrates the steps to deploy geo-web services and how to connect clients to the services. 


## Objectives

1. Explain the basics software architecture of web-based GIS applications and how do they compare with more generic web-based applications.
2. Describe how the Server-Client model is used in web-based GIS applications and common toolchains.
3. Implement a simple client to consume Geo-Web services (MWS, WMTS, and WFS) using Jupyter notebooks.
4. Do some geeky things with Python and geodata.


## Client-Server Model

Like many web-apps, geo-web apps follow the client-server model. The *server* exposes data services and the client *connects* to such services and provides an GUI inteface for the users. 
Geo Web-map servers implement standads for exposing services. Each service provides certain capabilities that the client can request. The most popular are the following:

* Web Map Service (WMS): for publishing maps as images.
* Web Feature Service (WFS): for publishing maps and attributes of geospatial data. It also provides capabilities to capture user's inputs to create or update data stored by the server.
* Web Map Tile Service (WMTS): for publishing maps or data layers using tiles for more eficient data transfer.

The figure below shows a general sofware architecture of a geo-web app using GeoServer on the server side and a Jupyter Notebooks on the client side. These two component interact via an API exposing WMS, WFS or WMTS.

![geo-web app architecture](http://url/to/img.png)




## Toolchain

### Server Side

* [Geoserver](http://geoserver.org/): a server used for geospatial data. Java based.
* [PostgreSQL](https://www.postgresql.org/) + [PostGIS](https://postgis.net/): A relational database with goespatial capabilites.


### Client Side

* Python
* Jupyter Notebooks via [Anaconda](https://www.anaconda.com/), and the following packages:
    * **ipywidgets**, enables widgets in jupyter notebook for dynamic content
    * **ipyleaflet**, enables the display of maps on jupyter notebooks using [LeafLet](https://leafletjs.com/). Leaflet is a  JavaScript library for interactive maps.


## Some Guidelines

* Linux Server, to deploy a geo-web server we need a dedicate machine for this task; for example a remote server in a cloud-based platform running Ubuntu Server 18.04. *Note that people often use the term 'server' to refer to hardware or software, or the combination of hardware and software.*
* Communication with a remote server is done using SSH(Secured Shell). On Linux this is done directly from a *Terminal*, on Windows, we need an SSH client, for example [Bitvise](https://www.bitvise.com/ssh-client). 

### Installing GeoServer

1. Download Geoserver; mind about the version.

```shell
$ wget https://sourceforge.net/projects/geoserver/files/GeoServer/2.18.0/geoserver-2.18.0-bin.zip
```

2.  If needed, install `unzip`, and unzip the file the preferred location. Geoserver recommends to use `/usr/share/geoserver`

```shell
$ sudo apt unzip
$ sudo unzip geoserver-2.18.0-bin.zip -d /usr/share/geoserver
```

3. Add the location of GeoServer as an environment variable.

```shell
$ echo "export GEOSERVER_HOME=/usr/share/geoserver" >> ~/.profile
. ~/.profile
```
4. Make your user the owner of the `geoserver` directory. 

```shell
$ sudo chown -R <USER_NAME> /usr/share/geoserver/
```

5. Start GeoServer. Go to `geserver/bin` and execute the `startup.sh`

```shell
$ cd /usr/share/geoserver/bin
$ sh startup.sh
```

6.  In the browser go to `http://localhost:8080/geoserver`


More on how to install and use Geoserver at https://docs.geoserver.org/latest/en/user/installation/linux.html

### Installing PostreSQL and PostGIS

1. Install **PostreSQL**. Installing and manipulating PostgreSQL required a list of laborious steps, that are well documented around the Internet. For details check this [blog-post](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-18-04)

2. Installing **PostGIS**. PostGIS is an extension on top of PostgreSQL which enable handling geospatial data inside ProgreSQL. Again, there's a ton of documentation on several ways to do this, [here's a way](https://computingforgeeks.com/how-to-install-postgis-on-ubuntu-debian/). Something important to remember is that even when you have installed PostGIS, you have to enable this extension when creating a database explicitly. 


### Jupyter

We will use jupyter as a friendly environment to build a GIS web-client that will retrieve data from Geoserver. In a real-world situation, you will use web frameworks such as DJango, Flask, ReAct, etc. to build a web client.

1. On the *Anaconda prompt* install the `ipywidgets` and `ipyleaflet` packages to the *base* environment. 

```shell
$ conda install -c conda-forge ipyleaflet ipyleaflet
```

`-c`:= channel

2. Start **Jupyter Notbook**, create a new notebook and run the code below to verify that the packages can be loaded into the notebook.

```python
from ipyleaflet import Map, Marker

center = (51.999285, 4.373791)

m = Map(center=center, zoom=14)

marker = Marker(location=center, draggable=True)
m.add_layer(marker)
display(m)
```
You should see a map appearing before your eyes, if it doesn't, look for help in [StackOverflow](https://stackoverflow.com/questions)


### FAQ

* [I'm lost. How do I find my lat and lon?](https://www.latlong.net/)
* [What's that thing called 'zoom level'?](https://leafletjs.com/examples/zoom-levels/)
* [What other cool stuff can I add to my GIS client?](https://blog.jupyter.org/interactive-gis-in-jupyter-with-ipyleaflet-52f9657fa7a)
* [I am hardcore. Where do I find the official documentation of ipyleaflet?](https://ipyleaflet.readthedocs.io/en/latest/)

