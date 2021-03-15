The GRiD API v3 is documented in [swagger.v3.yaml](swagger.v3.yaml).

GRiD also provides a WFS endpoint for querying point cloud and raster data.
This is documented in [wfs.rst](wfs.rst).

Import the Swagger files into Postman using
[these](https://www.getpostman.com/docs/importing_swagger) instructions.

Or, head over to the [Swagger UI demo](http://petstore.swagger.io/) and paste
the [this
link](https://raw.githubusercontent.com/CRREL/GRiD-API/master/swagger.v3.yaml)
into the bar at the top of the screen. You can also explore the document by
importing it into the [Swagger Editor demo](http://editor.swagger.io/#/) - just
use the [same
link](https://raw.githubusercontent.com/CRREL/GRiD-API/master/swagger.v3.yaml)
to the Swagger YAML.

# Transition to OAS 3.0 and Automated Testing

The file [oas-3.0.yaml](oas-3.0.yaml) contains a version of the Swagger 2.0
spec for GRiD API v3 that was first converted to OpenAPI 3.0 (OAS 3.0) by
https://editor.swagger.io and has been further modified manually in Postman. It
should serve as a draft representation of the GRiD API v3 spec represented in
OAS 3.0.

The file
[grid-v3-oas-3.0-test-collection.json](grid-v3-oas-3.0-test-collection.json) is
a Postman Collection (in Collection format v2.1) that can be imported into both
Postman and Katalon (Katalon must be setup as a Web Service project for this to
work). The Collection was first created by importing the OAS 3.0 schema into
Postman and allowing Postman to automatically create the Collection. As such,
every documented endpoint at the time of creation has a corresponding request
in the Collection. Requests have since been manually reorganized into asset
lifecycles, e.g., first create and AOI, then get AOI details, edit the AOI, and
finally delete the AOI.

Collections can be run as a group (rather than making individual requests).
Upon completion, a report is presented that summarizes all passing and failing
tests. Each Collection run can be linked with an execution environment (in fact
an environment choice is always required!). This makes switching between
testgrid and production as simple as changing the environment. Environments
need only specify the `baseUrl`, e.g., https://grid.nga.mil/grid/api/v3 for
production GRiD, and `access_token` which is established through the GRiD UI
for the corresponding GRiD instance. We could extend the Collection to work
through the full OAuth 2.0 workflow, but leave this for future work.

## OAS 3.0 schema validation

Note that Postman will validate a collection against a linked OAS 3.0 API in
the desktop version (support added with
https://github.com/postmanlabs/postman-app-support/issues/6614). Issues in
which the responses do not validate will be raised with individual requests.

A separate ticket is open, with no ETA as of November 2020, to be able to write
tests that validate against an OAS 3.0 schema
(https://github.com/postmanlabs/postman-app-support/issues/8920). As such, it
is not really possible to validate requests/responses as part of an automated
CI/CD process.
