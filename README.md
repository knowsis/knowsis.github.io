**Table of Contents**

- [What is the Knowsis API?](#what-is-the-knowsis-api)
  - [Technical Overview](#technical-overview)
	- [Authentication](#authentication)
	- [Response Formats](#response-formats)
  - [API Clients](#api-clients)
- [API Endpoints](#api-endpoints)
	- [List Assets](#get-assets)
		- [Example request/response](#example-requestresponse)
		- [Asset List Resource](#asset-list-resource)
		- [Metadata Resource](#metadata-resource)
	- [Asset Details](#get-assetsidentifier)
		- [Example request/response](#example-requestresponse-1)
		- [Asset Resource](#asset-resource)
		- [Asset Identifier Resource](#asset-identifier-resource)
	- [Asset Sentiment](#get-assetsidentifiersentiment)
		- [Example request/response](#example-requestresponse-2)
		- [Asset Sentiment Resource](#asset-sentiment-resource)
		- [Datapoint Resource](#datapoint-resource)
		- [Sentiment Resource](#sentiment-resource)
		- [Volume Resource](#volume-resource)		
	- [Asset Themes](#get-assetsidentifierthemes)
		- [Example request/response](#example-requestresponse-3)
		- [Theme List Resource](#theme-list-resource)
		- [Theme Resource](#theme-resource)
- [Insights Endpoints](#insights-endpoints)
	- [Asset Tweets](#get-tweets)
- [Asset Identifiers](#asset-identifiers)
- [Errors](#errors)


***


# What is the Knowsis API?

The Knowsis API allows developers to add Knowsis analytics to their website and applications. Knowsis sentiment data is derived from 1000s of online sources and is generated through our own proprietary machine learning algorithms. 

We make the sentiment of 100s of publicly traded assets (equities, commodities, indices, forex pairs) and non tradable assets (macro drivers, pre IPO companies etc) available.

## Technical Overview

Our API is accessible via HTTPS, is RESTful, and offers JSON response formats (find the schema below). All data responses are UTF-8 encoded.

We presently offer sentiment data for the current day.

Times and dates are provided in UTC timezone and are in ISO 8601 format.


## Authentication
We use OAuth for authentication. As all resources are protected, you must sign every request you make using your API consumer key and secret, as per the OAuth Consumer Request 1.0 Draft 1 specification. We strongly recommend using an existing OAuth library. The [oauth.net](http://www.oauth.net/code) website lists suggested libraries by language.

The following parameters MUST appear in every request:

+ **oauth_consumer_key** - The consumer key provided to you by Knowsis
+ **oauth_nonce** - A random string of characters that differs from call to call (this helps to prevent replay attacks) be sure to make these characters legal (percent-encoded)
+ **oauth_timestamp** - The number of seconds elapsed since midnight, 1 January 1970. Be sure this is within ten minutes of the real time
+ **oauth_signature_method** - The method used to generate the signature. We currently only support HMAC-SHA1
+ **oauth_signature** - You generate the signature by passing into a cryptographic function your consumer key, your shared secret, and an encoded version of the "base string"


The oauth_version parameter is optional; the value will be assumed to be 1.0 if it is not provided.

## Response Formats

We can render responses for you using JSON. 

The default format is JSON

In order to specify your choice of response format use a standard HTTP Accept header.


```
Accept: application/json, text/javascript

```


## API Clients

We currently offer a python API Client (pyknowsis) which is available from pypi. 

```
pip install pyknowsis

```

You can also get the latest version of the source code from our [github repository](http://www.github.com/knowsis/pyknowsis).


Documentation is also available on the [github repository](https://github.com/knowsis/pyknowsis/blob/master/README.md)




***


# API Endpoints

Access to the Knowsis API is available through a RESTful interface

The Knowsis API is available for registered users at https://api.knowsis.com/. To register an account contact api@knowsis.com

## List Assets


The list assets endpoint will return an asset list resource containing all asset resources available to your account. Asset lists can be paged to return upto 100 assets at a time

```
GET /assets/
```

There are also four asset list filter endpoints which will only return assets of the requested type:


<table>
  <thead><tr><th>Endpoint</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>equities</td><td>list of asset resources</td><td>A list of equities</td></tr>
    <tr><td>commodities</td><td>list of asset resources</td><td>A list of commodities</td></tr>
    <tr><td>indices</td><td>list of asset resources</td><td>A list of indices</td></tr>
    <tr><td>forex</td><td>list of asset resources</td><td>A list of forex pairs</td></tr>
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

###Asset List Resource

The asset list resource is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>meta</td><td>metadata resource</td><td>paging metadata</td></tr>
    <tr><td>assets</td><td>list of asset resources</td><td>available assets</td></tr>
  </tbody>
</table>


### Metadata Resource
The metadata resource is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>page</td><td>int</td><td>requested/current page</td></tr>
    <tr><td>pagesize</td><td>int</td><td>requested page size</td></tr>
    <tr><td>items</td><td>int</td><td>number of items in the current page</td></tr>
    <tr><td>total_items</td><td>int</td><td>total items available</td></tr>
  </tbody>
</table>


## Asset Details

The asset endpoint will return a single asset based on the specified {identifier} value. 

```
GET /assets/{identifier}/
```

### Example request/response

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


### Asset Resource
The asset resource is made up of the following fields:


<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>name</td><td>string</td><td>display name for this asset</td></tr>
    <tr><td>identifiers</td><td>list of asset identifier resource</td><td>list of asset identifier resource</td></tr>
  </tbody>
</table>


### Asset Identifier Resource


`Accept: application/json, text/javascript`

```
{
  "identifier": "$MMM", 
  "type": "Cashtag"
}
```


The asset identifier resource is up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>identifier</td><td>string</td><td>identifier value</td></tr>
    <tr><td>type</td><td>list of asset identifier resource</td><td>type of identifier</td></tr>
  </tbody>
</table>


## Asset Sentiment

The asset sentiment endpoint will return a list of sentiment resources. The default view is the current day’s sentiment data for a single asset based on the specified {identifier} value. The date which the data refers to is also returned in the request

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

#### Example request/response

JSON Response

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



### Asset Sentiment Resource

The asset sentiment resource is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>name</td><td>string</td><td>name for the asset</td></tr>
    <tr><td>identifier</td><td>string</td><td>identifier used in the request</td></tr>
    <tr><td>startdate</td><td>datetime</td><td>the start date of the datapoint range returned</td></tr>
    <tr><td>enddate</td><td>datetime</td><td>the end date of the datapoint range returned</td></tr>
    <tr><td>datapoints</td><td>list of datapoint resources</td><td>datapoint</td></tr>
  </tbody>
</table>


### Datapoint Resource
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


The datapoint resource is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>date</td><td>datetime</td><td>date which datapoint relates to</td></tr>
    <tr><td>sentiment</td><td>sentiment resource</td><td>sentiment value</td></tr>
    <tr><td>volume</td><td>volume resource</td><td>volume value</td></tr>    
  </tbody>
</table>


### Sentiment Resource
```
  "sentiment": {
    "current": 64,
    "previous": 58,
    "change": -6
  }
```

The sentiment resource is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>current</td><td>integer</td><td>sentiment for the current period</td></tr>
    <tr><td>previous</td><td>integer</td><td>sentiment for the previous period</td></tr>
    <tr><td>change</td><td>integer</td><td>absolute change between current and previous sentiment values</td></tr>
  </tbody>
</table>



### Volume Resource

```
  "volume":{
    "change": -36
  }
```



The volume resource is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>change</td><td>integer</td><td>change from normal social conversation volume level</td></tr>    
  </tbody>
</table>



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



### Theme List Resource

The theme list resource is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>themes</td><td>list of theme resources</td><td>list of themes for the requested asset</td></tr>
  </tbody>
</table>


### Theme Resource

The theme resource is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>title</td><td>string</td><td>Theme title</td></tr>
  </tbody>
</table>



***

# Insights Endpoints

Access to the Insights endpoints is via the same oAuth credentials as the Knowsis data API above. This API is responsible for rendering more visual elements such as widgets and graphs.

## Asset Tweets

This endpoint will return a widget containing the most recent tweets for a particular {identifier}, and will auto-update via javascript as new tweets become available. High-level analytics such as sentiment & volume will also be visible  depending on subscription level.

```
GET /assets/w/{identifier}/
```

The following are optional query string parameters 

|Field|Type|Description|
|-----|----|-----------|
|css|encoded url|the https url to a stylesheet be injected into the <head> of the response for client styling|


### Example request

```
GET https://insights.knows.is/assets/w/$ARM/?css=https://www.client.com/style.css
Accept: text/html
```


<p>The html will be styled as follows and any of the CSS classes can be styled:</p>

```html
<html>

<body>
<div class="container">
    <div class=" app-container">
        <div id="ARMH " class="tweets-view-container ">
            <ul class="tweets-list ">
                <li class="tweet-container">
                    <div class="tweet-title-container">
                        <a href="https://twitter.com/intent/user?screen_name=HalftimeReport">
                            <div class="tweet-profile-icon"><img
                                    src="https://testinsights.knows.is/external/twitter_profile/?url=https://pbs.twimg.com/profile_images/590580807753986049/fhYEXRiC_normal.png"
                                    width="15px" height="15px" alt="User Image"></div>
                            <div class="tweet-profile">CNBC Halftime Report</div>
                            <div class="tweet-username">@HalftimeReport</div>
                        </a>
                        <a class="tweet-date-link" href="https://twitter.com/HalftimeReport/status/738400580079517697"
                           target="_blank">
                            <div class="tweet-date" data-created="2016-06-02T16:03:11"
                                 title="Thu, 2 Jun 2016 16:03:11 +0100">2 minutes
                            </div>
                        </a>
                    </div>
                    <div class="tweet-content">
                        Best days behind for Apple? $AAPL
                        <a href="http://twitter.com/HalftimeReport/status/738400580079517697/photo/1"
                           class="link-primary media-url" target="_blank">pic.twitter.com/7a00FrhTaK</a>

                        <div class="tweet-media">
                            <a href="http://twitter.com/HalftimeReport/status/738400580079517697/photo/1"
                               target="_blank">
                                <img class="img-responsive"
                                     src="https://testinsights.knows.is/external/image/?url=https://pbs.twimg.com/media/Cj9TaZsWgAAKCIM.jpg"
                                     alt="Image attached to this tweet">
                            </a>
                        </div>
                    </div>
                </li>
            </ul>
        </div>
        <div id="powered-by-knowsis ">
            Powered by <a href="http://knowsis.com " target="_blank " title="Knowsis | Actionable Web Intelligence ">Knowsis</a>
        </div>
    </div>
</div>
</body>

</html>
```

<p>The "Powered By Knowsis" section must not be styled, moved or hidden without prior agreement.</p>

### Images

By default images attached to a tweet are shown and links to these images are hidden.

If you want to hide images and display links instead, add the following css to your stylesheet:

```css
.media-url {
	display: inline;
}

.tweet-media {
	display: none;
}
```

***

# Asset Identifiers

We support several publicly available identifiers for retrieving details of the assets that we track. A full list of available identifiers can be found using the /assets/ endpoint to fetch a list of all assets.

The following common ticker symbol formats are currently supported in requests for individual assets:

```
AAPL:US
AAPL.0
NASDAQ:AAPL
APPL
```

we also support the most common social media format, the Twitter cashtag:

```
$GOOG
```

and International Securities Identification Numbers (ISIN): 

```
US0378331005
```

Macro and asset driver topics do not have a ticker symbol or ISIN code so you will need to refer to these by the Knowsis proprietary identifiers which can be found by calling the /assets/ endpoint. 



### Notes 

As identifiers may contain reserved characters, you should ensure that the identifier has been url encoded before being sent to the API.


***

# Errors

In the event of a problem with your request you will receive an error response

As much as possible, Knowsis attempts to use the appropriate HTTP status codes to indicate the general class of problem. We will also provide a body to the request in the requested format with more details on the problem where available. You should handle errors in your application and present your end users with a more friendly response than the error messages provided here.



<table>
  <thead><tr><th>Error Message</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>400 (Bad Request)</td><td>Any case where a parameter is invalid, or a required parameter is missing. This includes the case where OAuth parameters are not provided.</td></tr>
    <tr><td>401 (Unauthorized)</td><td>The OAuth signature was provided but was invalid.</td></tr>
    <tr><td>403 (Forbidden)</td><td>Access to the requested resource was refused by the server. Your api account does not have permissions to access the request resource.</td></tr>
    <tr><td>404 (Not Found)</td><td>The requested resource does not exist.</td></tr>
    <tr><td>405 (Method Not Allowed)</td><td>Attempting to use POST with a GET-only endpoint, or vice-versa.</td></tr>
    <tr><td>409 (Conflict)</td><td>The request could not be completed as it is. Use the information included in the response to modify the request and retry.</td></tr>
    <tr><td>500 (Internal Server Error)</td><td>Our servers are having problems. The request is probably valid but needs to be retried later.</td></tr>
  </tbody>
</table>




Example error response body
```
{
  "error": {
    "errorCode": "400",
    "errorMessages": [
      "Missing parameter OAuth Consumer",
      "Missing parameter OAuth Nonce",
      "Missing parameter OAuth Signature"
    ]
  }
}
```

The error resource is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>errorCode</td><td>integer</td><td>The relevant HTTP error code</td></tr>
    <tr><td>errorMessages</td><td>list of strings</td><td>List of human readable error messages</td></tr>
  </tbody>
</table>


Additional details are provided in the errorMessages part of the error resource. It should be one of the following types of errors.

<table>
  <thead><tr><th>Error Message</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>Missing OAuth parameter</td><td>The case where any of the required OAuth parameters are not provided. we will also specify the name of parameter that is missing.</td></tr>
    <tr><td>Invalid OAuth Consumer</td><td>The provided OAuth Consumer key was not valid</td></tr>
    <tr><td>Signature verification failed</td><td>The provided OAuth signature did not match that generated by the server.</td></tr>
    
  </tbody>
</table>


