GRiD WFS
========

Get Point Cloud or Raster Features
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Get a list of point cloud and/or raster features via GRiD's Web Feature
Service (WFS).

Endpoint
^^^^^^^^

::

    GET <instance_url>/<instance_root>_ba/cgi-bin/gridws

Request Parameters
^^^^^^^^^^^^^^^^^^

This is not an exhaustive list of parameters for the WFS endpoint, but
represents a common use case - querying for point cloud and/or raster
features by bounding box. Please refer to the WFS specification or any
number of Internet tutorials for more complex use cases.

+-------------------+--------------------------------------------------------------------+
| Query parameter   | Value                                                              |
+===================+====================================================================+
| service           | *Required*. wfs                                                    |
+-------------------+--------------------------------------------------------------------+
| version           | *Required*. 1.1.0                                                  |
+-------------------+--------------------------------------------------------------------+
| request           | *Required*. getfeature                                             |
+-------------------+--------------------------------------------------------------------+
| typename          | *Optional*. ``ms:gridws_pointcloud`` and/or ``ms:gridws_raster``   |
+-------------------+--------------------------------------------------------------------+
| bbox              | *Optional*. minx,miny,maxx,maxy                                    |
+-------------------+--------------------------------------------------------------------+

Response Format
^^^^^^^^^^^^^^^

On success, the HTTP status code in the header response is ``200`` OK
and the response body contains the WFS response in XML format.

Example
^^^^^^^

::

    curl -u <username> "http://gridte.rsgis.erdc.dren.mil/te_ba/cgi-bin/gridws?service=wfs&version=1.1.0&request=getfeature&typename=ms:gridws_pointcloud&bbox=62,33,62.1,33.1"

::

    <?xml version='1.0' encoding="UTF-8" ?>
    <wfs:FeatureCollection
       xmlns:ms="http://mapserver.gis.umn.edu/mapserver"
       xmlns:gml="http://www.opengis.net/gml"
       xmlns:wfs="http://www.opengis.net/wfs"
       xmlns:ogc="http://www.opengis.net/ogc"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://mapserver.gis.umn.edu/mapserver 
       http://gridte-proc.erdc.dren.mil/te_ba/cgi-bin/gridws?SERVICE=WFS&amp;VERSION=1.1.0&amp;REQUEST=DescribeFeatureType&amp;TYPENAME=ms:gridws_pointcloud&amp;OUTPUTFORMAT=text/xml;%20subtype=gml/3.1.1  
       http://www.opengis.net/wfs http://schemas.opengis.net/wfs/1.1.0/wfs.xsd">
          <gml:boundedBy>
            <gml:Envelope srsName="EPSG:4326">
                    <gml:lowerCorner>33.001454 62.094691</gml:lowerCorner>
                    <gml:upperCorner>33.006002 62.100088</gml:upperCorner>
            </gml:Envelope>
          </gml:boundedBy>
        <gml:featureMember>
          <ms:gridws_pointcloud gml:id="gridws_pointcloud.149319">
            <gml:boundedBy>
                    <gml:Envelope srsName="EPSG:4326">
                            <gml:lowerCorner>33.001454 62.094691</gml:lowerCorner>
                            <gml:upperCorner>33.006002 62.100088</gml:upperCorner>
                    </gml:Envelope>
            </gml:boundedBy>
            <ms:msGeometry>
              <gml:Polygon srsName="EPSG:4326">
                <gml:exterior>
                  <gml:LinearRing>
                    <gml:posList srsDimension="2">33.001454 62.094691 33.006002 62.094691 33.006002 62.100088 33.001454 62.100088 33.001454 62.094691 </gml:posList>
                  </gml:LinearRing>
                </gml:exterior>
              </gml:Polygon>
            </ms:msGeometry>
            <ms:COLLECT_ID>652</ms:COLLECT_ID>
            <ms:COLLECTION>collectName</ms:COLLECTION>
            <ms:FILE_NAME>filename.ntf</ms:FILE_NAME>
            <ms:DATE_LOADED>2012-09-01T00:00:00Z</ms:DATE_LOADED>
            <ms:PC_ID>149319</ms:PC_ID>
            <ms:X>62.0973893743891</ms:X>
            <ms:Y>33.0037279493031</ms:Y>
            <ms:FILE_SIZE_MB>25.8</ms:FILE_SIZE_MB>
            <ms:COLLECTDATE>2011-10-19T00:00:00Z</ms:COLLECTDATE>
            <ms:DOWNLOAD_URL>http://gridte.rsgis.erdc.dren.mil//te_ba/export/pointcloud/149319/laz/</ms:DOWNLOAD_URL>
            <ms:SENSOR_NAME>BuckEye</ms:SENSOR_NAME>
          </ms:gridws_pointcloud>
        </gml:featureMember>
    </wfs:FeatureCollection>
