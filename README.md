# Docker for OSMCoastline

[OSMCoastline](https://github.com/osmcode/osmcoastline) docker images derived from [geographica/gdal2](https://github.com/GeographicaGS/Docker-GDAL2), that is from Ubuntu 16.04 Xenial Xerus base image.

- [Docker Hub repository](https://hub.docker.com/r/shuntak/osmcoastline/)

## Usage

Pull an image.

```
docker pull shuntak/osmcoastline
# or you can build by yourself
docker build ./2.1.4 -t shuntak/osmcoastline:2.1.4
```

Run OSMCoastline tools.

```
docker run --rm -v /data:/root/workspace shuntak/osmcoastline /bin/bash -c 'osmcoastline_filter -o workspace/coastline.osm.pbf workspace/planet.osm.pbf'
docker run --rm -v /data:/root/workspace shuntak/osmcoastline /bin/bash -c 'osmcoastline -c -b --max-points=1000 -o workspace/coastline.db workspace/coastline.osm.pbf'
```
