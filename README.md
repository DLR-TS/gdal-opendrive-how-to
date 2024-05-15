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

## QGIS Demo

<video width="640" controls>
  <source src="https://github.com/DLR-TS/gdal-opendrive-how-to/assets/6084449/8b653324-e726-43fb-83eb-6400de7d67e7" type="video/mp4">
</video>

## References

- Scholz, Michael and Böttcher, Oliver and Bardak, Gülşen (2024): [*Making domain-specific automotive engineering road space data in OpenDRIVE available for GIS*](https://elib.dlr.de/203887/). International Conference on Geoinformation Data, Processing and Applications (GeoDPA), Oldenburg, Germany.
- Scholz, Michael und Böttcher, Oliver und Bardak, Gülşen (2024): [*OpenDRIVE-HD-Karten mittels GDAL ins GIS bringen*](https://elib.dlr.de/198809/). FOSSGIS 2024, Hamburg, Germany. 
- Scholz, Michael and Bardak, Gülşen (2023): [*Providing a libOpenDRIVE-based GDAL driver for conversion of lane-detailed road network datasets commonly used in automotive engineering into GIS tools*](https://elib.dlr.de/194420/). FOSS4G 2023, Prizren, Kosovo. 
- Scholz, Michael and Orozco Idrobo, Ana Maria (2017): [*Supporting the Implementation of Driving Simulator Environments Through Established GIS Approaches by Extending the Geospatial Data Abstraction Library (GDAL) with OpenDRIVE*](https://elib.dlr.de/110123/). In: Proceedings of the Driving Simulator Conference 2017 Europe VR, p. 51-54. Stuttgart, Germany.
