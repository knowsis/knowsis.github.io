---
title: Assets
last_updated: June 10, 2016
sidebar: api_sidebar
permalink: /api-assets/
---

## List Assets


The list assets endpoint will return an asset list object containing all asset objects available to your account. Asset lists can be paged to return upto 100 assets at a time

```
GET /assets/
```

There are also four asset list filter endpoints which will only return assets of the requested type:


<table>
  <thead><tr><th>Endpoint</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>equities</td><td>list of asset objects</td><td>A list of equities</td></tr>
    <tr><td>commodities</td><td>list of asset objects</td><td>A list of commodities</td></tr>
    <tr><td>indices</td><td>list of asset objects</td><td>A list of indices</td></tr>
    <tr><td>forex</td><td>list of asset objects</td><td>A list of forex pairs</td></tr>
  </tbody>
</table>

```
GET /equities/

GET /commodities/

GET /indices/

GET /forex/
```



### Example request/response

JSON Response

```
GET https://api.knows.is/assets/
Accept: application/json, text/javascript
```

```
{
  "meta":{
    "page":1,
    "pagesize": 100,
    "items": 2,
    "total_items": 2
  },
  "assets": [
    {
      "name": "Anglo American PLC",
      "type": "Equity"
      "identifiers": [
        {
          "identifier": "AAL:LN",
          "type": "Bloomberg"
        },
        {
          "identifier": "AAL.L",
          "type": "Reuters"
        },
        {
          "identifier": "GB00B1XZS820",
          "type": "ISIN"
        }
      ]
    },
    {
      "name": "ARM Holdings PLC",
      "type": "Equity",
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
  ]
}
```

