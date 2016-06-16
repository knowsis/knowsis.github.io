---
title: API Objects
last_updated: June 8, 2016
sidebar: api_sidebar
permalink: /api-objects/
---


## Asset List Object

The asset list object is made up of the following fields:


| Field             | Type   | Description                                                   |
|-------------------|--------|---------------------------------------------------------------|
| meta              | object | [metadata object](#metadata-object)                           |
| assets            | list   | list of available [asset](#asset-object) objects              |



## Metadata Object
The metadata object is made up of the following fields:


| Field             | Type   | Description                                                   |
|-------------------|--------|---------------------------------------------------------------|
| page              | integer| requested/current page                                        |
| pagesize          | integer| requested page size                                           |
| items             | integer| number of items in the current page                           |
| total_items       | integer| total items available                                         |


```
{
  "meta":{
    "page":1,
    "pagesize": 100,
    "items": 2,
    "total_items": 2
  }
}

```



## Asset Object
The asset object is made up of the following fields:

| Field             | Type   | Description                                                   |
|-------------------|--------|---------------------------------------------------------------|
| name              | string | display name for this asset                                   |
| identifiers       | list   | list of [identifier objects](#asset-identifier-object)        |
| websocket_channel | string | websocket channel identifier to subscribe to for asset events |
| endpoints         | string | [endpoints object](#endpoints-object)                         |
| widgets           | string | [widgets object](#widgets-object)                             |


```
{

    "name": "Anglo American PLC",
    "identifier": "anglo-american-plc",    
    "identifiers": [
      {
        "identifier": "AAL:LN",
        "type": "Bloomberg"
      },
      
      {
        "identifier": "GB00B1XZS820",
        "type": "ISIN"
      }
    ],
    "websocket_channel": "3a158d211ccb5a4cb1100000",
    "endpoints": {
      "themes": "http://api.knows.is/assets/anglo-american-plc/themes/",
      "content": "http://api.knows.is/assets/anglo-american-plc/content/",
      "sentiment": "http://api.knows.is/assets/anglo-american-plc/sentiment/"
    },
    "widgets": {
      "tweets": "https://insights.knows.is/widgets/tweets/anglo-american-plc/",
      "content": "https://insights.knows.is/widgets/content/anglo-american-plc/"
    }

}
```



## Asset Identifier Object
The asset object is made up of the following fields:

| Field      | Type   | Description         |
|------------|--------|---------------------|
| identifier | string | identfier value     |
| type       | string | type of identifier  |

```
{
    "identifier": "GB00B1XZS820",
    "type": "ISIN"
} 
```

## Endpoints Object

A list of available endpoint urls for a given asset


| Field             | Type   | Description                                                   |
|-------------------|--------|---------------------------------------------------------------|
| themes            | string | url to request for asset themes                               | 
| content           | string | url to request for asset content                              |
| sentiment         | string | url to request for asset sentiment                            |

```
{
    "themes": "http://api.knows.is/assets/anglo-american-plc/themes/",
    "content": "http://api.knows.is/assets/anglo-american-plc/content/",
    "sentiment": "http://api.knows.is/assets/anglo-american-plc/sentiment/"
}

```

## Widgets Object

A list of available HTML widget urls for a given asset

| Field             | Type   | Description                                                   |
|-------------------|--------|---------------------------------------------------------------|
| content           | string | url to request asset content widget                           |
| tweets            | string | url to request asset tweets widget                            |

```

{
    "tweets": "https://insights.knows.is/widgets/tweets/anglo-american-plc/",
    "content": "https://insights.knows.is/widgets/content/anglo-american-plc/"
}
```

## Asset Sentiment Object

The asset sentiment object is made up of the following fields:


| Field             | Type    | Description                                                   |
|-------------------|---------|---------------------------------------------------------------|
| name              | string  | name of the requested sset                                    |
| identifier        | string  | identifier used in the request                                |
| startdate         | datetime| the start date of the datapoint range returned                |
| enddate           | datetime| the end date of the datapoint range returned                  |
| datapoints        | list    | list of [datapoint objects](#datapoint-object)                |

```
{
  "name": "ARM Holdings PLC",
  "identifier": "$ARMH",
  "startdate": "2012-01-01T00:00:00Z",
  "enddate": "2013-01-01T00:00:00Z",
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
    }
  ]
}

```

## Datapoint Object

The datapoint object is made up of the following fields:

| Field             | Type    | Description                                                   | Optional |
|-------------------|---------|---------------------------------------------------------------|:--------:|
| date              | datetime| date which datapoint relates to                               |          |
| sentiment         | object  | [sentiment object](#sentiment-object)                         |     *    |
| volume            | object  | [volume object](#volume-object)                               |     *    |
| tweet counts      | object  | [tweet counts object](#tweet-counts-object)                   |     *    |

Depending on your API package you may not receive all fields in the datapoint object, speak to your account manager or contact [support@knowsis.com](mailto:support@knowsis.com) for more information.


```
{
  "date": "2013-01-01T00:00:00Z",
  "sentiment": {
    "current": -19,
    "previous": -4,
    "change": -15
  },
  "volume": {
    "change": 6
  },
  "tweet_counts":{
    "positive": 1,
    "negative": 1,
    "neutral": 1,
    "total": 3,
  }
}
```

## Sentiment Object


The sentiment object is made up of the following fields:

| Field             | Type    | Description                                                   | Optional |
|-------------------|---------|---------------------------------------------------------------|:--------:|
| current           | integer | sentiment for the current period                              |          |
| previous          | integer | sentiment for the previous period                             |     *    |
| change            | integer | absolute change between current and previous sentiment values |     *    |





```
{
  "sentiment": {
    "current": 64,
    "previous": 58,
    "change": -6
  }
}
```


## Volume Object

The volume object is made up of the following fields:

| Field             | Type    | Description                                                   | Optional |
|-------------------|---------|---------------------------------------------------------------|:--------:|
| change            | integer | change from normal social conversation volume level           |          |


```
{
  "volume":{
    "change": -36
  }
}
```

## Tweet Counts Object


The tweet counts object is made up of the following fields:

| Field             | Type    | Description                              |
|-------------------|---------|------------------------------------------|
| positive          | integer | count of tweets with positive sentiment  |
| negative          | integer | count of tweets with negative sentiment  |
| neutral           | integer | count of tweets with neutral sentiment   |
| total             | integer | total count of tweets                    |


```
{
    "tweet_counts": {
        "positive": 12,
        "negative": 67,
        "neutral": 123,
        "total": 202
    }
}
```

## Theme List Object

The theme list object is made up of the following fields:

| Field    | Type  | Description                                                    |
|----------|-------|----------------------------------------------------------------|
| themes   | list  | list of [theme objects](#theme-object) for the requests asset  |


```
{
  "themes":[
    {"title": "Theme 1"},
    {"title": "Theme 2"}
  ]
}
```


## Theme Object

The theme object is made up of the following fields:

| Field    | Type   | Description      |
|----------|--------|------------------|
| title    | string | Theme title      |


```
{
    "title": "Theme Title"
}
```