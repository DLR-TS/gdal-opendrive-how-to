# OpenDRIVE vector driver for GDAL

The driver is [not yet](https://github.com/OSGeo/gdal/pull/9504) part of the official GDAL distribution. For now, clone our DLR development branch [`libopendrive`](https://github.com/DLR-TS/gdal/tree/libopendrive):

```bash
git clone https://github.com/DLR-TS/gdal.git --branch libopendrive --single-branch
```

Use the new driver functions conveniently through our [custom Docker image](https://github.com/DLR-TS/gdal/blob/libopendrive/doc/source/drivers/vector/xodr.rst#convenient-usage-through-docker-image):

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