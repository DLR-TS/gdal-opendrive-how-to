# OpenDRIVE vector driver for GDAL

Currently, this driver is being [reviewed](https://github.com/OSGeo/gdal/pull/9504) in order to be integrated as optional plugin of GDAL. 

## Getting hands on

For now, clone our DLR development branch [`libopendrive`](https://github.com/DLR-TS/gdal/tree/libopendrive):

```bash
git clone https://github.com/DLR-TS/gdal.git --branch libopendrive --single-branch
```

Build the custom Docker image as described in the [XODR driver documentation](https://github.com/DLR-TS/gdal/blob/libopendrive/doc/source/drivers/vector/xodr.rst#convenient-usage-through-docker-image):

```bash
cd gdal/docker/ubuntu-small/
docker build -t gdal/xodr -f DockerfileXODR .
```

Verify availability of the driver. Calling `ogrinfo --formats` should list the `XODR` driver as first item:

```bash
docker run --rm -it gdal/xodr ogrinfo --formats

Supported Formats:
  XODR -vector- (rov): OpenDRIVE - Open Dynamic Road Information for Vehicle Environment
  PCIDSK -raster,vector- (rw+v): PCIDSK Database File       
  PDS4 -raster,vector- (rw+vs): NASA Planetary Data System 4
  ...
```

You can use the new driver functions through the Docker container. For example, use `ogr2ogr` to convert a local `.xodr` file into any other supported OGR output format:

```bash
docker run --rm -v ${PWD}:/home -it gdal/xodr ogr2ogr -f "GPKG" /home/<file>.gpkg /home/<file>.xodr
```

Our goal is to make these functions conveniently usable through the official GDAL distribution in future, also enabling drag-and-drop of XODR into QGIS, for example.