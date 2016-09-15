I've written these up in Pandoc markdown, which is easily converted to GitHub Flavored Markdown, strict markdown, reStructuredText, HTML, PDF, Microsoft Word, etc.

For example,

```
pandoc endpoints.md objects.md -o v#_api_details.html --css /gridvm1/static/css/grid-api.css --highlight-style tango -s
pandoc endpoints.md objects.md -s -t rst -o composed_api.rst
```
