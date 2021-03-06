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

  Key               Value Type                                      Value Description
  ----------------- ----------------------------------------------- ----------------------------------------------
  export\_set        array of [exports objects](#export-object)      The exports of the AOI.
  aoi               array of [aoi objects](#aoi-object2)            The AOI detail (repeated).
  pc\_intersects     array of [collect objects](#collect-object)     The intersecting PC collects for the AOI.
  raster\_intersects array of [collect objects](#collect-object)     The intersecting raster collects for the AOI.

### AOI Upload object

  Key          Value Type   Value Description
  ------------ ------------ ---------------------------------------------------
  geometry     string       WKT of the uploaded AOI.
  pk           integer      The primary key of the uploaded AOI.
  name         string       The name of the uploaded AOI.
  subscribed   boolean      Whether or not the user is subscribed to the AOI.

### Collect object

  Key                 Value Type       Value Description
  ------------------- ---------------- -------------------------------------------------------
  fields.name         string           The name of the collect.
  model               string           The model (e.g., loaddata.collect).
  pk                  integer          The primary key of the collect.
  collected\_at        timestamp        The time of the collection:  `YYYY-MM-DD HH24:MI:SS.FF6`
  classification      string           Classification (e.g., `UNCLASS`).
  sensor.name         string           The name of the sensor.
  dimensions          array of strings The dimensions in the data (e.g., ["X","Y","Z","I").
  resolution          real             The resolution of the collected data.
  point\_density       real             The number of points per square mile in the collect.
  geometry            string           WKT of the collect.
  area                real             Area of the collect (square miles).
  intersect\_geometry  string           WKT of the intersection of the collect and this AOI.
  intersect\_area      real             Area of the intersection (square miles).
  coverage\_ratio     real             Ratio of intersection area to AOI area (0 to 1).
  filesize            real             Estimated size (bytes).
  num\_points          real             Number of points.

### Export object

  Key          Value Type   Value Description
  ------------ ------------ -----------------------------------------------------------
  status       string       The status of the export (e.g., SUCCESS, FAILED, QUEUED).
  started\_at   timestamp    Time of creation for the AOI: `YYYY-MM-DD HH24:MI:SS.FF6`
  name         string       The name of the export.
  datatype     string       The datatype (e.g., LAS 1.2, DTM).
  hsrs         string       The Horizontal Spatial Reference System EPSG code.
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
