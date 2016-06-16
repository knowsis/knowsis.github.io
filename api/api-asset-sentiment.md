---
title: Asset Sentiment
last_updated: June 8, 2016
sidebar: api_sidebar
permalink: /api-asset-sentiment/
---

The asset sentiment endpoint will return a list of sentiment objects. The default view is the current day’s sentiment data for a single asset based on the specified {identifier} value. The date which the data refers to is also returned in the request

```
GET /assets/{identifier}/sentiment/
```

For API consumers that have licensed our historical sentiment data there are optional parameters to get sentiment for a specified date range

<table>
  <thead><tr><th>Parameter</th><th>Format</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>startdate</td><td>date - (YYYYMMDD)</td><td>the first day in the requested range</td></tr>
    <tr><td>enddate</td><td>date - (YYYYMMDD)</td><td>the last day in the requested range</td></tr>
  </tbody>
</table>

The asset sentiment endpoint will adhere to the following behaviour:

1. If no start date or end date is provided the data will be for the current day only.
2. If there is no start date, the data will be returned for the end date only.
3. If there is no end date, the data range will span from the start date provided up until the current day.
4. If the start date is after the end date, the start date will be ignored and the API will adhere to the step 3.

### Example request/response

```
GET https://api.knows.is/assets/$ARMH/sentiment/?startdate=20121231&enddate=20130101
Accept: application/json, text/javascript
```

```
{
  "name": "ARM Holdings PLC",
  "identifier": "$ARMH",
  "startdate": "2012-12-31T00:00:00Z",
  "enddate": "2013-01-02T00:00:00Z",
  "datapoints": [
    {
      "date": "2013-01-01T00:00:00Z",
      "sentiment": {
        "current": -19,
        "previous": -4,
        "change": -15
      },
      "volume": {
        "change": 6
      }      
    },
    {     
      "date": "2012-12-31T00:00:00Z",     
      "sentiment": {
        "current": -4,
        "previous": -40,
        "change": 36
      },
      "volume": {
        "change": 456
      }
    }
  ]
}
```
