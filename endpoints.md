GRiD API v1
========

API Endpoint Reference
----------------------

### Get Point Cloud or Raster Features

Get a list of point cloud and/or raster features via GRiD's Web Feature
Service (WFS).

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/cgi-bin/gridws
~~~~

#### Request Parameters

This is not an exhaustive list of parameters for the WFS endpoint, but
represents a common use case - querying for point cloud and/or raster
features by bounding box. Please refer to the WFS specification or any
number of Internet tutorials for more complex use cases.

  Query parameter   Value
  ----------------- --------------------------------------------------------------
  service           *Required*. wfs
  version           *Required*. 1.1.0
  request           *Required*. getfeature
  typename          *Optional*. `ms:gridws_pointcloud` and/or `ms:gridws_raster`
  bbox              *Optional*. minx,miny,maxx,maxy

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains the WFS response in XML format.

#### Example

~~~~ {.bash}
curl -u <username> "http://gridte.rsgis.erdc.dren.mil/te_ba/cgi-bin/gridws?service=wfs&version=1.1.0&request=getfeature&typename=ms:gridws_pointcloud&bbox=62,33,62.1,33.1"
~~~~

~~~~ {.xml}
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
~~~~

### Get a User's AOI List

Get a list of the AOIs created by or shared with the current GRiD user.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v1/aoi
~~~~

#### Request Parameters

  Query parameter   Value
  ----------------- --------------------------------------------------------
  source            *Required*. Your GRiD generated API key.
  geom              *Optional*. A WKT geometry used to filter AOI results.

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains an array of [AOI object](#aoi-object) in JSON
format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v1/aoi/?geom=POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))&?source=grid
~~~~

~~~~ {.json}
{
    "123": {
        "aoi": [
            {
                "fields": {
                    "clip_geometry": "SRID=4326;POLYGON ((68.9150709532930961 33.5950250284996983, 68.8704389952918063 33.5955969812235011, 68.8724989318148033 33.5858732691386024, 68.9020246886466055 33.5853012519442018, 68.9068312072003977 33.5549789148388982, 68.9274305724316037 33.5589843621810999, 68.9274305724316037 33.5944530719840984, 68.9150709532930961 33.5950250284996983))", 
                    "created_at": "2013-04-16T13:10:33.974", 
                    "is_active": true, 
                    "name": "First_Aoi", 
                    "notes": "", 
                    "source": "", 
                    "user": 102
                }, 
                "model": "export.aoi", 
                "pk": 123
            }
        ], 
    }, 
    "1304": {
        "aoi": [
            {
                "fields": {
                    "clip_geometry": "SRID=4326;POLYGON ((64.2115925480768936 36.8743567152622020, 59.2018269230769008 32.7632670467287994, 68.6940144230768936 32.9847159272803978, 64.2115925480768936 36.8743567152622020))", 
                    "created_at": "2015-09-23T09:50:19.856", 
                    "is_active": true, 
                    "name": "Second_Aoi", 
                    "notes": "", 
                    "source": "", 
                    "user": 102
                }, 
                "model": "export.aoi", 
                "pk": 1304
            }
        ], 
    }, 
    "GRiD API": {
        "API Version": "v1"
    }
}
~~~~

### Get AOI Details

Get information for a single AOI.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v1/aoi/{pk}
~~~~

#### Request Parameters

  Path parameter   Value
  ---------------- ------------------------------
  pk                *Required*. The primary key for the AOI.
  
  Query parameter   Value
  ----------------- ------------------------------------------------
  source            *Required*. Your GRiD generated API key.

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains an [AOI Detail object](#aoi-detail-object) in
JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v1/aoi/123?source=grid
~~~~

~~~~ {.json}
{
    "GRiD API": {
        "API Version": "v1"
    }, 
    "aoi": [
        {
            "fields": {
                "clip_geometry": "SRID=4326;POLYGON ((68.9150709532930961 33.5950250284996983, 68.8704389952918063 33.5955969812235011, 68.8724989318148033 33.5858732691386024, 68.9020246886466055 33.5853012519442018, 68.9068312072003977 33.5549789148388982, 68.9274305724316037 33.5589843621810999, 68.9274305724316037 33.5944530719840984, 68.9150709532930961 33.5950250284996983))", 
                "created_at": "2013-04-16T13:10:33.974", 
                "is_active": true, 
                "name": "First_Aoi", 
                "notes": "", 
                "source": "", 
                "user": 102
            }, 
            "model": "export.aoi", 
            "pk": 123
        }
    ], 
    "export_set": [
        {
            "datatype": "LAS 1.2", 
            "hsrs": "32642", 
            "name": "First_Aoi-UTMzone42N_2015-Oct-15.zip", 
            "pk": 1335, 
            "started_at": "2015-10-15T18:06:13.272161", 
            "status": "SUCCESS", 
            "url": "http://127.0.0.1:8000/export/download/1335/"
        }, 
        {
            "datatype": "DSM", 
            "hsrs": "32642", 
            "name": "First_Aoi_WGS84-UTMzone42N_2015-Oct-15.zip", 
            "pk": 1328, 
            "started_at": "2015-10-15T17:59:05.937854", 
            "status": "SUCCESS", 
            "url": "http://127.0.0.1:8000/export/download/1328/"
        }, 
    ], 
    "pointcloud_collects": [
        {
            "datatype": "LAS 1.2", 
            "name": "20110323_00_0_UFO", 
            "pk": 168
        }
    ], 
    "raster_collects": [
        {
            "datatype": "DSM", 
            "name": "20080407_00_0_UFO", 
            "pk": 228
        }
    ]
}
~~~~

### Add AOI

Create a new AOI for the given geometry.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v1/aoi/add
~~~~

#### Request Parameters

  Query parameter   Value
  ----------------- -----------------------------------------------------
  name              *Required*. The name for the AOI.
  geom              *Required*. A WKT geometry describing the AOI.
  source            *Required*. Your GRiD generated API key.
  subscribe         *Optional*. True, False, T, F, 1, 0. Default: false

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains an [AOI Detail object](#aoi-detail-object) in
JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v1/aoi/add/?source=grid&name=test&geom=POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))&subscribe=True
~~~~

~~~~ {.json}
{
    "1592": {
        "aoi": [
            {
                "fields": {
                    "clip_geometry": "SRID=4326;POLYGON ((30.0000000000000000 10.0000000000000000, 40.0000000000000000 40.0000000000000000, 20.0000000000000000 40.0000000000000000, 10.0000000000000000 20.0000000000000000, 30.0000000000000000 10.0000000000000000))", 
                    "created_at": "2015-11-13T12:58:28.040", 
                    "is_active": true, 
                    "name": "test", 
                    "notes": "", 
                    "source": "api", 
                    "user": 102
                }, 
                "model": "export.aoi", 
                "pk": 1592
            }
        ], 
        "export_set": [], 
        "pointcloud_collects": [], 
        "raster_collects": []
    }, 
    "GRiD API": {
        "API Version": "v1"
    }, 
    "success": true
}
~~~~

### Get Export Details

Get information for a single export.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v1/export/{pk}
~~~~

#### Request Parameters

  Path parameter   Value
  ---------------- ---------------------------------
  pk               *Required*.The primary key for the export.
  
  Query parameter   Value
  ----------------- ------------------------------------------------
  source           *Required*. Your GRiD generated API key.  

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains an [Export Detail
object](#export-detail-object) in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v1/export/1335?source=grid
~~~~

~~~~ {.json}
{
  "GRiD API": {
    "API Version": "v1"
    }
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
      "created_at": "2015-05-12T18:25:05.082077",
      "pk": 1069,
      "notes": ""
    }, {
      "status": "SUCCESS",
      "tda_type": "Hlz",
      "name": "HelicopterLandingZoneResult",
      "url": "http://gridte.rsgis.erdc.dren.mil/te_ba/tda/download/1068/",
      "created_at": "2015-05-12T18:24:20.701910",
      "pk": 1068,
      "notes": ""
    }
  ]
}
~~~~

### Lookup Geoname

Get suggested AOI name based on geographic coordinates of the geometry.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v1/geoname
~~~~

#### Request Parameters

  Query parameter   Value
  ----------------- ------------------------------------------------
  geom              *Required*. A WKT geometry describing the AOI.
  source            *Required*. Your GRiD generated API key.

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains a [Geoname object](#geoname-object) in JSON
format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v1/geoname/?geom=POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))&source=grid
~~~~

~~~~ {.json}
{
    "GRiD API": {
        "API Version": "v1"
    }, 
    "name": "Great Sand Sea", 
    "provided_geometry": "POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))"
}
~~~~

### Get Task Details

Get task status/details for the provided task\_id.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v1/task/{task_id}
~~~~

#### Request Parameters

  Path parameter   Value
  ---------------- ---------------------
  task\_id          *Required*. The ID of the task.
  
  Query parameter   Value
  ----------------- ------------------------------------------------
  source            *Required*. Your GRiD generated API key.

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains an [Task object](#export-detail-object) in
JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v1/task/bacb736e-e900-457c-9b24-fd409bc3019d/?source=grid
~~~~

~~~~ {.json}
{
  "GRiD API": {
    "API Version": "v1"
  }, 
  "task_traceback": "",
  "task_state": "SUCCESS",
  "task_tstamp": "2015-09-09T14:19:36.080",
  "task_name": "export.tasks.generate_export",
  "task_id": "774b4666-5706-4237-8661-df0f96cd7b9c"
}
~~~~

### Generate Point Cloud Export

Generate point cloud export for the given AOI primary key and collect
primary keys.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v1/aoi/{pk}/generate/pointcloud
~~~~

#### Request Parameters

  Path parameter   Value
  ---------------- -----------------------------
  pk               The primary key of the AOI.

  Query parameter         Value
  ----------------------- ---------------------------------------------------------------------------------------------------------------------------------
  collects                *Required*. A list of collection primary keys to include in the export, separated by `+` or `,`.
  source                  *Required*. Your GRiD generated API key.
  intensity               *Optional*. Whther or not to export intensity. Default: True.
  dim\_classification     *Optional*. Wthere or not to export classification. Default: True
  hsrs                    *Optional*. Accepts an EPSG code. Defaults to AOI SRS
  file\_export\n_options  *Optional*. Determmine file merging strategy.  Accepts ``individual`` and ``collect``. Default ``individual``
  compressed              *Optional*. Whether or not to export compressed data. Default: True.
  send\_email             *Optional*. Whether or not to notify user via email upon completion. Default: False.
  generate\_dem           *Optional*. Whether or not to generate a DEM from the export. Default: False.
  cell\_spacing           *Optional*. Used together with ``generate\_dem``.  Default: 1.0
  pcl\_terrain            *Optional*. Used to trigger a PMF Bare Earth export. Accepts ``ubran``, ``suburban``, ``mountainous``, and ``foliated``.  Default: None
  sri\_hres               *Optional*. Used to trigger a Sarnoff Bare Earth export.  Accespts the horizontal resolution.  Default: None
  
#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains a [Generate export
object](#generate-export-object) in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/api/v1/aoi/2389/generate/pointcloud/?collects=100+102&source=grid
~~~~

~~~~ {.json}
{
  "GRiD API": {
    "API Version": "v1"
  }, 
  "started" : true,
  "task_id" : "774b4666-5706-4237-8661-df0f96cd7b9c"
}
~~~~


### Generate Raster Export

Generate point cloud export for the given AOI primary key and collect
primary keys.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v1/aoi/{pk}/generate/raster
~~~~

#### Request Parameters

  Path parameter   Value
  ---------------- -----------------------------
  pk               The primary key of the AOI.

  Query parameter         Value
  ----------------------- ---------------------------------------------------------------------------------------------------------------------------------
  collects                *Required*. A list of collection primary keys to include in the export, separated by `+` or `,`.
  source                  *Required*. Your GRiD generated API key.
  hsrs                    *Optional*. Accepts an EPSG code. Defaults to AOI SRS
  file\_export\n_options  *Optional*. Determmine file merging strategy.  Accepts ``individual`` and ``collect``. Default ``individual``
  compressed              *Optional*. Whether or not to export compressed data. Default: True.
  send\_email             *Optional*. Whether or not to notify user via email upon completion. Default: False.

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains a [Generate export
object](#generate-export-object) in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/api/v1/aoi/2389/generate/raster/?collects=100+102&source=grid
~~~~

~~~~ {.json}
{
  "GRiD API": {
    "API Version": "v1"
  }, 
  "started" : true,
  "task_id" : "774b4666-5706-4237-8661-df0f96cd7b9c"
}
~~~~
