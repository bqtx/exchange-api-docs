# Exchange API Docs

The project contains files composing OpenAPI (former Swagger) file specification describing [exchange-public](https://ci.tux.it/bqtx/exchange-services/tree/master/exchange-public) endpoints.

To be able to work with multiple files (and contain main file dimensions) a specific worflow is need to be adopted in order to be able to work on the project.

## Edit file locally

In order to be able to see generated UI you need to serve the project to the online editor. (There is a Preview Swagger extension for VsCode too, but it doesn't seems to work pretty weel)

You can use both online hosted editor or run it yourself downloading the project or serving it with docker, check [swagger-editor](https://github.com/swagger-api/swagger-editor).
The easiest way is to use the online swagger editor tool.

First you need to serve the project through a web server enabling cors requests.

Install http-server:

> npm i -g http-server

Launch http-server:

> http-server --cors . -c0

Now navigate to `http://editor.swagger.io/?url=http://localhost:8080/openapi.yaml` and you will be able to see the openapi.yaml file in your editor. Editing through the editor WON'T edit the file locally, so use the editor just for check the final output. The easiest error to check whether the are some compilation error is to use `swagger-cli` validate command:

> swagger-cli validate openapi.yaml

## Generate bundle file

An output json format file containing all files bundles together can be generated using `swagger-cli`

Install cli:

> npm install --global swagger-cli

Generate file:

> swagger-cli bundle --outfile openapi.json -r openapi.yaml

## Project structure

The root of the project is the openapi.yaml file from which the output is generated. The openapi file is written following openapi 3.0.0 standard, taking advantage of file splitting.

### paths

Paths contains endpoints divided by context (second element in path, after /api). Paths containing path parameters are not included in path files due to a bug in swagger editor compilation that required path parameter to be declared in root file.

### models

Models contains reusable database models structure (currently just MongoDB documents).

### bodies

Bodeis contains reused body requests for paths and extended bodies from models.

### responses

Responses contains reusable response object for paths

common.yaml files contains reusable common fields.
