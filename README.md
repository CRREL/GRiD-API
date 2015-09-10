I've written these up in Pandoc markdown, which is easily converted to GitHub Flavored Markdown, strict markdown, reStructuredText, HTML, PDF, Microsoft Word, etc.

For example,

```
pandoc endpoints.md objects.md -o api.html --highlight-style tango -s
```

I'll work on making sure the stuff below is ported into api.md or objects.md as appropriate.

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
