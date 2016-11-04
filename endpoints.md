GRiD API v2
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
~~~~

### Get a User's AOI List

Get a list of the AOIs created by or shared with the current GRiD user.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v2/aoi
~~~~

#### Request Parameters

  Query parameter   Value
  ----------------- --------------------------------------------------------
  source            *Required*. Your GRiD generated API key.
  geom              *Optional*. A WKT geometry used to filter AOI results.

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains an 'aoi_list' dictionary that contains an array of [AOI object](#aoi-object) in JSON
format. 
On failure, the HTTP status code in the header response is `400` BAD and the response body contains an error 
in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v2/aoi/?geom=POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))&source=grid
~~~~

~~~~ {.json}
{
    "aoi_list": [
      {
        "geom": "SRID=4326;POLYGON ((68.9150709532930961 33.5950250284996983, 68.8704389952918063 33.5955969812235011,
        68.8724989318148033 33.5858732691386024, 68.9020246886466055 33.5853012519442018, 68.9068312072003977 33.5549789148388982,
        68.9274305724316037 33.5589843621810999, 68.9274305724316037 33.5944530719840984, 68.9150709532930961 33.5950250284996983))", 
        "created_at": "2013-04-16T13:10:33.974", 
        "is_active": true, 
        "name": "First_Aoi", 
        "notes": "notes", 
        "source": "map", 
        "user": 102,
        "pk": 123
      },
      {
        "geom": "SRID=4326;POLYGON ((64.2115925480768936 36.8743567152622020, 59.2018269230769008 32.7632670467287994,
        68.6940144230768936 32.9847159272803978, 64.2115925480768936 36.8743567152622020))", 
        "created_at": "2015-09-23T09:50:19.856", 
        "is_active": true, 
        "name": "Second_Aoi", 
        "notes": "", 
        "source": "map", 
        "user": 102,
        "pk": 1304
      }
    ], 
}
~~~~

### Get AOI Details

Get information for a single AOI.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v2/aoi/{pk}
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
On failure, the HTTP status code in the header response is `400` 
BAD and the response body contains an error in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v2/aoi/123/?source=grid
~~~~

~~~~ {.json}
{
    "geom": "SRID=4326;POLYGON ((68.9150709532930961 33.5950250284996983, 68.8704389952918063 33.5955969812235011,
    68.8724989318148033 33.5858732691386024, 68.9020246886466055 33.5853012519442018, 68.9068312072003977 33.5549789148388982,
    68.9274305724316037 33.5589843621810999, 68.9274305724316037 33.5944530719840984, 68.9150709532930961 33.5950250284996983))",
    "created_at": "2013-04-16T13:10:33.974",
    "is_active": true,
    "name": "First_Aoi",
    "notes": "",
    "source": "api",
    "user": 102,
    "pk": 123, 
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
    "pointcloud_intersects": [
        {
            "percent_coverage": 1.0,
            "point_count": 3040524,
            "classification": "UNCLASS",
            "area": 3.17799291347327,
            "datatype": "LAS 1.2",
            "density": 0.9657120156,
            "filesize": 61731366,
            "collected_at": "2012-05-04",
            "pk": 209,
            "sensor": "NGA ALIRT",
            "name": "20120504_00_0_UFO"
        }
    ], 
    "raster_intersects": []
}
~~~~

### Add AOI

Create a new AOI for the given geometry.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v2/aoi/add
~~~~

#### Request Parameters

  Query parameter   Value
  ----------------- -----------------------------------------------------
  source            *Required*. Your GRiD generated API key.
  name              *Required*. The name for the AOI.
  geom              *Required*. A WKT geometry describing the AOI.
  subscribe         *Optional*. True, False, T, F, 1, 0. Default: false

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains an [AOI Detail object](#aoi-detail-object) in
JSON format. 
On failure, the HTTP status code in the header response is 
`400` BAD and the response body contains an error in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v2/aoi/add/?source=grid&name=test&geom=POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))&subscribe=True
~~~~

~~~~ {.json}
{
    "geom": "SRID=4326;POLYGON ((30.0000000000000000 10.0000000000000000, 40.0000000000000000 40.0000000000000000,
    20.0000000000000000 40.0000000000000000, 10.0000000000000000 20.0000000000000000, 30.0000000000000000 10.0000000000000000))",
    "created_at": "2015-11-13T12:58:28.040",
    "is_active": true,
    "name": "test",
    "notes": "",
    "source": "api",
    "user": 102,
    "pk": 1592,
    "export_set": [],
    "pointcloud_intersects": [],
    "raster_intersects": [
        {
        "name": "20120424_00_0_UFO",
        "classification": "UNCLASS",
        "area": 27.4865918090656,
        "datatype": "DSM",
        "filesize": 109947223,
        "collected_at": "2012-04-24",
        "percent_coverage": 0.02,
        "pk": 233,
        "sensor": "NGA ALIRT"
        }
    ],
}
~~~~

### Edit AOI

Update an AOIs name, notes, or geometry.  In order to change an AOI's geometry, it must contain 0 generated exports.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v2/aoi/edit/<pk>
~~~~

#### Request Parameters

  Path parameter   Value
  ---------------- -----------------------------
  pk               The primary key of the AOI.

  Query parameter   Value
  ----------------- -----------------------------------------------------
  source            *Required*. Your GRiD generated API key.
  name              *Optional*. The name for the AOI.
  geom              *Optional*. A WKT geometry describing the AOI.
  notes             *Optional*. The notes for the AOI.

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains an [AOI Detail object](#aoi-detail-object) in
JSON format. 
On failure, the HTTP status code in the header response is 
`400` BAD and the response body contains an error in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v2/aoi/edit/123/?source=grid&name=new name&notes=updated notes
~~~~

~~~~ {.json}
{
    "geom": "SRID=4326;POLYGON ((30.0000000000000000 10.0000000000000000, 40.0000000000000000 40.0000000000000000,
    20.0000000000000000 40.0000000000000000, 10.0000000000000000 20.0000000000000000, 30.0000000000000000 10.0000000000000000))",
    "created_at": "2015-11-13T12:58:28.040",
    "is_active": true,
    "name": "new name",
    "notes": "updated notes",
    "source": "api",
    "user": 102,
    "pk": 123,
    "export_set": [],
    "pointcloud_intersects": [],
    "raster_intersects": [],
    "export_set": [], 
    "pointcloud_intersects": [], 
    "raster_intersects": [],
}
~~~~

### Delete AOI

Delete an existing AOI.  

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v2/aoi/delete/<pk>
~~~~

#### Request Parameters

  Path parameter   Value
  ---------------- -----------------------------
  pk               The primary key of the AOI.
  
  Query parameter   Value
  ----------------- ------------------------------------------------
  source            *Required*. Your GRiD generated API key.

#### Response Format

On success, the HTTP status code in the header response is `200` OK.
On failure, the HTTP status code in the header response is `400` BAD and the response body contains an error in JSON format.
#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v2/aoi/delete/123/?source=grid
~~~~

### Get Export Details

Get information for a single export.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v2/export/{pk}
~~~~

#### Request Parameters

  Path parameter   Value
  ---------------- ---------------------------------
  pk               *Required*.The primary key for the export.
  
  Query parameter   Value
  ----------------- ------------------------------------------------
  source            *Required*. Your GRiD generated API key.  

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains an [Export Detail
object](#export-detail-object) in JSON format.
On failure, the HTTP status code in the header response is `400` BAD and 
the response body contains an error in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v2/export/1335/?source=grid
~~~~

~~~~ {.json}
{
  "status": "SUCCESS",
  "pcl_terrain": "",
  "dim_classification": true,
  "file_export_options": "individual",
  "file_export_type": "las12",
  "name": "",
  "classification": "",
  "datatype": "LAS 1.2",
  "notes": "",
  "rgb": false,
  "hsrs": "32641",
  "url": "http://localhost:8000/export/download/2880/",
  "intensity": true,
  "pk": 2880,
  "generate_dem": false,
  "started_at": "2016-05-16T16:18:12.752305",
  "sri_hres": null,
  "decimation_radius": null,
  "capacity": null,
  "length": null,
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

### Edit Export

Update an Exports name or notes.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v2/export/edit/<pk>
~~~~

#### Request Parameters

  Path parameter   Value
  ---------------- -----------------------------
  pk               The primary key of the export.

  Query parameter   Value
  ----------------- -----------------------------------------------------
  source            *Required*. Your GRiD generated API key.
  name              *Optional*. The name for the export.
  notes             *Optional*. User notes.

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains an [Export Detail object](#export-detail-object) in
JSON format.
On failure, the HTTP status code in the header response is `400` BAD and the response body contains an error 
in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v2/export/edit/1335/?source=grid&name=new name&notes=notes
~~~~

~~~~ {.json}
{
    "status": "SUCCESS",
    "pcl_terrain": "",
    "dim_classification": true,
    "file_export_options": "individual",
    "file_export_type": "las12",
    "name": "new name",
    "classification": "",
    "datatype": "LAS 1.2",
    "notes": "notes",
    "rgb": false,
    "hsrs": "32641",
    "url": "http://localhost:8000/export/download/1335/",
    "intensity": true,
    "pk": 1335,
    "generate_dem": false,
    "started_at": "2016-05-16T16:18:12.752305",
    "sri_hres": null,
    "decimation_radius": null,
    "capacity": null,
    "length": null,
    },
    "exportfiles": [
    {
      "url": "http://gridte.rsgis.erdc.dren.mil/te_ba/export/download/file/30359/",
      "pk": 30359,
      "name": "ExportedFile.laz"
    }
    ],
    "tda_set": [],
}
~~~~

### Delete Export

Delete an existing Export.  

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v2/export/delete/<pk>
~~~~

#### Request Parameters

  Path parameter   Value
  ---------------- -----------------------------
  pk               The primary key of the export.
  
  Query parameter   Value
  ----------------- ------------------------------------------------
  source            *Required*. Your GRiD generated API key.

#### Response Format

On success, the HTTP status code in the header response is `200` OK.
On failure, the HTTP status code in the header response is `400` BAD and the response body contains an error 
in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v2/export/delete/1335/?source=grid
~~~~


### Get Product Details

Get information for a single Product.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v2/product/{pk}
~~~~

#### Request Parameters

  Path parameter   Value
  ---------------- ------------------------------
  pk                *Required*. The primary key for the Product.
  
  Query parameter   Value
  ----------------- ------------------------------------------------
  source            *Required*. Your GRiD generated API key.

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains an [Product Detail object](#product-detail-object) in
JSON format.
On failure, the HTTP status code in the header response is `400` BAD and the response body contains an error 
in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v2/product/252/?source=grid
~~~~

~~~~ {.json}
{
    "geom": "POLYGON ((70.0499966824633020 35.2004503720556983, 70.0493481153355049 35.1499987225927981, 70.1000060967199943 35.1495493748128993, 70.1006859587326971 35.2000001882180982, 70.0499966824633020 35.2004503720556983))",
    "name": "20101109_00_0_UFO",
    "classification": "UNCLASS",
    "collected_at": "2010-11-09",
    "datatype": "DSM",
    "pk": 252,
    "area": 25.8400993148659,
    "sensor": "NGA ALIRT",
    "filesize": 103347831
}
~~~~

### Lookup Geoname

Get suggested AOI name based on geographic coordinates of the geometry.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v2/geoname
~~~~

#### Request Parameters

  Query parameter   Value
  ----------------- ------------------------------------------------
  source            *Required*. Your GRiD generated API key.
  geom              *Required*. A WKT geometry describing the AOI.

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains a [Geoname object](#geoname-object) in JSON
format.
On failure, the HTTP status code in the header response is `400` BAD and the response body contains an error 
in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v2/geoname/?geom=POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))&source=grid
~~~~

~~~~ {.json}
{
    "name": "Great Sand Sea", 
    "geom": "POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))"
}
~~~~

### Get Task Details

Get task status/details for the provided task\_id.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v2/task/{task_id}
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
On failure, the HTTP status code in the header response is `400` BAD and the response body contains an error 
in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/v2/task/bacb736e-e900-457c-9b24-fd409bc3019d/?source=grid
~~~~

~~~~ {.json}
{
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
GET <instance_url>/<instance_root>_ba/api/v2/aoi/{pk}/generate/pointcloud
~~~~

#### Request Parameters

  Path parameter   Value
  ---------------- -----------------------------
  pk               The primary key of the AOI.

  ----------------------------------------------------------------------------------------------
  Query parameter       Value
  --------------------- -------------------------------------------------------------------------
  source                *Required*. Your GRiD generated API key.
  
  products              *Required*. A list of product primary keys to include in the export, separated by `+` or `,`.
  
  name                  *Optional*. An optional name for the export.
  
  intensity             *Optional*. Whether or not to export intensity. Default: True.
  
  dim\_classification   *Optional*. Whether or not to export classification. Default: True.
  
  hsrs                  *Optional*. Accepts an EPSG code. Defaults to AOI SRS.
  
  file\_export\_options *Optional*. Determine file merging strategy. Accepts ``individual`` and ``collect``. Default: ``individual``.
  
  file\_export\_type    *Optional*. Determine the format of the output file. Accepts ``las12``, ``las14``, ``nitf``, ``pdf``, and ``bpf3``.  Default: ``las12``.
  
  compressed            *Optional*. Whether or not to export compressed data. Default: True.
  
  send\_email           *Optional*. Whether or not to notify user via email upon completion. Default: False.
  
  generate\_dem         *Optional*. Whether or not to generate a DEM from the pointcloud. Default: False.
  
  cell\_spacing         *Optional*. Used together with ``generate_dem``.  Default: 1.0.
  
  pcl\_terrain          *Optional*. Used to trigger a PMF Bare Earth export. Accepts ``ubran``, ``suburban``, ``mountainous``, and ``foliated``.  Default: None.  Cannot be used with sri_hres option.
  
  sri\_hres             *Optional*. Used to trigger a Sarnoff Bare Earth export.  Accepts the horizontal resolution.  Default: None.  Cannot be used with pcl\_terrain option.
  
  decimation\_radius    *Optional*. The minimum distance between points. If a neighboring point is found within this radius, it will be discarded. Uses PDAL decimation filter. Default: None.
  
  capacity              *Optional*. How many points to fit into each tile. The number of points in each tile will not exceed this value, and will sometimes be less than it. Uses PDAL chipper filter. Cannot be used with length option. Default: None.
  
  length                *Optional*. The target length of generated tiles. Units determined by source data. Uses PDAL splitter filter. Cannot be used with capacity option. Default: None.
  ----------------------------------------------------------------------------------------------

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains a [Generate export
object](#generate-export-object) in JSON format.
On failure, the HTTP status code in the header response is `400` BAD and the response body contains an error 
in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/api/v2/aoi/2389/generate/pointcloud/?products=100+102&source=grid
~~~~

~~~~ {.json}
{
  "export_id" : 1568,
  "task_id" : "774b4666-5706-4237-8661-df0f96cd7b9c"
}
~~~~


### Generate Raster Export

Generate point cloud export for the given AOI primary key and collect
primary keys.

#### Endpoint

~~~~ {.bash}
GET <instance_url>/<instance_root>_ba/api/v2/aoi/{pk}/generate/raster
~~~~

#### Request Parameters

  Path parameter   Value
  ---------------- -----------------------------
  pk               The primary key of the AOI.

  ------------------------------------------------------------------------------------------------
  Query parameter        Value
  ---------------------- -------------------------------------------------------------------------
  source                 *Required*. Your GRiD generated API key.
  
  products               *Required*. A list of product primary keys to include in the export, separated by `+` or `,`.
  
  name                   *Optional*. An optional name for the export.
  
  hsrs                   *Optional*. Accepts an EPSG code. Defaults to AOI SRS.
  
  file\_export\_options  *Optional*. Determine file merging strategy.  Accepts ``individual`` and ``collect``. Default ``individual``
  
  file\_format\_options  *Optional*. Determine the format of the output file.  Accepts  ``GTiff`` and ``NITF``. Default: ``GTiff``
  
  compressed             *Optional*. Whether or not to export compressed data. Default: True.
  
  send\_email            *Optional*. Whether or not to notify user via email upon completion. Default: False.
  ------------------------------------------------------------------------------------------------

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains a [Generate export
object](#generate-export-object) in JSON format.
On failure, the HTTP status code in the header response is `400` BAD and the response body contains an error 
in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/api/v2/aoi/2389/generate/raster/?collects=100+102&source=grid
~~~~

~~~~ {.json}
{
  "export_id" : 1569,
  "task_id" : "774b4666-5706-4237-8661-df0f96cd7b9c"
}
~~~~
