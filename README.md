1. AOI List  
  * Description: Returns a JSON list of all AOIs for the requesting user, AOI list can be filtered based on the passing of a geom parameter as a selection area.  
  * Example: /api/export/?geom=POLYGON ((68.9150709532930961 33.5950250284996983, 68.8704389952918063 33.5955969812235011, 68.8724989318148033 33.5858732691386024, 68.9020246886466055 33.5853012519442018, 68.9068312072003977 33.5549789148388982, 68.9274305724316037 33.5589843621810999, 68.9274305724316037 33.5944530719840984, 68.9150709532930961 33.5950250284996983))
2. AOI Details  
  * Description: Returns JSON formatted details for a given AOI based on a provided pk.
  * Example: /api/export/100/
  * Options: 
    - datatype: Used to filter the collects returned on the given type. Accepts 'pointcloud' or 'raster'. String.  If not given collects with all types will be returned.
   * Example: /api/export/100/?datatype=pointcloud
3. AOI Add
  * Description: Allows for creation of an AOI with the passing of name and geom parameters.  Also allows for subscription to a new AOI by passing a subscribe parameter.  Subscribe parameter can distinguish between True, False, T, F, 1, and 0.  Default is false, but all other provided values will be assumed to be a value of True.  
  * Example: /api/export/add/?name=test&geom=POLYGON ((68.9150709532930961 33.5950250284996983, 68.8704389952918063 33.5955969812235011, 68.8724989318148033 33.5858732691386024, 68.9020246886466055 33.5853012519442018, 68.9068312072003977 33.5549789148388982, 68.9274305724316037 33.5589843621810999, 68.9274305724316037 33.5944530719840984, 68.9150709532930961 33.5950250284996983))&subscribe=True
4. Export Details  
  * Description: Returns JSON formatted details for a given export based on a provided pk.
  * Example: /api/export/export/100/
5. Geoname Lookup  
  * Description: Allows for a geoname lookup based on a passed geom parameter
  * Example: /api/export/geoname/?geom=POLYGON ((68.9150709532930961 33.5950250284996983, 68.8704389952918063 33.5955969812235011, 68.8724989318148033 33.5858732691386024, 68.9020246886466055 33.5853012519442018, 68.9068312072003977 33.5549789148388982, 68.9274305724316037 33.5589843621810999, 68.9274305724316037 33.5944530719840984, 68.9150709532930961 33.5950250284996983))
6. Task Details
  * Description: Returns a JSON version of the task status/details of a provided task_id
  * Example: /api/export/task/bacb736e-e900-457c-9b24-fd409bc3019d/
7. Pointcloud Export
  * Description: Allows for initiation of pointcloud exports via an url call with a provided AOI pk and the pks of the collects to be included. Multiple collect pks can be used, if separated by a '+' or ','.  Additional options may also be included.  Options not passed will use default values for exporting.
  * Example: /api/export/aoi/101/generate/pointcloud/?collects=100+102
  * Options:
    - hsrs: Accepts an EPSG code.  Integer.  Defaults to AOI SRS.
    - intensity: Boolean.  Defaults to True.
    - dim_classification: Boolean.  Defaults to True.
    - file_export_options: Used to determine file merging strategy. Accepts 'individual', 'collect', and 'super'.  String.  Defaults to 'individual'
    - compressed: Boolean.  Defaults to True.
    - send_email: Boolean.  Defaults to False.
    - generate_dem: Used to trigger a DEM from pointcloud export.  Boolean. Defaults to False.
    - cell_spacing: Used together with generate_dem.  Float.  Defaults to 1 with generate_dem otherwise defaults to None.
    - pcl_terrain: Used to trigger a PMF Bare Earth export, accepts the terrain 'urban', 'suburban', 'mountainous', and 'foliated'.  String.  Defaults to None.
    - sri_hres: Used to trigger a Sarnoff Bare Earth export, accepts the hres.  Decimal.  Defaults to None.
  * Example: /api/export/aoi/101/generate/pointcloud/?collects=100+102&send_email=True&file_export_options=collect
8. Raster Export
  * Description: Allows for initiation of raster exports via an url call with a provided AOI pk and the pks of the collects to be included. Multiple collect pks can be used, if separated by a '+' or ','.  Additional options may also be included.  Options not passed will use default values for exporting.
  * Example: /api/export/aoi/101/generate/raster/?collects=100+102
  * Options:
    - hsrs: Accepts an EPSG code.  Integer.  Defaults to AOI SRS.
    - file_export_options: Used to determine file merging strategy. Accepts 'individual' and 'collect'.  String.  Defaults to 'individual'
    - file_format_options: Used to determine file merging strategy. Accepts 'GTiff' and 'NITF'.  String.  Defaults to 'GTiff'
    - compressed: Boolean.  Defaults to True.
    - send_email: Boolean.  Defaults to False.
  * Example: /api/export/aoi/101/generate/raster/?collects=100+102&send_email=True&file_export_options=collect
  
