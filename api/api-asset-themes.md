---
title: Assets
last_updated: June 8, 2016
sidebar: api_sidebar
permalink: /api-asset-themes/
---

## Asset Themes

The asset themes endpoint will return a list of themes for the asset based on the specified {identifier} value. 

```
GET /assets/{identifier}/themes/
```

### Example request/response
JSON Response

```
GET https://api.knows.is/assets/$ARMH/themes/
Accept: application/json, text/javascript
```

```
{
  "name": "ARM Holdings PLC",
  "identifier": "$ARMH",
  "startdate": "2013-01-01T00:00:00Z",
  "enddate": "2013-01-01T00:00:00Z",
  "dailythemes": [
    {
      "date": "2013-01-01T00:00:00Z",
      "themes": [
        {
          "title": "The title of the theme"
        }
      ]
    },
    {
      "date": "2013-01-02T00:00:00Z",
      "themes": [
        {
          "title": "The title of the first theme"
        },
        {
          "title": "The title of the next theme"
        }
      ]
    }
  ]
}
```



