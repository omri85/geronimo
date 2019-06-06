Geronimo Search public user guide

# Welcome to Geronimo Search

## Usage guide:
### Before you start:

Make sure you have your *userKey* and your *code*
* **userKey** - unique key per user. The name of the index to search
* **code** - authentication key. Allows access to Geronimo API.

Both of those values must be query parameters in any API call.

### Setup your index in 2 simple steps:
#### Step 1 - upload your jsons:
First you need to upload your documents. Your docuemnts will not be indexed yet, but will be pedning mode.

Endpoint:
/POST https://ctrlf-general.azurewebsites.net/api/StoreDocument

Payload: the json to store.

Example: https://ctrlf-general.azurewebsites.net/api/StoreDocument?code=my-code&userKey=myuser

Payload:
{
  "name": "Alice's Adventures in Wonderland",
  "author":  "Lewis Carroll"
}

Pricing: 0.1351$ per 1,000 calls.

#### Step 2 - index the documents:
After you're done uploading all the documents you want to store you should index them. After this operation, all the documents will be available for search.

Endpoing:
/GET https://ctrl-functions-20190430173935078.azurewebsites.net/api/IndexDocument

Example: /GET https://ctrl-functions-20190430173935078.azurewebsites.net/api/IndexDocument?code=mycode&userKey=myuser

Pricing: 0.05$ per call

### Search
Now the index is ready and you can search using the *search* API:

/POST https://ctrl-functions-20190430173935078.azurewebsites.net/api/Search

Body params:
* "field" [string] - the json field you want to query. (mandatory)
* "term" [string] - the term you want to look up (mandatory)
* "limit" [int] - limit the number of results (optional, default=10, max=100)
* "isRegex" [boolean] - true if the term is a regular expression (optional, default=false)

Example:

https://ctrl-functions-20190430173935078.azurewebsites.net/api/Search?code=mycode&userKey=myuser

Payload:
{
  "field": "name",
  "author": "lewis",
  "limit": 1,
  "isRegex": false
}

Pricing:  0.087$ per 1,000 calls.
