---
title: Asset Details
last_updated: June 8, 2016
sidebar: api_sidebar
permalink: /api-asset-details/
---


The asset endpoint will return a single [asset object](/api-objects/#asset-object) based on the specified {identifier} value. 

```
GET /assets/{identifier}/
```

## Example request/response

```
GET https://api.knows.is/assets/$MSFT/
Accept: application/json, text/javascript
```

```
{
  
  "name": "Microsoft Corporation",
  "identifier": "microsoft-corporation",
  "identifiers": [
    {
      "identifier": "MSFT",
      "type": "Yahoo"
    },
    {
      "identifier": "$MSFT",
      "type": "Cashtag"
    },
    {
      "identifier": "MSFT:US",
      "type": "Bloomberg"
    },
    {
      "identifier": "MSFT.O",
      "type": "Reuters"
    },
    {
      "identifier": "NASDAQ:MSFT",
      "type": "Google"
    },
    {
      "identifier": "US5949181045",
      "type": "ISIN"
    },
    {
      "identifier": "microsoft-corporation",
      "type": "Knowsis"
    }
  ],
  "websocket_channel": "3a158d211ccb5a4cb1100000",
  "endpoints": {
    "themes": "http://api.knows.is/assets/microsoft-corporation/themes/",
    "content": "http://api.knows.is/assets/microsoft-corporation/content/",
    "sentiment": "http://api.knows.is/assets/microsoft-corporation/sentiment/"
  },
  "widgets": {
    "tweets": "https://insights.knows.is/widgets/tweets/microsoft-corporation/",
    "content": "https://insights.knows.is/widgets/content/microsoft-corporation/"
  }
}
```



