---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://app.blockdaemon.com/login'>Log In to BLOCKDAEMON</a>

search: true
---

# Introduction

Welcome to the Blockdaemon API!

# Authentication

> To authorize, use this code:

```shell
# With curl, you can just pass the correct header with each request
curl "'https://dev.api.blockdaemon.com/v1/logs?node=:id&protocol=:protocol'"
  -H "Authorization: Bearer TOKEN"
```

> Make sure to replace `TOKEN` with your API key, `NODEID` with the node xid, and `PROTOCOL` with the protocol string.

Blockdaemon currently uses the token assigned to you after login, stored in the local storage of your browser.

Blockdaemon expects the value of the token to be passed as a header:

`Authorization: Bearer TOKEN`

<aside class="notice">
You must replace <code>TOKEN</code> with the value of your authorization token.
</aside>

# Errors

The Blockdaemon API uses the following error codes:


Error Status Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your authorization token is invalid or expired.
403 | Forbidden -- The request is hidden for administrators only.
404 | Not Found -- The specified resource could not be found.
405 | Method Not Allowed -- An invalid method was used in the request.
406 | Not Acceptable -- You requested a format that isn't json.
410 | Gone -- A request can no longer be made to this endpoint.
429 | Too Many Requests -- Wait longer between request.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.

# Monitoring

## List Logs

```shell
curl "'https://dev.api.blockdaemon.com/v1/logs?node=:id&protocol=:protocol'"
  -H "Authorization: Bearer TOKEN"
```

> The above command returns JSON structured like this:

```json
{
  "data":
    {
      "logs":
        [
          {
            "info":
              {
                "nodeName":"My Node",
                "nodeXid":"blo12c345k67daem89o0n"
              },
            "message":"Hello World!"
          }
        ],
      "nextPageToken":"n3X7p4G370k3N"
    }
}
```

This endpoint retrieves logs for the node.

### HTTP Request

`GET https://dev.api.blockdaemon.com/v1/logs?node=:id&protocol=:protocol`

### Query Parameters

Parameter | Required |  Default | Description
--------- | -------- | ------- | -----------
protocol | yes | none | Protocol is the blockchain protocol, right now only XRP and HARMONY are valid.
node | yes |none | xid of the node can be obtained from front end by selecting Connect from the Actions dropdown and grabbing it from the URL
pageSize | no | 100 | Cannot exceed 499 results page size.
pageToken | no | none| Each page has returns a pageToken for the next page in the data.
