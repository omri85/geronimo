Geronimo Search public user guide

# Welcome to Geronimo Search

## Usage guide:
### Before you start:

Make sure you have your *userKey* and your *code*
* **userKey** - unique key per user. The name of the index to search
* **code** - authentication key. Allows access to Geronimo API.

Both of those values must be query parameters in any API call.

### Setup your index:
#### Option 1: 2 steps - first storing then indexing:
##### Step 1 - upload your jsons:
First you need to upload your documents. Your docuemnts will not be indexed yet, but will be pedning mode.

Endpoint:
/POST http://www.geronimosearch.com/api/*userKey*/*index*/_store

Payload: a json to store.

Example: http://www.geronimosearch.com/api/myUserKey/recipes/_store?code=my-code

Payload:
{
  "name": "Alice's Adventures in Wonderland",
  "author":  "Lewis Carroll"
}

Pricing: 0.1351$ per 1,000 calls.

##### Step 2 - index the documents:
After you're done uploading all the documents you want to store you should index them. After this operation, all the documents will be available for search.

Endpoing:
/GET http://www.geronimosearch.com/api/*userKey*/*index*/_index

Payload: an array of jsons to store.

Example: /GET http://www.geronimosearch.com/api/myUserKey/recipes/_index?code=my-code

Pricing: 0.05$ per call

#### Option 2: Bulk indexing - immediate indexing without storing first:
Get all your documents ready in a json array and send them together

Endpoing:
/POST http://www.geronimosearch.com/api/*userKey*/*index*/_bindex

Example: /POST http://www.geronimosearch.com/api/myUserKey/recipes/_bindex?code=my-code

Payload:
[
    {
        "name": "Alice's Adventures in Wonderland",
        "author":  "Lewis Carroll"
    },
    {
        "name": "1984",
        "author":  "George Orwell",
        "year": 1948
    }
]

Pricing: 0.10$ per call

### Search
Now the index is ready and you can search using the *search* API:

/POST http://www.geronimosearch.com/api/*userKey*/_search

Body params:
* "field" [string] - the json field you want to query. (mandatory)
* "output" [string] - comma saperated list of the json field names to retrieve (mandatory)
* "term" [string] - the term you want to look up (mandatory)
* "indices" [string] - comma saperated list of indices to search in (mandatory)
* "limit" [int] - limit the number of results (optional, default=10, max=100)
* "isRegex" [boolean] - true if the term is a regular expression (optional, default=false)

Example:

https://ctrl-functions-20190430173935078.azurewebsites.net/api/myUserKey/_search?code=mycode

Payload:
{
  "field": "name",
  "author": "lewis",
  "indices": "main,myindex"
  "limit": 1,
  "isRegex": false,
  "output": "name,author"
}

Pricing:  0.087$ per 1,000 calls.
