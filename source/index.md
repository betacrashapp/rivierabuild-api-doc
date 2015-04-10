---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='#'>Sign Up for an API Key</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Riviera Build API! You can use our API to access Riviera Build API endpoints, which can get information on the application you have access to, builds uploaded, even upload builds!

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "https://apps.rivierabuild.com/api/applications"
  -H "api-key: your-api-key"
```

> Make sure to replace `your-api-key` with your API key.

Riviera Build uses API keys to allow access to the API. You can get your Riviera Build API key in the [settings section](https://apps.rivierabuild.com/settings).

Riviera Build expects for the API key to be included in all API requests to the server in a header that looks like the following:

`api-key: your-api-key`

<aside class="notice">
You must replace `your-api-key` with your personal API key.
</aside>

# Applications

## Get All applications

```shell
curl "https://apps.rivierabuild.com/api/applications"
  -H "api-key: your-api-key"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id":1,
    "user_id":1,
    "name":"Crazy App",
    "logo_url":"https://example.com/image.png"
    },
    {
      "id":2,
      "user_id":1,
      "name":"Simple App",
      "logo_url":"https://example.com/image.png"
    }
]
```

This endpoint retrieves all applications.

### HTTP Request

`GET https://apps.rivierabuild.com/api/applications`


## Create an application

```shell
curl -XPOST "https://apps.rivierabuild.com/api/applications"
  -H "api-key: your-api-key"
  -F application[name]="Example App"
  -F file=@"/path/to/the/image/to/upload"
```

> The above command returns JSON structured like this:

```json
{
  "id":2,
  "user_id":1,
  "name":"Example App",
  "logo_url":"https://example.com/image.png"
}
```

This endpoint creates an application.

### HTTP Request

`POST https://apps.rivierabuild.com/api/applications`

### Parameters

Parameter | Description
--------- | -----------
application[name] | Name of the application
file | Logo image file, as part of the the POST body (Optional)


## Delete an application

```shell
curl -XDELETE "https://apps.rivierabuild.com/api/applications/1"
  -H "api-key: your-api-key"
```

> The above command returns JSON structured like this:

```json
{
  "result":"deleted"
}
```

This endpoint deletes an application.

### HTTP Request

`DELETE https://apps.rivierabuild.com/api/applications/<ID>`

### Parameters

Parameter | Description
--------- | -----------
ID | Application ID


#Builds
## Upload a build

```shell
curl -XPOST "https://apps.rivierabuild.com/api/upload"
  -H "api-key: your-api-key"
  -F file=@"/path/to/ipa/file"
  -F availability="1_week"
  -F passcode="secretpassword"
  -F app_id="1"
  -F commit_sha="ewtotj4535ogjropgjerotj3"
  -F note="This build is awesome!"
```

> The above command returns JSON structured like this:

```json
{
  "success":true,
  "file_url":"https://apps.rivierabuild.com/get/dovjek"
}
```

This endpoint uploads a build to Riviera Build.

### HTTP Request

`POST https://apps.rivierabuild.com/api/upload`

### Parameters

Parameter | Description
--------- | -----------
file | IPA of APK file to upload
availability | Determines for how long the build will be available
passcode | Optional password that would be required to install the build
app_id | Optional application ID that you want to associate your build to
commit_sha | Optional Commit SHA associated to this build
note | Optional release note. Support Markdown.
