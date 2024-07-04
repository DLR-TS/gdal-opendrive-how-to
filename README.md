# OpenDRIVE vector driver for GDAL

The driver is [scheduled](https://github.com/OSGeo/gdal/pull/9504) to become part of GDAL release 3.10.

## Getting hands on

Pull one of the two Docker images which have the driver already included:

- either Ubuntu-based
  ```bash
   docker pull ghcr.io/osgeo/gdal:ubuntu-full-latest
  ```
- or Alpine-based
  ```bash
  docker pull ghcr.io/osgeo/gdal:alpine-normal-latest
  ```

For example, spawning the Alpine container, verify availability of the driver by calling `ogrinfo --format XODR`:

```bash
docker run --rm -it ghcr.io/osgeo/gdal:alpine-normal-latest ogrinfo --format XODR

Format Details:
  Short Name: XODR
  Long Name: OpenDRIVE - Open Dynamic Road Information for Vehicle Environment
  Supports: Vector
  Supports: Open() - Open existing dataset.
<OpenOptionList>
  ...
</OpenOptionList>
```

You can now use the new driver functions through the Docker container. For example, use `ogr2ogr` to convert a local `.xodr` file into GeoPackage, or into any other supported OGR output format:

```bash
docker run --rm -v ${PWD}:/home -it ghcr.io/osgeo/gdal:alpine-normal-latest ogr2ogr -f "GPKG" /home/<file>.gpkg /home/<file>.xodr
```

## QGIS Demo

Our goal is to make these functions conveniently usable through the official GDAL distribution in future, thus, also enabling drag-and-drop of XODR into QGIS. The following video shows the current workaround through a previously created GeoPackage.

<video width="640" controls>
  <source src="https://github.com/DLR-TS/gdal-opendrive-how-to/assets/6084449/8b653324-e726-43fb-83eb-6400de7d67e7" type="video/mp4">
</video>

## Context references

- Scholz, Michael and Böttcher, Oliver and Bardak, Gülşen (2024): [*Improving interoperability between OpenDRIVE HD map data and GIS using GDAL*](https://talks.osgeo.org/foss4g-europe-2024/talk/SD7SGV/). FOSS4G Europe 2024, Tartu, Estonia.
- Scholz, Michael and Böttcher, Oliver and Bardak, Gülşen (2024): [*Making OpenDRIVE HD map data easily accessible in GIS*](https://elib.dlr.de/197330/). Geospatial World Forum 2024, Rotterdam, Netherlands.        
- Scholz, Michael and Böttcher, Oliver and Bardak, Gülşen (2024): [*Making domain-specific automotive engineering road space data in OpenDRIVE available for GIS*](https://elib.dlr.de/203887/). International Conference on Geoinformation Data, Processing and Applications (GeoDPA), Oldenburg, Germany.
- Scholz, Michael und Böttcher, Oliver und Bardak, Gülşen (2024): [*OpenDRIVE-HD-Karten mittels GDAL ins GIS bringen*](https://elib.dlr.de/198809/). FOSSGIS 2024, Hamburg, Germany. 
- Scholz, Michael and Bardak, Gülşen (2023): [*Providing a libOpenDRIVE-based GDAL driver for conversion of lane-detailed road network datasets commonly used in automotive engineering into GIS tools*](https://elib.dlr.de/194420/). FOSS4G 2023, Prizren, Kosovo. 
- Scholz, Michael and Orozco Idrobo, Ana Maria (2017): [*Supporting the Implementation of Driving Simulator Environments Through Established GIS Approaches by Extending the Geospatial Data Abstraction Library (GDAL) with OpenDRIVE*](https://elib.dlr.de/110123/). In: Proceedings of the Driving Simulator Conference 2017 Europe VR, p. 51-54. Stuttgart, Germany.
