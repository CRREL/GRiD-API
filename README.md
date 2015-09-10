I've written these up in Pandoc markdown, which is easily converted to GitHub Flavored Markdown, strict markdown, reStructuredText, HTML, PDF, Microsoft Word, etc.

For example,

```
pandoc endpoints.md objects.md -o api.html --highlight-style tango -s
```

I'll work on making sure the stuff below is ported into api.md or objects.md as appropriate.

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
