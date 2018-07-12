# Docker for OSMCoastline

[OSMCoastline](https://github.com/osmcode/osmcoastline) docker images derived from [geographica/gdal2](https://github.com/GeographicaGS/Docker-GDAL2), that is from Ubuntu 16.04 Xenial Xerus base image.

[GDAL](http://www.gdal.org/) and [Libosmium](https://github.com/osmcode/libosmium) are also available.

- [Docker Hub repository](https://hub.docker.com/r/shuntak/osmcoastline/)

## Usage

Pull an image.

```
docker pull shuntak/osmcoastline
```

You can build an image by yourself.

```
git clone https://github.com/shun-tak/docker-osmcoastline.git
docker build ./docker-osmcoastline/2.1.4 -t shuntak/osmcoastline:2.1.4
```

Run OSMCoastline tools.

Assuming that `/data` is your local working directory.

```
docker run --rm -v /data:/root/workspace shuntak/osmcoastline /bin/bash -c 'osmcoastline_filter -o workspace/coastline.osm.pbf workspace/planet.osm.pbf'
docker run --rm -v /data:/root/workspace shuntak/osmcoastline /bin/bash -c 'osmcoastline -c -b --max-points=1000 -o workspace/coastline.db workspace/coastline.osm.pbf'
```

Run GDAL utility programs.

```
docker run --rm shuntak/osmcoastline /bin/bash -c 'ogrinfo --version'
```
