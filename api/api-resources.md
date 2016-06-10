---
title: API Objects
last_updated: June 8, 2016
sidebar: api_sidebar
permalink: /api-objects/
---


## Asset List Object

The asset list object is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>meta</td><td>metadata object</td><td>paging metadata</td></tr>
    <tr><td>assets</td><td>list of asset objects</td><td>available assets</td></tr>
  </tbody>
</table>


## Metadata Object
The metadata object is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>page</td><td>int</td><td>requested/current page</td></tr>
    <tr><td>pagesize</td><td>int</td><td>requested page size</td></tr>
    <tr><td>items</td><td>int</td><td>number of items in the current page</td></tr>
    <tr><td>total_items</td><td>int</td><td>total items available</td></tr>
  </tbody>
</table>

## Asset Object
The asset object is made up of the following fields:


<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>name</td><td>string</td><td>display name for this asset</td></tr>
    <tr><td>identifiers</td><td>list of asset identifier object</td><td>list of asset identifier object</td></tr>
    <tr><td>websocket_channel</td><td>string</td><td>websocket channel to subscribe to for asset events</td></tr>
  </tbody>
</table>


## Asset Identifier Object


`Accept: application/json, text/javascript`

```
{
  "identifier": "$MMM", 
  "type": "Cashtag"
}
```


The asset identifier object is up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>identifier</td><td>string</td><td>identifier value</td></tr>
    <tr><td>type</td><td>list of asset identifier object</td><td>type of identifier</td></tr>
  </tbody>
</table>

## Asset Sentiment Object

The asset sentiment object is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>name</td><td>string</td><td>name for the asset</td></tr>
    <tr><td>identifier</td><td>string</td><td>identifier used in the request</td></tr>
    <tr><td>startdate</td><td>datetime</td><td>the start date of the datapoint range returned</td></tr>
    <tr><td>enddate</td><td>datetime</td><td>the end date of the datapoint range returned</td></tr>
    <tr><td>datapoints</td><td>list of datapoint objects</td><td>datapoint</td></tr>
  </tbody>
</table>


## Datapoint Object
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
  }
}
```


The datapoint object is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>date</td><td>datetime</td><td>date which datapoint relates to</td></tr>
    <tr><td>sentiment</td><td>sentiment object</td><td>sentiment value</td></tr>
    <tr><td>volume</td><td>volume object</td><td>volume value</td></tr>    
    <tr><td>tweet counts</td><td>tweet count object</td><td>raw tweet counts</td></tr>    
  </tbody>
</table>


## Sentiment Object
```
{
  "sentiment": {
    "current": 64,
    "previous": 58,
    "change": -6
  }
}
```

The sentiment object is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>current</td><td>integer</td><td>sentiment for the current period</td></tr>
    <tr><td>previous</td><td>integer</td><td>sentiment for the previous period</td></tr>
    <tr><td>change</td><td>integer</td><td>absolute change between current and previous sentiment values</td></tr>
  </tbody>
</table>


## Tweet Counts Object
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

The tweet counts object is made up of the following fields:


<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>positive</td><td>integer</td><td>count of tweets with positive sentiment</td></tr>
    <tr><td>negative</td><td>integer</td><td>count of tweets with negative sentiment</td></tr>
    <tr><td>neutral</td><td>integer</td><td>count of tweets with neutral sentiment</td></tr>
    <tr><td>total</td><td>integer</td><td>total count of tweets</td></tr>
  </tbody>
</table>


## Volume Object

```
{
  "volume":{
    "change": -36
  }
}
```



The volume object is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>change</td><td>integer</td><td>change from normal social conversation volume level</td></tr>    
  </tbody>
</table>




## Theme List Object

The theme list object is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>themes</td><td>list of theme objects</td><td>list of themes for the requested asset</td></tr>
  </tbody>
</table>

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

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>title</td><td>string</td><td>Theme title</td></tr>
  </tbody>
</table>

```
{
    "title": "Theme Title"
}
```