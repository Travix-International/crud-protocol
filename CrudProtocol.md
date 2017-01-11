# CRUD HTTP protocol

Although `ng-admin` supports mapping to different API implementations, by standardizing on a specific CRUD protocol we speed up the
implementation of new functionality, as well as standardize the experience for the end-user.

## Operations

The following operations MUST be implemented:

* Get a list of all entities. Arguments:
    - Paging SHOULD be implemented
    - Filtering MAY be implemented
    - Sorting MAY be implemented

The following operations MAY be implemented (depending on your use case):

* Get a specific entity by ID
* Add a new entity
* Update an entity
* Delete an entity
If add or update is implemented, then 'get by id' MUST be implemented as well.

Beyond this, custom operations MAY be implemented as seen fit. This may be needed when the problem domain involves
complex entity relations other other requirements.

Entities being returned SHOULD by default return a column `id`, acting as the unique ID of the record.
This may not always be possible, hence this is not a MUST - at the expense of a more complex implementation
if `id` is not available. Compound keys are not supported.

# Status code
Each operation has a set of supported HTTP status codes. They are the typical ones, such as 200 (OK),
5xx (server error), 404 (Not found), 409 (Conflict), etc.

## Error handling
For certain response codes, an error structure MUST be returned. This allows the UI to display more meaningful messages
to the end user to understand what is going on. For example, a 400 (Bad request) being returned due to a validation
issue, SHOULD tell the user what did not pass validation.

## Per-operation documentation

### Description of common models

These models are used repeatedly in the various operations.

#### Error

|Field|Type|Description|
|-|-|-|
|message|string|Textual description of the error

#### Dataset

|Field|Type|Description|
|-|-|-|
|items|array|Array of the type of entity being queried|
|pagingInfo|PagingInfo|Information about the page being viewed|

#### PagingInfo

|Field|Type|Description|
|-|-|-|
|supportsPaging|bool|Indication if paging is supported by this list command|
|pageSize|int|Amount of items per page|
|pageNumber|int|Page to request. 1-based|
|doesKnowTotalRecords|bool|Whether the total record count is known and returned|
|totalRecordCount|int|Total amount of records. Can be 0 if paging is not supported|


### Get List

* Purpose: get a list of entities, optionally with sorting, filtering and paging.
* Mandatory to implement: yes

#### Request

* Method: GET
* Route: api_url/{resourceName}/{id}

#### Response

|HTTP Status|Type in body|Meaning|
|-:|-|-|
|200|Dataset|All is ok, here's the requested data|
|400|Error|Request is understood, but invalid|
|500|Error|Error when processing the request


### Get by ID

* Purpose: get a specific entity by its ID
* Mandatory to implement: no, return HTTP 405 if not implemented

#### Request

* Method: GET
* Route: api_url/{resourceName}
* URL arguments

|Field|Type|Description|
|-|-|-|
|pageSize|int|Amount of items per page|
|pageNumber|int|Page to request. 1-based|
|sortColumn|string|Column to sort by|
|sortDirection|string|(['Asc', 'Desc'], default 'Asc'): sort direction
|filter|string|field to sort on (default: '')

* URL argument restrictions
  - `pageSize` and `pageNumber` are only mandatory if the API supports paging
  - sortColumn / direction is only mandatory if the API does support sorting
  - filter is only mandatory if the API does support filtering

#### Response

|HTTP Status|Type in body|Meaning|
|-:|-|-|
|200|Dataset|Ok, entity found|
|400|Error|Request is understood, but invalid|
|404|_(none)_|Entity does not exist (anymore)|
|405|_(none)_|Operation not supported on this resource|
|500|Error|Error when processing the request|


### Add
`// todo`
### Update
`// todo`
### Delete
`// todo`
