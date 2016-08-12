---
title: Push API
last_updated: June 8, 2016
sidebar: api_sidebar
permalink: /websockets/
---


We make a websockets channel available for each asset to receive push notifications of any updates to that asset. 
The id of the websocket channel can be found in the [asset object](/api-objects#asset-object]) of the asset list or asset details endpoints.

The websocket channels are used to power our own [Social Insights](http://insights.knows.is) product and as such some of the events may not be relevant for your own use case.


## Pusher

We have partnered with [Pusher](http://www.pusher.com) to provide our push api infrastucture. 

In order to connect to our websockets you can use one the many SDKs that Pusher provide for interacting with their systems. Full details can be found [here](https://pusher.com/docs/libraries)


### Credentials

In order to connect to the websocket channels you will need an app id, key and secret which we will provide. Please contact [support@knowsis.com](mailto:support@knowsis.com) with your request for an app key and your use case.


## Message Types

We will send the following message types via the websocket channel:

### anomaly_alert_triggered

The anomaly_alert_triggered event will be sent out whenever an anomaly alert for the asset is raised. The payload of the alert will be the alert identifier and the datetime for when the alert was triggered.

```javascript
{
    "alert_id": "57602570f3d4f757039a14ef"
    "trigger_time": "2016-06-02T14:57:56",
    "credibility": "high"
}
```

Credibility is a score as to whether the content is from, or has been retweeted by a credible source. Credible sources are accounts that have been identified by Knowsis proprietary systems as credible within the area of capital markets. This can be used for filtering if you only want to show alerts that are considered to be credible. Values currently returned are either "high", "medium" or "unknown".


To display the content of an alert you can use the [Alert HTML Widget](/widget-alert/) which accepts the alert id as an 


### anomaly_alert_removed

In the event that our systems revoke an anomaly alert due to more information received, we will fire an anomaly_alert_removed event. The payload of the alert will be the identifier for the alert that has been revoked.

```javascript
{
    'alert_id': '57602570f3d4f757039a14ef'
}
```

This message is only relevant if you are storing or displaying a list of alerts to your end users.


### datapoint

A datapoint event will be sent out whenever the normalised volume and/or sentiment for the asset has changed. The payload of this message will be the sentiment ([simple](/api-asset-sentiment/#simple-sentiment)) & volume ([normalised](/api-asset-sentiment/#normalised-volume)).


```javascript
{
    'sentiment': 2,
    'volume': 2.1
}
```

### tweets

The tweets and remove_tweets events can be ignored as they are used by the [Tweet Stream HTML Widget](/widget-tweet-stream/) and we are not currently able to deliver tweets directly via the API due to Twitter's licensing agreements.

If you require a tweet stream in your application you should use the Tweet Stream HTML Widget which provides the latest tweets for each asset and will automatically update when new tweets are available.

### top_content


A top_content event will be sent out whenever there has been a change to the content for the asset. At the moment the payload of this message will be empty and will rely on you making your own call back to our [asset_content](/api-asset-content/) endpoint to retrieve the updated top content. 


```javascript
{}
```

Alternativey you can use the [Top Content HTML Widget](/widget-top-content/) which provides the aggregated content for the last 6 hours and will automatically update when new content is available.


### price

A price data event will be sent out whenever the price of an asset changes. The price data in the price message is delayed.


```javascript

{    
    high: 13.96,
    last: 13.9501,
    last_trade: "2016-06-23T11:34:00",
    low: 13.82,
    open: 13.84,
    previous_close: "13.6100",
    volume: 32801805
}


```

## Network Security

For information on firewall whitelisting requirements please contact [support@knowsis.com](mailto:support@knowsis.com)
