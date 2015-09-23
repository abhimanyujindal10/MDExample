# MDExample
# C2C AWS API GATEWAY REST CLIENT

The C2C AWS API Gateway Rest Client for JavaScript allows developers to build libraries or applications that make use of [AWS API GATEWAY REST API](https://docs.aws.amazon.com/apigateway/api-reference/).


## Installing with npm

C2C AWS API Gateway Rest Client is currently present on private npm repository(http://packages.c2c.local:8080/) of C2C. You need to set registry path for the this npm repostitory. After this you can install this REST client by simply typing the following into a terminal window:

```sh
npm install c2cs-aag-client
```


## Loading the module

After you've installed the module, you can require this module in your node application using require():

```js
var Aag = require("c2cs-aag-client");
```


## Example

```js
var Aag = require("c2cs-aag-client");

// Load AWS Settings
var aagConfig = {
	accessKeyId		: process.env.AWS_ACCESS_KEY 	|| "xxxxxxx..........",
	secretAccessKey	: process.env.AWS_SECRET_KEY 	|| "xxxxxxx..........",
	region			: process.env.AWS_REGION 		|| "xx..."
};

var apiId = "xxxxx...";
var limit = 50;

Aag.getApiResources( apiID, limit ).then(function(res){
	console.log("Success");
	console.log(res);
}, function(err){
	console.log("Error");
	console.log(err);
});

```

## Functions Reference

### createApi( requestData ) 

To create new API

API method name 	: {restapi:create}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/restapi-create/
HTTP Request 		: POST /restapis

**Parameters**

**requestData**: `object`

**Returns**: `function`, promise

**Example**:
```js
//requestData sample
var requestData = { "name" : "test", "description" : "test desc" };

//call
createApi( requestData ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### createResource( requestData, parentId ) 

To create new resource in API

API method name 	: {resource:create}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/resource-create/
HTTP Request 		: POST /restapis/<restapi_id>/resources/<parent_id>

**Parameters**

**requestData**: `object`

**parentId**: `string`

**Returns**: `function`, promise

**Example**:
```js
//requestData sample
var requestData = { "pathPart" : "test" };

//call
createResource( requestData, parentId ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### getApiResources( apiId, limit ) 

To get all resources of API

API method name 	: {restapi:resources}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/restapi-resources/
HTTP Request 		: GET /restapis/<restapi_id>/resources{?limit,embed}

**Parameters**

**apiId**: `string`

**limit**: `integer`

**Returns**: `function`, promise

**Example**:
```js
//call
getApiResources( apiId, limit ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### getApiResourceById( resourceId )

To get all resources of API

API method name 	: {resource:by-id}
API method link 	: https://docs.aws.amazon.com/apigateway/api-reference/link-relation/resource-by-id/
HTTP Request 		: GET /restapis/<restapi_id>/resources/{resource_id}{?embed}

**Parameters**

**resourceId**: `string`

**Returns**: `function`, promise

**Example**:
```js
//call
getApiResourceById( resourceId ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### getApiResourceMethod( resourceId, httpMethod )

To get method of resource

API method name 	: {resource:methods}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/resource-methods/
HTTP Request 	: GET /restapis/<restapi_id>/resources/<resource_id>/methods/<http_method>

**Parameters**

**resourceId**: `string`

**httpMethod**: `string`

**Returns**: `function`, promise

**Example**:
```js
//call
getApiResourceById( resourceId, httpMethod ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### createResourceMethod( requestMethod, requestData, resourceId ) 

Create method for a resource

API method name 	: {method:put}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/method-put/
HTTP Request 		: PUT /restapis/<restapi_id>/resources/<resource_id>/methods/{http_method}

**Parameters**

**requestMethod**: `string`

**requestData**: `object`

**resourceId**: `string`

**Returns**: `function`, promise

**Example**:
```js
//requestData sample
var requestData = {
	"authorizationType" : "NONE",
	"requestParameters" : {}
};

//call
createResourceMethod( requestMethod, requestData, resourceId ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```

### updateMethodRequest( requestMethod, requestData, resourceId ) 

Update resource method for queryStrings or headers 

API method name 	: {method:update}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/method-update/
HTTP Request 		: PATCH /restapis/<restapi_id>/resources/<resource_id>/methods/<http_method>

**Parameters**

**requestMethod**: `string`

**requestData**: `object`

**resourceId**: `string`

**Returns**: `function`, promise

**Example**:
```js
//requestData Sample : 
//{"patchOperations":[{"op":"add","path":"/requestParameters/method.request.querystring.year"}]}
//{"patchOperations":[{"op":"add","path":"/requestParameters/method.request.header.test"}]}
//{"patchOperations":[{"op":"remove","path":"/requestParameters/method.request.header.test"}]}
var requestData = {"patchOperations":[{"op":"remove","path":"/requestParameters/method.request.header.test"}]};

//call
updateMethodRequest( requestMethod, requestData, resourceId ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```

### updateMethodIntegration( requestMethod, requestData, resourceId ) 

Update integration request for queryStrings or headers 

API method name 	: {integration:update}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/integration-update/
HTTP Request 		: PATCH /restapis/<restapi_id>/resources/<resource_id>/methods/<http_method>/integration

**Parameters**

**requestMethod**: `string`

**requestData**: `object`

**resourceId**: `string`

**Returns**: `function`, promise

**Example**:
```js
//requestData sample
var requestData = {"patchOperations":[{"op":"add","path":"/requestParameters/integration.request.querystring.param_test","value":"method.request.querystring.test"}]};

//call
updateMethodIntegration( requestMethod, requestData, resourceId ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### attachMethodResponseModel( requestMethod, modelName, resourceId, httpCode ) 

To attach response model for method

API method name 	: {methodresponse:put}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/method-put/
HTTP Request 		: PUT /restapis/<restapi_id>/resources/<resource_id>/methods/<http_method>/responses/{status_code}

**Parameters**

**requestMethod**: `string`

**modelName**: `string`

**resourceId**: `string`

**httpCode**: `string`

**Returns**: `function`, promise

**Example**:
```js
//call
attachMethodResponseModel( requestMethod, modelName, resourceId, httpCode ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### addMethodIntegration( requestMethod, requestData, resourceId ) 

To add method integration

API method name 	: {integration:put}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/integration-put/
HTTP Request 		: PUT /restapis/<restapi_id>/resources/<resource_id>/methods/<http_method>/integration

**Parameters**

**requestMethod**: `string`

**requestData**: `object`

**resourceId**: `string`

**Returns**: `function`, promise

**Example**:
```js
//call
addMethodIntegration( requestMethod, requestData, resourceId ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### attachIntegrationResponseModel( requestMethod, resourceId, httpCode ) 

To attach integration reponse model for method

API method name 	: {integrationresponse:put}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/integrationresponse-put/
HTTP Request 		: PUT /restapis/<restapi_id>/resources/<resource_id>/methods/<http_method>/integration/responses/{status_code}

**Parameters**

**requestMethod**: `string`

**resourceId**: `string`

**httpCode**: `string`

**Returns**: `function`, promise

**Example**:
```js
//call
attachIntegrationResponseModel( requestMethod, resourceId, httpCode ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### attachIntegrationRequestTemplate( requestMethod, resourceId, mapTemplate ) 

To attach integration request template for method

API method name 	: {integration:update}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/integration-update/
HTTP Request 		: PATCH /restapis/<restapi_id>/resources/<resource_id>/methods/<http_method>/integration

**Parameters**

**requestMethod**: `string`

**resourceId**: `string`

**mapTemplate**: `string`

**Returns**: `function`, promise

**Example**:
```js
//call
attachIntegrationRequestTemplate( requestMethod, resourceId, mapTemplate ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### attachIntegrationResponseTemplate( requestMethod, resourceId, mapTemplate, httpcode ) 

To attach integration response template for method

API method name 	: {integrationresponse:update}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/integrationresponse-update/
HTTP Request 		: PATCH /restapis/<restapi_id>/resources/<resource_id>/methods/<http_method>/integration/responses/<status_code>

**Parameters**

**requestMethod**: `string`

**resourceId**: `string`

**mapTemplate**: `string`

**httpcode**: `string`

**Returns**: `function`, promise

**Example**:
```js
//call
attachIntegrationResponseTemplate( requestMethod, resourceId, mapTemplate, httpcode ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### addEmptyRequestMappingTemplate( requestMethod, resourceId ) 

To add empty request template with name `application/json`

API method name 	: {integration:update}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/integration-update/
HTTP Request 		: PATCH /restapis/<restapi_id>/resources/<resource_id>/methods/<http_method>/integration

**Parameters**

**requestMethod**: `string`

**resourceId**: `string`

**Returns**: `function`, promise

**Example**:
```js
//call
addEmptyRequestMappingTemplate( requestMethod, resourceId ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### addEmptyResponseMappingTemplate( requestMethod, resourceId, httpCode ) 

To add empty response template with name `application/json`

API method name 	: {integrationresponse:update}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/integrationresponse-update/
HTTP Request 		: PATCH /restapis/<restapi_id>/resources/<resource_id>/methods/<http_method>/integration/responses/<status_code>

**Parameters**

**requestMethod**: `string`

**resourceId**: `string`

**httpCode**: `string`

**Returns**: `function`, promise

**Example**:
```js
//call
addEmptyResponseMappingTemplate( requestMethod, resourceId, httpCode ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### addApiKeyValidation( requestMethod, resourceId, flag ) 

To add api key validation for method

API method name 	: {method:update}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/method-update/
HTTP Request 		: PATCH /restapis/<restapi_id>/resources/<resource_id>/methods/<http_method>

**Parameters**

**requestMethod**: `string`

**resourceId**: `string`

**flag**: `string`

**Returns**: `function`, promise

**Example**:
```js
//call
addApiKeyValidation( requestMethod, resourceId, flag ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### generateModelTemplate( modelname ) 

To generate template of model

API method name 	: {model:generate-template}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/model-generate-template/
HTTP Request 		: GET /restapis/<restapi_id>/models/<model_name>/default_template

**Parameters**

**modelname**: `string`

**Returns**: `function`, promise

**Example**:
```js
//call
generateModelTemplate( modelname ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### createModel( modelName, modelDesc, modelSchema, modelContentType ) 

Creates a new Model for an API.

API method name 	: {model:create}
API method link 	: https://docs.aws.amazon.com/apigateway/api-reference/link-relation/model-create/
HTTP Request 		: POST /restapis/<restapi_id>/models

**Parameters**

**modelName**: `string`

**modelDesc**: `string`

**modelSchema**: `object`

**modelContentType**: `string`, (default = "application/json")

**Returns**: `function`, promise

**Example**:
```js
//call
createModel( modelName, modelDesc, modelSchema, modelContentType ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```

### updateModel( modelName, modelSchema )

Changes information about a model.
 
API method name 	: {model:update}
API method link 	: https://docs.aws.amazon.com/apigateway/api-reference/link-relation/model-update/
HTTP Request 		: PATCH /restapis/<restapi_id>/models/<model_name>

**Parameters**

**modelName**: `string`

**modelSchema**: `object`

**Returns**: `function`, promise

**Example**:
```js
//call
updateModel( modelName, modelSchema ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```

### getModelByName( modelName ) 

Gets information about the Model with the specified name.

API method name 	: {model:by-name}
API method link 	: https://docs.aws.amazon.com/apigateway/api-reference/link-relation/model-by-name/
HTTP Request 		: GET /restapis/<restapi_id>/models/{model_name}{?flatten}

**Parameters**

**modelName**: `string`

**Returns**: `function`, promise

**Example**:
```js
//call
getModelByName( modelName ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### deleteModel( modelName )

Deletes a model.

API method name 	: {model:delete}
API method link 	: https://docs.aws.amazon.com/apigateway/api-reference/link-relation/model-delete/
HTTP Request 		: DELETE /restapis/<restapi_id>/models/<model_name>

**Parameters**

**modelName**: `string`

**Returns**: `function`, promise

**Example**:
```js
//call
deleteModel( modelName ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### deleteResource( resourceId ) 

Deletes a resource.

API method name 	: {resource:delete}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/resource-delete/
HTTP Request 		: DELETE /restapis/<restapi_id>/resources/<resource_id>

**Parameters**

**resourceId**: `string`

**Returns**: `function`, promise

**Example**:
```js
//call
deleteResource( resourceId ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### deleteResourceMethod( resourceId, httpMethod )

A delete resource method.

API method name 	: {method:delete}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/method-delete/
HTTP Request 	: DELETE /restapis/<restapi_id>/resources/<resource_id>/methods/<http_method>

**Parameters**

**resourceId**: `string`

**httpMethod**: `string`

**Returns**: `function`, promise

**Example**:
```js
//call
deleteResourceMethod( resourceId, httpMethod ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### createDeployment( stageName, stageDescription, description, cacheClusterEnabled, cacheClusterSize ) 

Creates a Deployment for the API.

API method name 	: {deployment:create}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/deployment-create/
HTTP Request 		: POST /restapis/<restapi_id>/deployments

**Parameters**

**stageName**: `string`

**stageDescription**: `string`

**description**: `string`

**cacheClusterEnabled**: `string`

**cacheClusterSize**: `boolean`

**Returns**: `function`, promise

**Example**:
```js
//call
createDeployment( stageName, stageDescription, description, cacheClusterEnabled, cacheClusterSize ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```


### getStageByName( stageName ) 

Gets information about a Stage resource for a given name.

API method name 	: {stage:by-name}
API method link 	: http://docs.aws.amazon.com/apigateway/api-reference/link-relation/stage-by-name/
HTTP Request 		: GET /restapis/<restapi_id>/stages/{stage_name}

**Parameters**

**stageName**: `string`

**Returns**: `function`, promise

**Example**:
```js
//call
getStageByName( stageName ).then( function(res) {
	console.log(res);
}).catch( function (err) {
	console.log(err);
});
```
