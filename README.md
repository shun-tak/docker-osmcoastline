# Docker for OSMCoastline

[OSMCoastline](https://github.com/osmcode/osmcoastline) docker images derived from [geographica/gdal2](https://github.com/GeographicaGS/Docker-GDAL2). geographica/gdal2 is derived from an Ubuntu 16.04 Xenial Xerus base image.

## Usage

Build an image.

```
docker build ./2.1.4 -t osmcoastline
```

Run OSMCoastline tools.

```
docker run --rm -v /data:/root/workspace osmcoastline /bin/bash -c 'osmcoastline_filter -o workspace/coastline.osm.pbf workspace/planet.osm.pbf'
docker run --rm -v /data:/root/workspace osmcoastline /bin/bash -c 'osmcoastline -c -b --max-points=1000 -o workspace/coastline.db workspace/coastline.osm.pbf'
```
