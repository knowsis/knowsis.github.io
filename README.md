Knowsis API Documentation
=================


# What is the Knowsis API?

The Knowsis API allows developers to add Knowsis content to their website and applications. Knowsis sentiment data is derived from 1000s of online sources and is generated through our own proprietary machine learning algorithms. 

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

The Knowsis API is available at http://api.knows.is/

## GET /assets/

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



Example Request/Response

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


### GET /assets/{IDENTIFIER}/

The asset endpoint will return a single asset based on the specified {identifier} value. 

Example Request/Response

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


Asset Resource
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

Field
Type
Description
identifier
string
identifier value
type
string
type of identifier




GET /assets/{IDENTIFIER}/sentiment/

The asset sentiment endpoint will return a list of sentiment resources. The default view is the current day’s sentiment data for a single asset based on the specified {identifier} value. The date which the data refers to is also returned in the request

For API consumers that have access to historical sentiment data there are optional parameters to get sentiment for a specified date range

Parameter
Format
Description
startdate
date - (YYYYMMDD)
the first day in the requested range
enddate
date - (YYYYMMDD)
the last day of the requested range

The asset sentiment endpoint will adhere to the following behaviour:

1) If no start date or end date is provided the data will be for the current day only.
2) If there is no start date, the data will be returned for the end date only.
3) If there is no end date, the data range will span from the start date provided up until the current day.
4) If the start date is after the end date, the start date will be ignored and the API will adhere to the step 3.

Example request/response
JSON Response

GET http://api.knows.is/assets/$ARMH/sentiment/?startdate=20121231&enddate=20130101
Accept: application/json, text/javascript

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

GET http://api.knows.is/assets/$ARMH/sentiment/?start=20121231&end=20130101
Accept: application/xml, text/xml

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

Field


Description
name
string
display name for this asset
identifier
string
identifier used in the request
startdate
datetime
the start date of the datapoint range returned
enddate
datetime
the end date of the datapoint range returned
datapoints
list of datapoint resources
datapoint

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

Field
Type
Description
date
datetime
date which datapoint relates to
sentiment
sentiment resource
sentiment
volume
volume resource
volume
demographics
demographics resource
demographics


Sentiment Resource
```
  "sentiment": {
    "current": 64,
    "previous": 58,
    "change": -6
  }
```

The sentiment resource is made up of the following fields:

Field
Type
Description
current
integer
sentiment for the current period
Sentiment ranges from -50 (extremely bearish) to 50 (extremely bullish)
previous
integer
sentiment for the previous period
Sentiment ranges from -50 (extremely bearish) to 50 (extremely bullish)
change
string
absolute change between current and previous sentiment values

Volume Resource

```
  "volume":{
    "change": -36
  }
```



The sentiment resource is made up of the following fields:

Field
Type
Description
change
string
percentage change from normal social conversation volume level


Demographics Resource

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

Field
Type
Description
gender
gender resource
percentage split of conversation by gender
location
location resource
percentage split of conversation by continent
classification
classification resource
percentage split of conversation by user classification

For some users of social media platforms like Twitter it is not possible to accurately identify a gender (e.g. business accounts) or a location so in these cases we use “unspecified” as the returned value.
GET /assets/{IDENTIFIER}/themes/

The asset themes endpoint will return a list of themes for the asset based on the specified {identifier} value. 

Example request/response
JSON Response

GET http://api.knows.is/assets/$ARMH/themes/
Accept: application/json, text/javascript

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

GET http://api.knows.is/assets/$ARM/themes/
Accept: application/xml, text/xml

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

GET http://api.knows.is/assets/ARM.L/themes/
Accept: text/plain

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

Theme List Resource

The theme list resource is made up of the following fields:

Field
Type
Description
themes
list of theme resources
list of themes for the requested asset

Theme Resource

The theme resource is made up of the following fields:

Field
Type
Description
title
string
Theme title



Asset Identifiers
We support several publicly available identifiers for retrieving details of the assets that we track. A full list of available identifiers can be found using the /assets/ endpoint to fetch a list of all assets.

The following common ticker symbol formats are currently supported in requests for individual assets:

AAPL:US
AAPL.0
NASDAQ:AAPL
APPL


we also support the most common social media format, the StockTwits/Twitter cashtag:

$GOOG


and International Securities Identification Numbers (ISIN): 

US0378331005


Macro and asset driver topics do not have a ticker symbol or ISIN code so you will need to refer to these by the Knowsis proprietary identifiers which can be found by calling the /assets/ endpoint. 



Notes 

As identifiers may contain reserved characters, you should ensure that the identifier has been url encoded before being sent to the API.


Errors

In the event of a problem with your request you will receive an error response

As much as possible, Knowsis attempts to use the appropriate HTTP status codes to indicate the general class of problem. We will also provide a body to the request in the requested format with more details on the problem where available. You should handle errors in your application and present your end users with a more friendly response than the error messages provided here.

Error Message
Description
400 (Bad Request)
Any case where a parameter is invalid, or a required parameter is missing. This includes the case where OAuth parameters are not provided.
401 (Unauthorized)
The OAuth signature was provided but was invalid.
403 (Forbidden)
Access to the requested resource was refused by the server. Your api account does not have permissions to access the request resource.
404 (Not Found)
The requested resource does not exist.
405 (Method Not Allowed)
Attempting to use POST with a GET-only endpoint, or vice-versa.
409 (Conflict)
The request could not be completed as it is. Use the information included in the response to modify the request and retry.
500 (Internal Server Error)
Our servers are having problems. The request is probably valid but needs to be retried later.

Example error response body

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

The error resource is made up of the following fields:

Field
Type
Description
errorCode
string
The relevant HTTP error code
errorMessages
list of strings
List of human readable error messages

Additional details are provided in the errorMessages part of the error resource. It should be one of the following types of errors.

Error Message
Description
Missing OAuth parameter
The case where any of the required OAuth parameters are not provided. we will also specify the name of parameter that is missing.
Invalid OAuth Consumer
The provided OAuth Consumer key was not valid
Signature verification failed
The provided OAuth signature did not match that generated by the server.



