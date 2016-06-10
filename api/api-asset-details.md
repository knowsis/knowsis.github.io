---
title: Assets
last_updated: June 8, 2016
sidebar: api_sidebar
permalink: /api-asset-details/
---


The asset endpoint will return a single asset based on the specified {identifier} value. 

```
GET /assets/{identifier}/
```

## Example request/response

JSON Response

```
GET https://api.knows.is/assets/ARM.L/
Accept: application/json, text/javascript
```

```
{
  "name": "ARM Holdings PLC",
  "identifiers": [
    {
      "identifier": "ARM:LN",
      "type": "Bloomberg"
    },
    {
      "identifier": "ARMH:US",
      "type": "Bloomberg"
    }
  ]
}
```



