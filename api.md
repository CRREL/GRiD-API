GRiD API
========

API Endpoint Reference
----------------------

### Get a User's AOI List

Get a list of the AOIs created by or shared with the current GRiD user.

#### Endpoint

~~~~ {.bash}
GET http://gridte.rsgis.erdc.dren.mil/te_ba/api/export
~~~~

#### Request Parameters

  Query parameter    Value
  ------------------ ------------------------------------------------------
  geom               *Optional*. A WKT geometry used to filter AOI results.

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains an array of [AOI object](#aoi-object) in JSON
format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/export/?geom=POLYGON ((62.1873999999999967 34.3468000000000018, 62.1873999999999967 34.3451999999999984, 62.1901000000000010 34.3451999999999984, 62.1901000000000010 34.3468000000000018, 62.1873999999999967 34.3468000000000018))
~~~~

~~~~ {.json}
{
  "self_aoi_list": [
    {
      "name": "Citadel",
      "geometry": "POLYGON ((62.1873999999999967 34.3468000000000018, 62.1873999999999967 34.3451999999999984, 62.1901000000000010 34.3451999999999984, 62.1901000000000010 34.3468000000000018, 62.1873999999999967 34.3468000000000018))",
      "notes": "",
      "is_active": true,
      "source": "api",
      "num_exports": "3 exports",
      "pk": 1959,
      "created_at": "2015-07-07 23:30:29.088539"
    }, {
      "name": "GQ",
      "geometry": "POLYGON ((62.1864787493088969 34.3478412788699998, 62.1864787493088969 34.3420833670284011, 62.2000399980870995 34.3420833670284011, 62.1999970827424988 34.3478412788699998, 62.1981517229404020 34.3478589949110997, 62.1954265985821024 34.3478589949113982, 62.1905771646832974 34.3478589949115971, 62.1864787493088969 34.3478412788699998))",
      "notes": "",
      "is_active": true,
      "source": "map",
      "num_exports": "6 exports",
      "pk": 1855,
      "created_at": "2015-06-23 13:21:50.034012"
    }
  ]
}
~~~~

### Get AOI Details

Get information for a single AOI.

#### Endpoint

~~~~ {.bash}
GET http://gridte.rsgis.erdc.dren.mil/te_ba/api/export/{pk}
~~~~

#### Request Parameters

  Path parameter    Value
  ----------------- ------------------------------------------------------
  pk                The primary key for the AOI.

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains an [AOI Detail object](#aoi-detail-object) in
JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/export/1959
~~~~

~~~~ {.json}
{
  "export_set": [
    {
      "status": "SUCCESS",
      "stated_at": "2015-07-07 23:33:24.247148",
      "name": "Citadel_WGS84-UTMzone41N_2015-Jul-07.zip",
      "datatype": "LAS 1.2",
      "hsrs": 32641,
      "url": "http://gridte.rsgis.erdc.dren.mil/te_ba/export/download/3561/",
      "pk": 3561
    }, {
      "status": "SUCCESS",
      "stated_at": "2015-07-07 23:31:32.584232",
      "name": "Citadel_WGS84-UTMzone41N_2015-Jul-07.zip",
      "datatype": "DSM",
      "hsrs": 32641,
      "url": "http://gridte.rsgis.erdc.dren.mil/te_ba/export/download/3560/",
      "pk": 3560
    }
  ],
  "aoi": [
    {
      "fields": {
        "name": "Citadel",
        "created_at": "2015-07-07T23:30:29.088",
        "is_active": true,
        "source": "api",
        "user": 90,
        "clip_geometry": "POLYGON ((62.1873999999999967 34.3468000000000018, 62.1873999999999967 34.3451999999999984, 62.1901000000000010 34.3451999999999984, 62.1901000000000010 34.3468000000000018, 62.1873999999999967 34.3468000000000018))",
        "notes": ""
      },
      "model": "export.aoi",
      "pk": 1959
    }
  ],
  "collects": [
    {
      "fields": {
        "name": "20110914_00_0_UFO"
      },
      "model": "loaddata.collect",
      "pk": 2298
    }, {
      "fields": {
        "name": "20111123_00_0_UFO"
      },
      "model": "loaddata.collect",
      "pk": 3109
    }
  ]
}
~~~~

### Add AOI

Create a new AOI for the given geometry.

#### Endpoint

~~~~ {.bash}
GET http://gridte.rsgis.erdc.dren.mil/te_ba/api/export/add
~~~~

#### Request Parameters

  Query parameter    Value
  ------------------ ------------------------------------------------------
  name               *Required*. The name for the AOI.
  geom               *Required*. A WKT geometry describing the AOI.
  subscribe          *Optional*. True, False, T, F, 1, 0. Default: false

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains an [Upload object](#aoi-detail-object) in
JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/export/add/?name=test&geom=POLYGON ((68.9150709532930961 33.5950250284996983, 68.8704389952918063 33.5955969812235011, 68.8724989318148033 33.5858732691386024, 68.9020246886466055 33.5853012519442018, 68.9068312072003977 33.5549789148388982, 68.9274305724316037 33.5589843621810999, 68.9274305724316037 33.5944530719840984, 68.9150709532930961 33.5950250284996983))&subscribe=True
~~~~

~~~~ {.json}
{
  "aoi": [
    {
      "geometry": "POLYGON ((68.9150709532930961 33.5950250284996983, 68.8704389952918063 33.5955969812235011, 68.8724989318148033 33.5858732691386024, 68.9020246886466055 33.5853012519442018, 68.9068312072003977 33.5549789148388982, 68.9274305724316037 33.5589843621810999, 68.9274305724316037 33.5944530719840984, 68.9150709532930961 33.5950250284996983))",
      "pk": 2086,
      "name": "test",
      "subscribed": true
    }
  ],
  "success": true
}
~~~~

### Get Export Details

Get information for a single export.

#### Endpoint

~~~~ {.bash}
GET http://gridte.rsgis.erdc.dren.mil/te_ba/api/export/export/{pk}
~~~~

#### Request Parameters

  Path parameter   Value
  ---------------- -------------------------------------------------------
  pk               The primary key for the export.

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains an [Export Detail
object](#export-detail-object) in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/export/export/3124
~~~~

~~~~ {.json}
{
  "exportfiles": [
    {
      "url": "http://gridte.rsgis.erdc.dren.mil/te_ba/export/download/file/30359/",
      "pk": 30359,
      "name": "LAS_Kabul-24-Sep.BuckEye.09317_Kabul_Site09.GRiD.20150511.1839.laz"
    }
  ],
  "tda_set": [
    {
      "status": "SUCCESS",
      "tda_type": "Los",
      "name": "RAD M91",
      "url": "http://gridte.rsgis.erdc.dren.mil/te_ba/tda/download/1069/",
      "created_at": "2015-05-12 18:25:05.082077",
      "pk": 1069,
      "notes": ""
    }, {
      "status": "SUCCESS",
      "tda_type": "Hlz",
      "name": "Chinook",
      "url": "http://gridte.rsgis.erdc.dren.mil/te_ba/tda/download/1068/",
      "created_at": "2015-05-12 18:24:20.701910",
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
GET http://gridte.rsgis.erdc.dren.mil/te_ba/api/export/geoname
~~~~

#### Request Parameters

  Query parameter    Value
  ------------------ ------------------------------------------------------
  geom               *Required*. A WKT geometry describing the AOI.

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains a [Geoname object](#geoname-object) in JSON
format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/export/geoname/?geom=POLYGON ((68.9150709532930961 33.5950250284996983, 68.8704389952918063 33.5955969812235011, 68.8724989318148033 33.5858732691386024, 68.9020246886466055 33.5853012519442018, 68.9068312072003977 33.5549789148388982, 68.9274305724316037 33.5589843621810999, 68.9274305724316037 33.5944530719840984, 68.9150709532930961 33.5950250284996983))
~~~~

~~~~ {.json}
{
  "name": "Marghah Ghar",
  "provided_geometry": "POLYGON ((68.9150709532930961 33.5950250284996983, 68.8704389952918063 33.5955969812235011, 68.8724989318148033 33.5858732691386024, 68.9020246886466055 33.5853012519442018, 68.9068312072003977 33.5549789148388982, 68.9274305724316037 33.5589843621810999, 68.9274305724316037 33.5944530719840984, 68.9150709532930961 33.5950250284996983))"
}
~~~~

### Get Task Details

Get task status/details for the provided task\_id.

#### Endpoint

~~~~ {.bash}
GET http://gridte.rsgis.erdc.dren.mil/te_ba/api/export/task/{task_id}
~~~~

#### Request Parameters

  Path parameter    Value
  ----------------- ------------------------------------------------------
  task\_id          The ID of the task.

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains an [Task object](#export-detail-object) in
JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/export/task/bacb736e-e900-457c-9b24-fd409bc3019d/
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
IDs.

#### Endpoint

~~~~ {.bash}
GET http://gridte.rsgis.erdc.dren.mil/te_ba/api/export/aoi/{pk}/generate/pointcloud
~~~~

#### Request Parameters

  Path parameter    Value
  ----------------- ------------------------------------------------------
  pk                The primary key of the AOI.

  -------------------------------------------------------------------------
  Query parameter    Value
  ------------------ ------------------------------------------------------
  collects           *Required*. A list of collection IDs to include in the
                     export.
  -------------------------------------------------------------------------

#### Response Format

On success, the HTTP status code in the header response is `200` OK and
the response body contains a [Generate pointcloud
object](#generate-pointcloud-object) in JSON format.

#### Example

~~~~ {.bash}
curl -u <username> http://gridte.rsgis.erdc.dren.mil/api/export/aoi/2389/generate/pointcloud/?collects=5439
~~~~

~~~~ {.json}
{
  "started" : true,
  "task_id" : "774b4666-5706-4237-8661-df0f96cd7b9c"
}
~~~~

Object Model
------------

### AOI object

  Key            Value Type   Value Description
  -------------- ------------ -------------------------------------------------------------
  name           string       The name of the AOI.
  geometry       string       The WKT geometry of the AOI.
  notes          string       User notes.
  is\_active     boolean      Whether or not the AOI is active.
  source         string       Source of the AOI (e.g., map, api).
  num\_exports   string       The number of exports that have been generated for the AOI.
  pk             integer      The primary key of the AOI.
  created\_at    timestamp    Time of creation for the AOI: `YYYY-MM-DD HH24:MI:SS.FF6`

### AOI object2

  Key                     Value Type   Value Description
  ----------------------- ------------ -------------------------------------
  fields.name             string       The name of the AOI.
  fields.created\_at      timestamp    ISO 8601 format as UTC.
  fields.is\_active       boolean      Whether or not the AOI is active.
  fields.source           string       Source of the AOI (e.g., map, api).
  fields.user             integer      The id of the creating user.
  fields.clip\_geometry   string       The WKT geometry of the AOI.
  fields.notes            string       User notes.
  model                   string       The model (e.g., export.aoi).
  pk                      integer      The primary key of the AOI.

### AOI Detail object

  Key           Value Type                                    Value Description
  ------------- --------------------------------------------- ----------------------------
  export\_set   array of [exports objects](#export-object)    The exports of the AOI.
  aoi           array of [aoi objects](#aoi-object2)          The AOI detail (repeated).
  collects      array of [collect objects](#collect-object)   The collects for the AOI.

### AOI Upload object

  Key          Value Type   Value Description
  ------------ ------------ ---------------------------------------------------
  geometry     string       WKT of the uploaded AOI.
  pk           integer      The primary key of the uploaded AOI.
  name         string       The name of the uploaded AOI.
  subscribed   boolean      Whether or not the user is subscribed to the AOI.

### Collect object

  Key           Value Type   Value Description
  ------------- ------------ -------------------------------------
  fields.name   string       The name of the collect.
  model         string       The model (e.g., loaddata.collect).
  pk            integer      The primary key of the collect.

### Export object

  Key          Value Type   Value Description
  ------------ ------------ -----------------------------------------------------------
  status       string       The status of the export (e.g., SUCCESS, FAILED, QUEUED).
  stated\_at   timestamp    Time of creation for the AOI: `YYYY-MM-DD HH24:MI:SS.FF6`
  name         string       The name of the export.
  datatype     string       The datatype (e.g., LAS 1.2, DTM).
  hsrs         integer      The Horizontal Spatial Reference System EPSG code.
  url          string       The download URL of the export.
  pk           integer      The primary key of the export.

### Export Detail object

  Key           Value Type                                            Value Description
  ------------- ----------------------------------------------------- -------------------------------------
  exportfiles   array of [Exportfiles objects](#exportfiles-object)   The export files of the export set.
  tda\_set      array of [TDA Set objects](#tda-set-object)           The TDAs of the export set.

### Exportfiles object

  Key    Value Type   Value Description
  ------ ------------ --------------------------------------
  url    string       The download URL of the export file.
  pk     integer      The primary key of the export file.
  name   string       The name of the export file.

### Generate Pointcloud object

  Key        Value Type   Value Description
  ---------- ------------ ---------------------------------------------------------
  started    boolean      Whether or not the point cloud export task has started.
  task\_id   string       The id of the task.

### Geoname object

  Key                  Value Type   Value Description
  -------------------- ------------ -------------------------------------------
  name                 string       The suggested name.
  provided\_geometry   string       WKT used to determine the suggested name.

### Task object

  Key               Value Type   Value Description
  ----------------- ------------ -------------------------------------------------------------
  task\_traceback   string       TBD
  task\_state       string       The state of the task (e.g., SUCCESS, FAILED, QUEUED).
  task\_tstamp      timestamp    ISO 8601 format as UTC.
  task\_name        string       The name of the task (e.g., export.tasks.generate\_export).
  task\_id          string       The id of the task.

### TDA Set object

  Key           Value Type   Value Description
  ------------- ------------ -----------------------------------------------------------
  status        string       The status of the export (e.g., SUCCESS, FAILED, QUEUED).
  tda\_type     string       The TDA type (e.g., Hlz, Los).
  name          string       The name of the TDA.
  url           string       The download URL of the TDA.
  created\_at   timestamp    Time of creation for the TDA: `YYYY-MM-DD HH24:MI:SS.FF6`
  pk            integer      The primary key of the TDA.
  notes         string       User notes.

### Upload object

  Key       Value Type                                          Value Description
  --------- --------------------------------------------------- ---------------------------
  aoi       array of [aoi upload objects](#aoi-upload-object)   The uploaded AOI.
  success   boolean                                             The status of the upload.
