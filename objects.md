Object Model
------------

### AOI List object

  Key                     Value Type   Value Description
  ------------------- ------------ -------------------------------------
  name                string       The name of the AOI.
  created\_at         timestamp    The date of AOI creation. ISO 8601 format as UTC.
  is\_active          boolean      Whether or not the AOI is active.
  source              string       Source of the AOI (e.g., map, api).
  user                integer      The name of the creating user.
  clip\_geometry      string       The WKT geometry of the AOI.
  notes               string       User notes.
  pk                  integer      The primary key of the AOI.

### AOI Detail object

  Key                      Value Type                                             Value Description
  ---------------------- -------------------------------------------------------- -------------------------------------
  clip\_geometry         string                                                   The WKT geometry of the AOI.
  created\_at            timestamp                                                The date of AOI creation. ISO 8601 format as UTC.
  is\_active             boolean                                                  Whether or not the AOI is active.
  name                   string                                                   The name of the AOI.
  notes                  string                                                   User notes.
  source                 string                                                   Source of the AOI (e.g., map, api).
  user                   integer                                                  The id of the creating user.
  pk                     integer                                                  The primary key of the AOI.
  export\_set            array of [exports objects](#export-object)               The exports of the AOI.
  pointcloud\_intersects array of [pointcloud product objects](#pointcloud-product-object) The pointcloud products for the AOI.
  raster\_intersects     array of [raster product objects](#raster-product-object) The raster products for the AOI.

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
  coverage\_ratio string      The percent of the product area covered by the AOI.
  filesize       integer      The size of the product on the filesystem in bytes.
  point\_count    integer     The total number of points in the product.
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
  coverage\_ratio string      The percent of the product area covered by the AOI.
  filesize       integer      The size of the product on the filesystem in bytes.

### Export object

  Key                 Value Type   Value Description
  ------------------- ------------ -----------------------------------------------------------
  datatype            string       The datatype (e.g., LAS 1.2, DTM).
  user                integer      The id of the creating user.
  hsrs                string       The Horizontal Spatial Reference System EPSG code.
  name                string       The name of the export.
  pk                  integer      The primary key of the export.
  started\_at         timestamp    Time of creation for the AOI: `YYYY-MM-DD HH24:MI:SS.FF6`
  status              string       The status of the export (e.g., SUCCESS, FAILED, QUEUED).
  url                 string       The download URL of the export.

### Export Detail object (pointcloud)

  Key                   Value Type                                            Value Description
  --------------------- ----------------------------------------------------- -------------------------------------
  datatype              string       The datatype (e.g., LAS 1.2, DTM).
  user                  integer      The id of the creating user.
  hsrs                  string       The Horizontal Spatial Reference System EPSG code.
  name                  string       The name of the export.
  pk                    integer      The primary key of the export.
  started\_at           timestamp    Time of creation for the AOI: `YYYY-MM-DD HH24:MI:SS.FF6`
  status                string       The status of the export (e.g., SUCCESS, FAILED, QUEUED).
  url                   string       The download URL of the export.
  rgb                   boolean      Whether or not RGB dimension is included in exported data.
  intensity             boolean      Whether or not Intensity dimension is included in exported data.
  dim\_classification   boolean      Whether or not Classification dimension is included in exported data.
  file\_export\_options string       The file export option used (e.g., individual, collect, super).
  generate\_dem         boolean      Whether or not this was a generated DEM from pointcloud.
  cell\_spacing         float        The cell spacing used in DEM generation, if applicable.
  notes                 string       User notes.
  classification        string       The classifications selected for the export.
  pcl\_terrain          string       The PCL terrain option of the export.
  sri\_hres             decimal      The sri_hres value of the export.
  exportfiles           array of [Exportfile objects](#exportfile-object)   The export files of the export.
  tda\_set              array of [TDA objects](#tda-object)         The TDA set of the export.
  task\_id              string       The ID of the associated task used for generation.

### Export Detail object (raster)

  Key                   Value Type                                            Value Description
  --------------------- ----------------------------------------------------- -------------------------------------
  datatype              string       The datatype (e.g., LAS 1.2, DTM).
  user                  integer      The id of the creating user.
  hsrs                  string       The Horizontal Spatial Reference System EPSG code.
  name                  string       The name of the export.
  pk                    integer      The primary key of the export.
  started\_at           timestamp    Time of creation for the AOI: `YYYY-MM-DD HH24:MI:SS.FF6`
  status                string       The status of the export (e.g., SUCCESS, FAILED, QUEUED).
  url                   string       The download URL of the export.
  file\_export\_options string       The file export option used (e.g., individual, collect, super).
  file\_format\_options string       The format of the output file (e.g., GTiff, NITF).
  notes                 string       User notes.
  exportfiles           array of [Exportfile objects](#exportfile-object)   The export files of the export.
  tda\_set              array of [TDA objects](#tda-object)         The TDA set of the export.
  task\_id              string       The ID of the associated task used for generation.

### Exportfile object

  Key    Value Type   Value Description
  ------ ------------ --------------------------------------
  name   string       The name of the export file.
  pk     integer      The primary key of the export file.
  url    string       The download URL of the export file.

### Task object

  Key               Value Type   Value Description
  ----------------- ------------ -------------------------------------------------------------
  task\_traceback   string       The description of any failures if they occurred.
  task\_state       string       The state of the task (e.g., SUCCESS, FAILED, QUEUED).
  task\_tstamp      timestamp    ISO 8601 format as UTC.
  task\_name        string       The name of the task (e.g., export.tasks.generate\_export).
  task\_id          string       The id of the task.

### TDA object

  Key           Value Type   Value Description
  ------------- ------------ -----------------------------------------------------------
  created\_at   timestamp    Time of creation for the TDA: `YYYY-MM-DD HH24:MI:SS.FF6`
  name          string       The name of the TDA.
  notes         string       User notes.
  pk            integer      The primary key of the TDA.
  status        string       The status of the export (e.g., SUCCESS, FAILED, QUEUED).
  tda\_type     string       The TDA type (e.g., Hlz, Los).
  url           string       The download URL of the TDA.

