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
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/export/?geom=POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))
~~~~

~~~~ {.json}
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
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/export/add/?name=test&geom=POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))&subscribe=True
~~~~

~~~~ {.json}
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
curl -u <username> http://gridte.rsgis.erdc.dren.mil/te_ba/api/export/geoname/?geom=POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))
~~~~

~~~~ {.json}
{
  "name": "Some Place",
  "provided_geometry": "POLYGON ((30 10, 40 40, 20 40, 10 20, 30 10))"
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

  Query parameter    Value
  ------------------ --------------------------------------------------------------
  collects           *Required*. A list of collection IDs to include in the export.

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