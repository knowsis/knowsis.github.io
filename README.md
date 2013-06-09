**Table of Contents**

- [What is the Knowsis API?](#what-is-the-knowsis-api)
  - [Technical Overview](#technical-overview)
	- [Authentication](#authentication)
	- [Response Formats](#response-formats)
- [API Endpoints](#api-endpoints)
	- [List Assets](#get-assets)
		- [Example Request/Response](#example-requestresponse)
		- [Asset List Resource](#asset-list-resource)
	- [Asset Details](#get-assetsidentifier)
		- [Example Request/Response](#example-requestresponse-1)
		- [Asset Resource](#asset-resource)
		- [Asset Identifier Resource](#asset-identifier-resource)
	- [Asset Sentiment](#get-assetsidentifiersentiment)
		- [Example request/response](#example-requestresponse-2)
		- [Asset Sentiment Resource](#asset-sentiment-resource)
		- [Datapoint Resource](#datapoint-resource)
		- [Sentiment Resource](#sentiment-resource)
		- [Volume Resource](#volume-resource)
		- [Demographics Resource](#demographics-resource)
	- [Asset Themes](#get-assetsidentifierthemes)
		- [Example request/response](#example-requestresponse-3)
		- [Theme List Resource](#theme-list-resource)
		- [Theme Resource](#theme-resource)
- [Asset Identifiers](#asset-identifiers)
	- [Notes](#notes)
- [Errors](#errors)


***


# What is the Knowsis API?

The Knowsis API allows developers to add Knowsis analytics to their website and applications. Knowsis sentiment data is derived from 1000s of online sources and is generated through our own proprietary machine learning algorithms. 

We make the sentiment of 100s of publicly traded assets (equities, commodities, indices, forex pairs) and non tradable assets (macro drivers, pre IPO companies etc) available, as well as providing social demographics of the type of people that are discussing each asset.

## Technical Overview

Our API is accessible via HTTP, is RESTful, and offers both JSON, XML and plain text response formats (find the schemas below). All data responses are UTF-8 encoded.

We presently offer sentiment data for the current day.

Times and dates are provided in UTC timezone and are in ISO 8601 format.


## Authentication
We use OAuth for authentication. As all resources are protected, you must sign every request you make using your API consumer key and secret, as per the OAuth Consumer Request 1.0 Draft 1 specification. We strongly recommend using an existing OAuth library.

The following parameters MUST appear in every request:

**oauth_consumer_key** - The consumer key provided to you by Knowsis
**oauth_nonce** - A random string of characters that differs from call to call (this helps to prevent replay attacks) be sure to make these characters legal (percent-encoded) 
**oauth_timestamp** - The number of seconds elapsed since midnight, 1 January 1970. Be sure this is within ten minutes of the real time
**oauth_signature_method** - The method used to generate the signature. We currently only support HMAC-SHA1
**oauth_signature** - You generate the signature by passing into a cryptographic function your consumer key, your shared secret, and an encoded version of the "base string" 


The oauth_version parameter is optional; the value will be assumed to be 1.0 if it is not provided.

## Response Formats

We can render responses for you using JSON, XML or plain text. 

The default format is JSON

In order to specify your choice of response format use a standard HTTP Accept header.


```Accept: application/json, text/javascript```

```Accept: application/xml, text/xml```

```Accept: text/plain```


***


# API Endpoints

Access to the Knowsis API is available through a RESTful interface

The Knowsis API is available for registered users at http://api.knowsis.com/. To register an account contact api@knowsis.com

## List Assets

The assets endpoint will return an asset list resource containing all available asset resources.

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



### Example Request/Response

JSON Response

```
GET http://api.knows.is/assets/
Accept: application/json, text/javascript
```

```
{
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

XML Response

```
GET http://api.knows.is/assets/
Accept: application/xml, text/xml
```

```
<response>
  <assets>
    <asset>
      <name>Anglo American PLC</name>
      <type>Equity</type>
      <identifiers>
        <identifier>
          <value>AAL:LN</value>
          <type>Bloomberg</type>
        </identifier>
        <identifier>
          <value>AAL.L</value>
          <type>Reuters</type>
        </identifier>
        <identifier>
          <value>GB00B1XZS820</value>
          <type>ISIN</type>
        </identifier>
      </identifiers>
    </asset>
    <asset>
      <name>ARM Holdings PLC</name>
      <type>Equity</type>
      <identifiers>
        <identifier>
          <value>ARM:LN</value>
          <type>Bloomberg</type>
        </identifier>
        <identifier>
          <value>ARMH:US</value>
          <type>Bloomberg</type>
        </identifier>
      </identifiers>
    </asset>
  </assets>
</response>
```


Plain Text Response

```
GET http://api.knows.is/assets/
Accept: text/plain
```

```
name: Anglo American PLC"
type: Equity
id:Bloomberg:AAL:LN
id:Reuters:AAL.L
id:ISIN:GB00B1XZS820 

name: ARM Holdings PLC
type: Equity
id:BloomBerg|ARM:LN
id:BloomBerg|ARMH:US
```



###Asset List Resource
The asset list resource is made up of the following fields:


<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>assets</td><td>list of asset resources</td><td>available assets</td></tr>
  </tbody>
</table>


## Asset Details

The asset endpoint will return a single asset based on the specified {identifier} value. 

### Example Request/Response

JSON Response

```
GET http://api.knows.is/assets/ARM.L/
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

XML Response

```
GET http://api.knows.is/assets/ARM.L/
Accept: application/xml, text/xml
```

```
<response>
    <name>ARM Holdings PLC</name>
    <identifiers>
      <identifier>
        <value>ARM:LN</value>
        <type>Bloomberg</type>
      </identifier>
      <identifier>
        <value>ARMH:US</value>
        <type>Bloomberg</type>
      </identifier>
    </identifiers>
</response>
```

Plain Text Response

```
GET http://api.knows.is/assets/ARM.L/
Accept: text/plain
```

```
name:ARM Holdings PLC
identifier:BloomBerg|ARM:LN
identifier:BloomBerg|ARMH:US
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

Accept: application/xml, text/xml
```
<identifier>
  <value>$MMM</value>
  <type>"Cashtag</type>
</identifier>
```

Accept: text/plain
id:Cashtag|$MMM



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

For API consumers that have access to historical sentiment data there are optional parameters to get sentiment for a specified date range


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
GET http://api.knows.is/assets/$ARMH/sentiment/?startdate=20121231&enddate=20130101
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
      },
      "demographics": {
        "gender": {
          "Male": 64,
          "Female": 8,
          "unspecified": 28
        },
        "location": {
          "North America": 23,
          "South America": 0,
          "Europe": 38,
          "Africa": 0,
          "Asia": 22,
          "Australasia": 5,
          "unspecified": 12
        }
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
      },
      "demographics": {
        "gender": {
          "Male": 64,
          "Female": 8,
          "unspecified": 28
        },
        "location": {
          "North America": 23,
          "South America": 0,
          "Europe": 38,
          "Africa": 0,
          "Asia": 22,
          "Australasia": 5,
          "unspecified": 12
        }
      }
    }
  ]
}
```

XML Response

```
GET http://api.knows.is/assets/$ARMH/sentiment/?start=20121231&end=20130101
Accept: application/xml, text/xml
```

```
<response>
    <name>ARM Holdings PLC</name>
    <identifier>$ARMH</identifier>
    <startdate>2012-12-31T00:00:00Z</startdate>
    <enddate>2013-01-01T00:00:00Z</enddate>
    <datapoints>
      <datapoint>
        <date>2013-01-01T00:00:00Z</date>
        <sentiment>
          <current>50</current>
          <previous>12</previous>
          <change>38</change>
        </sentiment>
        <volume>
          <change>106</change>
        </volume>
        <demographics>
          <genders>
            <gender name="Male">64</gender>
            <gender name="Female">8</gender>
            <gender name="unspecified">28</gender>
          </genders>
          <locations>
            <location name="North America">23</location>
            <location name="Europe">38</location>
            <location name="South America">0</location>
            <location name="Asia">22</location>
            <location name="Africa">0</location>
            <location name="Australasia">5</location>
            <location name="unspecified">12</location>
          </locations>
        </demographics>
      </datapoint>
      <datapoint>
        <date>2012-12-31T00:00:00Z</date>
        <sentiment>
          <current>12</current>
          <previous>1</previous>
          <change>11</change>
        </sentiment>
        <volume>
          <change>5</change>
        </volume>
        <demographics>
          <genders>
            <gender name="Male">64</gender>
            <gender name="Female">8</gender>
            <gender name="unspecified">28</gender>
          </genders>
          <locations>
            <location name="North America">23</location>
            <location name="Europe">38</location>
            <location name="South America">0</location>
            <location name="Asia">22</location>
            <location name="Africa">0</location>
            <location name="Australasia">5</location>
            <location name="unspecified">12</location>
          </locations>
        </demographics>
      </datapoint>
    </datapoints>
  </response>
```


Plain Text Response

```
GET http://api.knows.is/assets/$ARMH/sentiment/?start=20121231&end=20130101
Accept: text/plain
```

```
name: ARM Holdings PLC
identifier:$ARMH
startdate:2012-12-31T00:00:00Z
enddate:2013-01-01T00:00:00Z

date:2013-01-01T00:00:00Z
sentiment:current:-26
sentiment:previous:-24
sentiment:change:-2
volume:change:-20
gender:Male:64
gender:Female:8
gender:unspecified:28
location:North America:28
location:Europe:38

date:2012-12-31T00:00:00Z
sentiment:current:-24
sentiment:previous:-2
sentiment:change:-22
volume:change:12
gender:Male:45
gender:Female:32
gender:unspecified:23
location:Asia:82
location:South America:18
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
  },
  "demographics": {
    "gender": {
      "Male": 64,
      "Female": 8,
      "unspecified": 28
    },
    "location": {
      "North America": 23,
      "South America": 0,
      "Europe": 38,
      "Africa": 0,
      "Asia": 22,
      "Australasia": 5,
      "unspecified": 12
    }
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
    <tr><td>demographics</td><td>demographics resource</td><td>demographics</td></tr>
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



### Demographics Resource

```
"demographics": {
  "gender": {
    "Male": 64,
    "Female": 8,
    "unspecified": 28
  },
  "location": {
    "North America": 23,
    "South America": 0,
    "Europe": 38,
    "Africa": 0,
    "Asia": 22,
    "Australasia": 5,
    "unspecified": 12
  }
}
```

The demographics resource is made up of the following fields:

<table>
  <thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead>
  <tbody>
    <tr><td>gender</td><td>gender resource</td><td>percentage split of conversation by gender</td></tr>    
    <tr><td>location</td><td>location resource</td><td>percentage split of conversation by location</td></tr>    
    <tr><td>classification</td><td>classification resource</td><td>percentage split of conversation by user classification</td></tr>    
  </tbody>
</table>


#### Note
For some users of social media platforms like Twitter it is not possible to accurately identify a gender (e.g. business accounts) or a location so in these cases we use “unspecified” as the returned value.


## Asset Themes

The asset themes endpoint will return a list of themes for the asset based on the specified {identifier} value. 

### Example request/response
JSON Response

```
GET http://api.knows.is/assets/$ARMH/themes/
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
          "title": "the title of the theme"
        }
      ]
    },
    {
      "date": "2013-01-02T00:00:00Z",
      "themes": [
        {
          "title": "the title of the first theme"
        },
        {
          "title": "the title of the next theme"
        }
      ]
    }
  ]
}
```

XML Response

```
GET http://api.knows.is/assets/$ARM/themes/
Accept: application/xml, text/xml
```

```
<response>
    <name>ARM Holdings PLC</name>
    <identifier>$ARMH</identifier>
    <startdate>2013-01-01T00:00:00Z</startdate>
    <enddate>2013-01-01T00:00:00Z</enddate>
    <dailythemes>
      <dailytheme>
        <date>2013-01-01T00:00:00Z</date>
        <themes>
          <theme>
            <title>this is the title of the theme</title>
          </theme>
          <theme>
            <title>this is another theme’s title</title>
          </theme>
        </themes>
      </dailytheme>
      <date>2013-01-02T00:00:00Z</date>
        <themes>
          <theme>
            <title>this is the title of the theme</title>
          </theme>
          <theme>
            <title>this is another theme’s title</title>
          </theme>
        </themes>
      </dailytheme>
    </dailythemes>
</response>
```

Plain Text Response

```
GET http://api.knows.is/assets/ARM.L/themes/
Accept: text/plain
```
```
name:ARM Holdings PLC
identifier:ARM.L
startdate:2013-01-01T00:00:00Z
enddate:2013-01-01T00:00:00Z

date:2013-01-01T00:00:00Z
theme:title:this is the title of the theme
theme:title:this is another theme’s title

date:2013-01-02T00:00:00Z
theme:title:this is the title of the theme
theme:title:this is another theme’s title
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


