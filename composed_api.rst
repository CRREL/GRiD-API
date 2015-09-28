GRiD API
========

API Endpoint Reference
----------------------

Get Point Cloud or Raster Features
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Get a list of point cloud and/or raster features via GRiD's Web Feature
Service (WFS).

Endpoint
^^^^^^^^

.. code:: bash

    GET http://gridte.rsgis.erdc.dren.mil/te_ba/cgi-bin/gridws

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

.. code:: bash

    curl -u <username> "http://gridte.rsgis.erdc.dren.mil/te_ba/cgi-bin/gridws?service=wfs&version=1.1.0&request=getfeature&typename=ms:gridws_pointcloud&bbox=62,33,62.1,33.1"

.. code:: xml

    <?xml version='1.0' encoding="UTF-8" ?>
    <wfs:FeatureCollection
       xmlns:ms="http://mapserver.gis.umn.edu/mapserver"
       xmlns:gml="http://www.opengis.net/gml"
       xmlns:wfs="http://www.opengis.net/wfs"
       xmlns:ogc="http://www.opengis.net/ogc"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://mapserver.gis.umn.edu/mapserver http://gridte-proc.erdc.dren.mil/te_ba/cgi-bin/gridws?SERVICE=WFS&amp;VERSION=1.1.0&amp;REQUEST=DescribeFeatureType&amp;TYPENAME=ms:gridws_pointcloud&amp;OUTPUTFORMAT=text/xml;%20subtype=gml/3.1.1  http://www.opengis.net/wfs http://schemas.opengis.net/wfs/1.1.0/wfs.xsd">
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

Get a User's AOI List
~~~~~~~~~~~~~~~~~~~~~

Get a list of the AOIs created by or shared with the current GRiD user.

Endpoint
^^^^^^^^

.. code:: bash

    GET http://gridte.rsgis.erdc.dren.mil/te_ba/api/v0/aoi

Request Parameters
^^^^^^^^^^^^^^^^^^

+-------------------+----------------------------------------------------------+
| Query parameter   | Value                                                    |
+===================+==========================================================+
| geom              | *Optional*. A WKT geometry used to filter AOI results.   |
+-------------------+----------------------------------------------------------+

Response Format
^^^^^^^^^^^^^^^

On success, the HTTP status code in the header response is ``200`` OK
and the response body contains an array of `AOI object <#aoi-object>`__
in JSON format.

Example
^^^^^^^

.. code:: bash

    curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v0/export/?geom=POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))

.. code:: json

    {
      "self_aoi_list": [
        {
          "name": "myFirstAOI",
          "geometry": "POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))",
          "notes": "",
          "is_active": true,
          "source": "api",
          "num_exports": "3 exports",
          "pk": 1959,
          "created_at": "2015-07-07 23:30:29.088539"
        }, {
          "name": "mySecondAOI",
          "geometry": "POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))",
          "notes": "",
          "is_active": true,
          "source": "map",
          "num_exports": "6 exports",
          "pk": 1855,
          "created_at": "2015-06-23 13:21:50.034012"
        }
      ]
    }

Get AOI Details
~~~~~~~~~~~~~~~

Get information for a single AOI.

Endpoint
^^^^^^^^

.. code:: bash

    GET http://gridte.rsgis.erdc.dren.mil/te_ba/api/v0/aoi/{pk}

Request Parameters
^^^^^^^^^^^^^^^^^^

+------------------+--------------------------------+
| Path parameter   | Value                          |
+==================+================================+
| pk               | The primary key for the AOI.   |
+------------------+--------------------------------+

Response Format
^^^^^^^^^^^^^^^

On success, the HTTP status code in the header response is ``200`` OK
and the response body contains an `AOI Detail
object <#aoi-detail-object>`__ in JSON format.

Example
^^^^^^^

.. code:: bash

    curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v0/aoi/1959

.. code:: json

    {
      "export_set": [
        {
          "status": "SUCCESS",
          "stated_at": "2015-07-07 23:33:24.247148",
          "name": "ExportNumberOne.zip",
          "datatype": "LAS 1.2",
          "hsrs": 32641,
          "url": "http://gridte.rsgis.erdc.dren.mil/te_ba/export/download/3561/",
          "pk": 3561
        }, {
          "status": "SUCCESS",
          "stated_at": "2015-07-07 23:31:32.584232",
          "name": "ExportNumberTwo.zip",
          "datatype": "DSM",
          "hsrs": 32641,
          "url": "http://gridte.rsgis.erdc.dren.mil/te_ba/export/download/3560/",
          "pk": 3560
        }
      ],
      "aoi": [
        {
          "fields": {
            "name": "myFirstAOI",
            "created_at": "2015-07-07T23:30:29.088",
            "is_active": true,
            "source": "api",
            "user": 90,
            "clip_geometry": "POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))",
            "notes": ""
          },
          "model": "export.aoi",
          "pk": 1959
        }
      ],
      "collects": [
        {
          "fields": {
            "name": "CollectA"
          },
          "model": "loaddata.collect",
          "pk": 2298
        }, {
          "fields": {
            "name": "CollectB"
          },
          "model": "loaddata.collect",
          "pk": 3109
        }
      ]
    }

Add AOI
~~~~~~~

Create a new AOI for the given geometry.

Endpoint
^^^^^^^^

.. code:: bash

    GET http://gridte.rsgis.erdc.dren.mil/te_ba/api/v0/aoi/add

Request Parameters
^^^^^^^^^^^^^^^^^^

+-------------------+-------------------------------------------------------+
| Query parameter   | Value                                                 |
+===================+=======================================================+
| name              | *Required*. The name for the AOI.                     |
+-------------------+-------------------------------------------------------+
| geom              | *Required*. A WKT geometry describing the AOI.        |
+-------------------+-------------------------------------------------------+
| subscribe         | *Optional*. True, False, T, F, 1, 0. Default: false   |
+-------------------+-------------------------------------------------------+

Response Format
^^^^^^^^^^^^^^^

On success, the HTTP status code in the header response is ``200`` OK
and the response body contains an `Upload object <#aoi-detail-object>`__
in JSON format.

Example
^^^^^^^

.. code:: bash

    curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v0/aoi/add/?name=test&geom=POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))&subscribe=True

.. code:: json

    {
      "aoi": [
        {
          "geometry": "POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))",
          "pk": 2086,
          "name": "uploadedAOI",
          "subscribed": true
        }
      ],
      "success": true
    }

Get Export Details
~~~~~~~~~~~~~~~~~~

Get information for a single export.

Endpoint
^^^^^^^^

.. code:: bash

    GET http://gridte.rsgis.erdc.dren.mil/te_ba/api/v0/export/{pk}

Request Parameters
^^^^^^^^^^^^^^^^^^

+------------------+-----------------------------------+
| Path parameter   | Value                             |
+==================+===================================+
| pk               | The primary key for the export.   |
+------------------+-----------------------------------+

Response Format
^^^^^^^^^^^^^^^

On success, the HTTP status code in the header response is ``200`` OK
and the response body contains an `Export Detail
object <#export-detail-object>`__ in JSON format.

Example
^^^^^^^

.. code:: bash

    curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v0/export/3124

.. code:: json

    {
      "exportfiles": [
        {
          "url": "http://gridte.rsgis.erdc.dren.mil/te_ba/export/download/file/30359/",
          "pk": 30359,
          "name": "ExportedFile.laz"
        }
      ],
      "tda_set": [
        {
          "status": "SUCCESS",
          "tda_type": "Los",
          "name": "LineOfSightResult",
          "url": "http://gridte.rsgis.erdc.dren.mil/te_ba/tda/download/1069/",
          "created_at": "2015-05-12 18:25:05.082077",
          "pk": 1069,
          "notes": ""
        }, {
          "status": "SUCCESS",
          "tda_type": "Hlz",
          "name": "HelicopterLandingZoneResult",
          "url": "http://gridte.rsgis.erdc.dren.mil/te_ba/tda/download/1068/",
          "created_at": "2015-05-12 18:24:20.701910",
          "pk": 1068,
          "notes": ""
        }
      ]
    }

Lookup Geoname
~~~~~~~~~~~~~~

Get suggested AOI name based on geographic coordinates of the geometry.

Endpoint
^^^^^^^^

.. code:: bash

    GET http://gridte.rsgis.erdc.dren.mil/te_ba/api/v0/geoname

Request Parameters
^^^^^^^^^^^^^^^^^^

+-------------------+--------------------------------------------------+
| Query parameter   | Value                                            |
+===================+==================================================+
| geom              | *Required*. A WKT geometry describing the AOI.   |
+-------------------+--------------------------------------------------+

Response Format
^^^^^^^^^^^^^^^

On success, the HTTP status code in the header response is ``200`` OK
and the response body contains a `Geoname object <#geoname-object>`__ in
JSON format.

Example
^^^^^^^

.. code:: bash

    curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v0/geoname/?geom=POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))

.. code:: json

    {
      "name": "Some Place",
      "provided_geometry": "POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))"
    }

Get Task Details
~~~~~~~~~~~~~~~~

Get task status/details for the provided task\_id.

Endpoint
^^^^^^^^

.. code:: bash

    GET http://gridte.rsgis.erdc.dren.mil/te_ba/api/v0/task/{task_id}

Request Parameters
^^^^^^^^^^^^^^^^^^

+------------------+-----------------------+
| Path parameter   | Value                 |
+==================+=======================+
| task\_id         | The ID of the task.   |
+------------------+-----------------------+

Response Format
^^^^^^^^^^^^^^^

On success, the HTTP status code in the header response is ``200`` OK
and the response body contains an `Task
object <#export-detail-object>`__ in JSON format.

Example
^^^^^^^

.. code:: bash

    curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v0/task/bacb736e-e900-457c-9b24-fd409bc3019d/

.. code:: json

    {
      "task_traceback": "",
      "task_state": "SUCCESS",
      "task_tstamp": "2015-09-09T14:19:36.080",
      "task_name": "export.tasks.generate_export",
      "task_id": "774b4666-5706-4237-8661-df0f96cd7b9c"
    }

Generate Point Cloud Export
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Generate point cloud export for the given AOI primary key and collect
primary keys.

Endpoint
^^^^^^^^

.. code:: bash

    GET http://gridte.rsgis.erdc.dren.mil/te_ba/api/v0/aoi/{pk}/generate/pointcloud

Request Parameters
^^^^^^^^^^^^^^^^^^

+------------------+-------------------------------+
| Path parameter   | Value                         |
+==================+===============================+
| pk               | The primary key of the AOI.   |
+------------------+-------------------------------+

+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| Query parameter         | Value                                                                                                                                     |
+=========================+===========================================================================================================================================+
| collects                | *Required*. A list of collection primary keys to include in the export, separated by ``+`` or ``,``.                                      |
+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| hsrs                    | *Optional*. Accepts an EPSG code. Defaults to AOI SRS.                                                                                    |
+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| intensity               | *Optional*. Whether or not to export intensity. Default: True.                                                                            |
+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| dim\_classification     | *Optional*. Whether or not to export classification. Default: True.                                                                       |
+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| file\_export\_options   | *Optional*. Determine file merging strategy. Accepts ``individual``, ``collect``, and ``super``. Default: ``individual``.                 |
+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| compressed              | *Optional*. Whether or not to export compressed data. Default: True.                                                                      |
+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| send\_email             | *Optional*. Whether or not to notify user via email upon completion. Default: False.                                                      |
+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| generate\_dem           | *Optional*. Whether or not to generate a DEM from the export. Default: False.                                                             |
+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| cell\_spacing           | *Optional*. Used together with ``generate_dem``. Default: 1.0.                                                                            |
+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| pcl\_terrain            | *Optional*. Used to trigger a PMF Bare Earth export. Accepts ``urban``, ``suburban``, ``mountainous``, and ``foliated``. Default: None.   |
+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
| sri\_hres               | *Optional* Used to trigger a Sarnoff Bare Earth export. Accepts the horizontal resolutions. Default: None.                                |
+-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+

Response Format
^^^^^^^^^^^^^^^

On success, the HTTP status code in the header response is ``200`` OK
and the response body contains a `Generate export
object <#generate-export-object>`__ in JSON format.

Example
^^^^^^^

.. code:: bash

    curl -u <username> http://gridte.rsgis.erdc.dren.mil/api/v0/aoi/2389/generate/pointcloud/?collects=100+102&send_email=True&file_export_options=collect

.. code:: json

    {
      "started" : true,
      "task_id" : "774b4666-5706-4237-8661-df0f96cd7b9c"
    }

Generate Raster Export
~~~~~~~~~~~~~~~~~~~~~~

Generate raster export for the given AOI primary key and collect primary
keys.

Endpoint
^^^^^^^^

.. code:: bash

    GET http://gridte.rsgis.erdc.dren.mil/te_ba/api/v1/aoi/{pk}/generate/raster

Request Parameters
^^^^^^^^^^^^^^^^^^

+------------------+-------------------------------+
| Path parameter   | Value                         |
+==================+===============================+
| pk               | The primary key of the AOI.   |
+------------------+-------------------------------+

+-------------------------+-----------------------------------------------------------------------------------------------------------------+
| Query parameter         | Value                                                                                                           |
+=========================+=================================================================================================================+
| collects                | *Required*. A list of collection primary keys to include in the export, separated by ``+`` or ``,``.            |
+-------------------------+-----------------------------------------------------------------------------------------------------------------+
| hsrs                    | *Optional*. Accepts an EPSG code. Defaults to AOI SRS.                                                          |
+-------------------------+-----------------------------------------------------------------------------------------------------------------+
| file\_export\_options   | *Optional*. Determine file merging strategy. Accepts ``individual`` and ``collect``. Default: ``individual``.   |
+-------------------------+-----------------------------------------------------------------------------------------------------------------+
| compressed              | *Optional*. Whether or not to export compressed data. Default: True.                                            |
+-------------------------+-----------------------------------------------------------------------------------------------------------------+
| send\_email             | *Optional*. Whether or not to notify user via email upon completion. Default: False.                            |
+-------------------------+-----------------------------------------------------------------------------------------------------------------+

Response Format
^^^^^^^^^^^^^^^

On success, the HTTP status code in the header response is ``200`` OK
and the response body contains a `Generate export
object <#generate-export-object>`__ in JSON format.

Example
^^^^^^^

.. code:: bash

    curl -u <username> http://gridte.rsgis.erdc.dren.mil/api/v1/aoi/2389/generate/raster/?collects=100+102&send_email=True&file_export_options=collect

.. code:: json

    {
      "started" : true,
      "task_id" : "774b4666-5706-4237-8661-df0f96cd7b9c"
    }

Object Model
------------

AOI object
~~~~~~~~~~

+----------------+--------------+---------------------------------------------------------------+
| Key            | Value Type   | Value Description                                             |
+================+==============+===============================================================+
| name           | string       | The name of the AOI.                                          |
+----------------+--------------+---------------------------------------------------------------+
| geometry       | string       | The WKT geometry of the AOI.                                  |
+----------------+--------------+---------------------------------------------------------------+
| notes          | string       | User notes.                                                   |
+----------------+--------------+---------------------------------------------------------------+
| is\_active     | boolean      | Whether or not the AOI is active.                             |
+----------------+--------------+---------------------------------------------------------------+
| source         | string       | Source of the AOI (e.g., map, api).                           |
+----------------+--------------+---------------------------------------------------------------+
| num\_exports   | string       | The number of exports that have been generated for the AOI.   |
+----------------+--------------+---------------------------------------------------------------+
| pk             | integer      | The primary key of the AOI.                                   |
+----------------+--------------+---------------------------------------------------------------+
| created\_at    | timestamp    | Time of creation for the AOI: ``YYYY-MM-DD HH24:MI:SS.FF6``   |
+----------------+--------------+---------------------------------------------------------------+

AOI object2
~~~~~~~~~~~

+-------------------------+--------------+---------------------------------------+
| Key                     | Value Type   | Value Description                     |
+=========================+==============+=======================================+
| fields.name             | string       | The name of the AOI.                  |
+-------------------------+--------------+---------------------------------------+
| fields.created\_at      | timestamp    | ISO 8601 format as UTC.               |
+-------------------------+--------------+---------------------------------------+
| fields.is\_active       | boolean      | Whether or not the AOI is active.     |
+-------------------------+--------------+---------------------------------------+
| fields.source           | string       | Source of the AOI (e.g., map, api).   |
+-------------------------+--------------+---------------------------------------+
| fields.user             | integer      | The id of the creating user.          |
+-------------------------+--------------+---------------------------------------+
| fields.clip\_geometry   | string       | The WKT geometry of the AOI.          |
+-------------------------+--------------+---------------------------------------+
| fields.notes            | string       | User notes.                           |
+-------------------------+--------------+---------------------------------------+
| model                   | string       | The model (e.g., export.aoi).         |
+-------------------------+--------------+---------------------------------------+
| pk                      | integer      | The primary key of the AOI.           |
+-------------------------+--------------+---------------------------------------+

AOI Detail object
~~~~~~~~~~~~~~~~~

+---------------+--------------------------------------------------+------------------------------+
| Key           | Value Type                                       | Value Description            |
+===============+==================================================+==============================+
| export\_set   | array of `exports objects <#export-object>`__    | The exports of the AOI.      |
+---------------+--------------------------------------------------+------------------------------+
| aoi           | array of `aoi objects <#aoi-object2>`__          | The AOI detail (repeated).   |
+---------------+--------------------------------------------------+------------------------------+
| collects      | array of `collect objects <#collect-object>`__   | The collects for the AOI.    |
+---------------+--------------------------------------------------+------------------------------+

AOI Upload object
~~~~~~~~~~~~~~~~~

+--------------+--------------+-----------------------------------------------------+
| Key          | Value Type   | Value Description                                   |
+==============+==============+=====================================================+
| geometry     | string       | WKT of the uploaded AOI.                            |
+--------------+--------------+-----------------------------------------------------+
| pk           | integer      | The primary key of the uploaded AOI.                |
+--------------+--------------+-----------------------------------------------------+
| name         | string       | The name of the uploaded AOI.                       |
+--------------+--------------+-----------------------------------------------------+
| subscribed   | boolean      | Whether or not the user is subscribed to the AOI.   |
+--------------+--------------+-----------------------------------------------------+

Collect object
~~~~~~~~~~~~~~

+---------------+--------------+---------------------------------------+
| Key           | Value Type   | Value Description                     |
+===============+==============+=======================================+
| fields.name   | string       | The name of the collect.              |
+---------------+--------------+---------------------------------------+
| model         | string       | The model (e.g., loaddata.collect).   |
+---------------+--------------+---------------------------------------+
| pk            | integer      | The primary key of the collect.       |
+---------------+--------------+---------------------------------------+

Export object
~~~~~~~~~~~~~

+--------------+--------------+---------------------------------------------------------------+
| Key          | Value Type   | Value Description                                             |
+==============+==============+===============================================================+
| status       | string       | The status of the export (e.g., SUCCESS, FAILED, QUEUED).     |
+--------------+--------------+---------------------------------------------------------------+
| stated\_at   | timestamp    | Time of creation for the AOI: ``YYYY-MM-DD HH24:MI:SS.FF6``   |
+--------------+--------------+---------------------------------------------------------------+
| name         | string       | The name of the export.                                       |
+--------------+--------------+---------------------------------------------------------------+
| datatype     | string       | The datatype (e.g., LAS 1.2, DTM).                            |
+--------------+--------------+---------------------------------------------------------------+
| hsrs         | integer      | The Horizontal Spatial Reference System EPSG code.            |
+--------------+--------------+---------------------------------------------------------------+
| url          | string       | The download URL of the export.                               |
+--------------+--------------+---------------------------------------------------------------+
| pk           | integer      | The primary key of the export.                                |
+--------------+--------------+---------------------------------------------------------------+

Export Detail object
~~~~~~~~~~~~~~~~~~~~

+---------------+----------------------------------------------------------+---------------------------------------+
| Key           | Value Type                                               | Value Description                     |
+===============+==========================================================+=======================================+
| exportfiles   | array of `Exportfiles objects <#exportfiles-object>`__   | The export files of the export set.   |
+---------------+----------------------------------------------------------+---------------------------------------+
| tda\_set      | array of `TDA Set objects <#tda-set-object>`__           | The TDAs of the export set.           |
+---------------+----------------------------------------------------------+---------------------------------------+

Exportfiles object
~~~~~~~~~~~~~~~~~~

+--------+--------------+----------------------------------------+
| Key    | Value Type   | Value Description                      |
+========+==============+========================================+
| url    | string       | The download URL of the export file.   |
+--------+--------------+----------------------------------------+
| pk     | integer      | The primary key of the export file.    |
+--------+--------------+----------------------------------------+
| name   | string       | The name of the export file.           |
+--------+--------------+----------------------------------------+

Generate Export object
~~~~~~~~~~~~~~~~~~~~~~

+------------+--------------+-----------------------------------------------------------+
| Key        | Value Type   | Value Description                                         |
+============+==============+===========================================================+
| started    | boolean      | Whether or not the point cloud export task has started.   |
+------------+--------------+-----------------------------------------------------------+
| task\_id   | string       | The id of the task.                                       |
+------------+--------------+-----------------------------------------------------------+

Geoname object
~~~~~~~~~~~~~~

+----------------------+--------------+---------------------------------------------+
| Key                  | Value Type   | Value Description                           |
+======================+==============+=============================================+
| name                 | string       | The suggested name.                         |
+----------------------+--------------+---------------------------------------------+
| provided\_geometry   | string       | WKT used to determine the suggested name.   |
+----------------------+--------------+---------------------------------------------+

Task object
~~~~~~~~~~~

+-------------------+--------------+---------------------------------------------------------------+
| Key               | Value Type   | Value Description                                             |
+===================+==============+===============================================================+
| task\_traceback   | string       | TBD                                                           |
+-------------------+--------------+---------------------------------------------------------------+
| task\_state       | string       | The state of the task (e.g., SUCCESS, FAILED, QUEUED).        |
+-------------------+--------------+---------------------------------------------------------------+
| task\_tstamp      | timestamp    | ISO 8601 format as UTC.                                       |
+-------------------+--------------+---------------------------------------------------------------+
| task\_name        | string       | The name of the task (e.g., export.tasks.generate\_export).   |
+-------------------+--------------+---------------------------------------------------------------+
| task\_id          | string       | The id of the task.                                           |
+-------------------+--------------+---------------------------------------------------------------+

TDA Set object
~~~~~~~~~~~~~~

+---------------+--------------+---------------------------------------------------------------+
| Key           | Value Type   | Value Description                                             |
+===============+==============+===============================================================+
| status        | string       | The status of the export (e.g., SUCCESS, FAILED, QUEUED).     |
+---------------+--------------+---------------------------------------------------------------+
| tda\_type     | string       | The TDA type (e.g., Hlz, Los).                                |
+---------------+--------------+---------------------------------------------------------------+
| name          | string       | The name of the TDA.                                          |
+---------------+--------------+---------------------------------------------------------------+
| url           | string       | The download URL of the TDA.                                  |
+---------------+--------------+---------------------------------------------------------------+
| created\_at   | timestamp    | Time of creation for the TDA: ``YYYY-MM-DD HH24:MI:SS.FF6``   |
+---------------+--------------+---------------------------------------------------------------+
| pk            | integer      | The primary key of the TDA.                                   |
+---------------+--------------+---------------------------------------------------------------+
| notes         | string       | User notes.                                                   |
+---------------+--------------+---------------------------------------------------------------+

Upload object
~~~~~~~~~~~~~

+-----------+--------------------------------------------------------+-----------------------------+
| Key       | Value Type                                             | Value Description           |
+===========+========================================================+=============================+
| aoi       | array of `aoi upload objects <#aoi-upload-object>`__   | The uploaded AOI.           |
+-----------+--------------------------------------------------------+-----------------------------+
| success   | boolean                                                | The status of the upload.   |
+-----------+--------------------------------------------------------+-----------------------------+

