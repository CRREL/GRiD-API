Object Model
------------

### AOI List object

  Key                     Value Type   Value Description
  ----------------------- ------------ -------------------------------------
  aoi.name                string       The name of the AOI.
  aoi.created\_at         timestamp    The date of AOI creation. ISO 8601 format as UTC.
  aoi.is\_active          boolean      Whether or not the AOI is active.
  aoi.source              string       Source of the AOI (e.g., map, api).
  aoi.user                integer      The id of the creating user.
  aoi.clip\_geometry      string       The WKT geometry of the AOI.
  aoi.notes               string       User notes.
  aoi.model               string       The model (e.g., export.aoi).
  aoi.pk                  integer      The primary key of the AOI.

### AOI Detail object

  Key                     Value Type   Value Description
  ----------------------- ------------ -------------------------------------
  aoi.clip\_geometry      string       The WKT geometry of the AOI.
  aoi.created\_at         timestamp    The date of AOI creation. ISO 8601 format as UTC.
  aoi.is\_active          boolean      Whether or not the AOI is active.
  aoi.name                string       The name of the AOI.
  aoi.notes               string       User notes.
  aoi.source              string       Source of the AOI (e.g., map, api).
  aoi.user                integer      The id of the creating user.
  aoi.pk                  integer      The primary key of the AOI.
  export\_set             array of [exports objects](#export-object)    The exports of the AOI.
  pointcloud_intersects   array of [product objects](#product-object)   The pointcloud products for the AOI
  raster_intersects       array of [product objects](#product-object)   The raster products for the AOI

### Pointcloud Product object

  Key            Value Type   Value Description
  -------------- ------------ -------------------------------------
  datatype       string       The datatype (e.g., LAS 1.2, DTM).
  name           string       The name of the product.
  pk             integer      The primary key of the product.
  sensor         string       The sensor used to make the collection.
  collect\_at    timestamp    The date of collection. ISO 8601 format as UTC.
  classification string       The security classification.
  geometry       string       The WKT geometry of the product.
  area           float        The area of the geometry in sq_km.
  coverage_ratio string       The percent of the product area covered by the AOI.
  filesize       integer      The size of the product on the filesystem in bytes.
  point_count    integer      The total number of points in the product.
  density        float        The average point density of the product.

### Raster Product object

  Key            Value Type   Value Description
  -------------- ------------ -------------------------------------
  datatype       string       The datatype (e.g., LAS 1.2, DTM).
  name           string       The name of the product.
  pk             integer      The primary key of the product.
  sensor         string       The sensor used to make the collection.
  collect\_at    timestamp    The date of collection. ISO 8601 format as UTC.
  classification string       The security classification.
  geometry       string       The WKT geometry of the product.
  area           float        The area of the geometry in sq_km.
  coverage_ratio string       The percent of the product area covered by the AOI.
  filesize       integer      The size of the product on the filesystem in bytes.

### Export object

  Key                 Value Type   Value Description
  ------------------- ------------ -----------------------------------------------------------
  datatype            string       The datatype (e.g., LAS 1.2, DTM).
  hsrs                string       The Horizontal Spatial Reference System EPSG code.
  name                string       The name of the export.
  pk                  integer      The primary key of the export.
  started\_at         timestamp    Time of creation for the AOI: `YYYY-MM-DD HH24:MI:SS.FF6`
  status              string       The status of the export (e.g., SUCCESS, FAILED, QUEUED).
  url                 string       The download URL of the export.

### Export Detail object

  Key                 Value Type                                            Value Description
  ------------------- ----------------------------------------------------- -------------------------------------
  datatype            string       The datatype (e.g., LAS 1.2, DTM).
  hsrs                string       The Horizontal Spatial Reference System EPSG code.
  name                string       The name of the export.
  pk                  integer      The primary key of the export.
  started\_at         timestamp    Time of creation for the AOI: `YYYY-MM-DD HH24:MI:SS.FF6`
  status              string       The status of the export (e.g., SUCCESS, FAILED, QUEUED).
  url                 string       The download URL of the export.
  rgb                 boolean      Whether or not RGB dimension is included in exported data.
  intensity           boolean      Whether or not Intensity dimension is included in exported data.
  dim_classification  boolean      Whether or not Classification dimension is included in exported data.
  file_export_options string       The file export option used (e.g., individual, collect, super).
  generate_dem        boolean      Whether or not this was a generated DEM from pointcloud.
  notes               string       The notes associated with the export.
  classification      string       The classifications selected for the export.
  pcl_terrain         string       The PCL terrain option of the export.
  sri_hres            decimal      The sri_hres value of the export.
  exportfiles         array of [Exportfiles objects](#exportfiles-object)   The export files of the export.
  tda\_set            array of [TDA Set objects](#tda-set-object)           The TDA set of the export.

### Exportfiles object

  Key    Value Type   Value Description
  ------ ------------ --------------------------------------
  name   string       The name of the export file.
  pk     integer      The primary key of the export file.
  url    string       The download URL of the export file.

### Generate Export object

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
  created\_at   timestamp    Time of creation for the TDA: `YYYY-MM-DD HH24:MI:SS.FF6`
  name          string       The name of the TDA.
  notes         string       User notes.
  pk            integer      The primary key of the TDA.
  status        string       The status of the export (e.g., SUCCESS, FAILED, QUEUED).
  tda\_type     string       The TDA type (e.g., Hlz, Los).
  url           string       The download URL of the TDA.

### Upload object

  Key       Value Type                                          Value Description
  --------- --------------------------------------------------- ---------------------------
  aoi       array of [aoi upload objects](#aoi-upload-object)   The uploaded AOI.
  success   boolean                                             The status of the upload.

### Error object
  Key       Value Type  Value Description
  --------- ----------- ---------------------------
  error     string      Description of the error from the given API request

